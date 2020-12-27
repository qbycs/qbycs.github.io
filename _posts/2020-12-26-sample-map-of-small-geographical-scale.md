---
type: page
title: 小地理范围的采集示意图制作方法
tags: 图表制作
key: sample-map-of-small-geographical-scale
---

近期，由于个人文章需要在小地理范围地形图上标注采样点，即一个精准位置标注的采样示意图。之前在中国地图上直接手动粗糙地标注采集点的方法已经难以满足当前较为严格的需求，经过一番查找琢磨，此处介绍一个基于ArcGis的采样示意图的制作方法，权当本人学习过程中的记录，以免遗忘。如能帮助他人，也算善事。

<!--more-->

## 1. 制图需求和效果展示

此此的个人制图需求有四点：

- 标注采集点的地图应为卫星影像地形图，可直观地显示海拔高低和山脉走势
- 采集点以经纬度的方式直接导入，可保精准无虞
- 采集点可以分组显示不同的标志，以示区别
- 图片边缘可额外显示经纬度和比例尺，以示地理位置和地理尺度

一些类似的已发表图片的效果如下：

![demo1](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/demo1.jpg){:.shadow} 

> 图片来源[在此](https://academic.oup.com/sysbio/article/65/6/947/2281629?login=true)

![demo2](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/demo2.jpg){:.shadow} 

> 图片来源[在此](https://www.researchgate.net/profile/Yan_Chen63/publication/338575760_Sky_islands_as_foci_for_divergence_of_fig_trees_and_their_pollinators_in_South-West_China/links/5e6230fda6fdcc37dd07b263/Sky-islands-as-foci-for-divergence-of-fig-trees-and-their-pollinators-in-South-West-China.pdf)

## 2. 地形图的获取

虽然以上示例图的地理范围较大，但仍易知，这类图的制作可分为三步：

1. 获取所需位置的地形图底图
2. 导入经纬度采样点集，并给予不同的标识
3. 制作经纬度边框、比例尺、指北针等等。

以上三步均可以在ArcGis中较为方便地完成。此处已经默认ArcGis已经装好，否则可以参考[此处](https://www.jb51.net/softs/682047.html)。下面就开始介绍在ArcGis中获取地形底图的方法。地形底图一般使用谷歌影像底图和天地图，ArcGis中提供了直接添加底图的方式添加天地图，但是天地图近年来关闭了免费免密钥的接口，导致此法失效。此处我们通过加载WMTS服务器的方法间接实现。此方法需先注册天地图帐号。

### 2.1 注册天地图开发者帐号

点击天地图网站[官网](https://sso.tianditu.gov.cn/)，开始注册。

![register-of-tianditu](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/register-of-tianditu.jpg){:.shadow} 

注册完成后，进入[开发者控制台](https://console.tianditu.gov.cn/api/key)，**创建小程序**，应用名称和行业类别可自由填写，IP白名单可不填，**应用类型**选服务端，提交完成后即可查看API的key密钥。

![creat-app-in-tianditu](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/creat-app-in-tianditu.jpg){:.shadow} 

![key-api-of-tianditu](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/key-api-of-tianditu.jpg){:.shadow} 

### 2.2 在 ArcGis 中配置WMTS服务器

![add-WMTS-servers](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/add-WMTS-servers.jpg){:.shadow} 

1. 双击右侧的**添加WMTS服务器**

2. 在**URL**处填入天地图的服务器网址，此处的网址链接的即为天地图的影像图，注意不同的坐标系，如墨卡托和大地坐标系。一般来说，对于手机或者其他GPS设备接受到的经纬度数据，建议使用CGCS2000天地图影像类型。如果需要天地图其他类型的底图资源，可参考以下表格：

   | 服务器地址  | 天地图资源类型  |
   | --------------------------------------- | ---------------------------------- |
   | http://t0.tianditu.com/cia_w/esri/wmts  | 天地图影像注记（墨卡托，WGS1984）  |
   | http://t0.tianditu.com/img_w/esri/wmts  | 天地图影像（墨卡托，WGS1984）      |
   | http://t0.tianditu.com/cia_c/esri/wmts  | 天地图影像注记（经纬度，CGCS2000） |
   | http://t0.tianditu.com/img_c/esri/wmts  | 天地图影像（经纬度，CGCS2000）     |
   | http://t0.tianditu.com/cva_w/esri/wmts  | 天地图街道注记（墨卡托，WGS1984）  |
   | http://t0.tianditu.com/vec_w/esri/wmts | 天地图街道（墨卡托，WGS1984）      |
   | http://t0.tianditu.com/cva_c/esri/wmts  | 天地图街道注记（经纬度，CGCS2000） |
   | http://t0.tianditu.com/vec_c/esri/wmts  | 天地图街道（经纬度，CGCS2000）     |

3. 输入**参数和值**，参数为tk，值即为天地图开发者的API key。

4. **获取图层**

5. **确认**即可看到添加进去的在线地图服务，将该**图层直接拖入到左侧图层**即可看见影像图，至此，影像底图获取完成。

   ![show-img-layer](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/show-img-layer.jpg){:.shadow} 

## 3. 导入采集坐标点

### 3.1 采集点经纬度数据准备

数据格式准备极为简单，excel表格即可，首行Header可自由命名，经纬度格式为十进制，如下：

| lon      | lat      |
| -------- | -------- |
| 113.0389 | 24.90954 |
| 113.0376 | 24.90803 |
| 113.0378 | 24.9066  |
| 113.0381 | 24.90613 |
| 113.0385 | 24.90529 |

### 3.2 采集点经纬度数据导入

![input-of-sample-sites](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/input-of-sample-sites.jpg){:.shadow} 

1. 调出ArcToolbox工具箱，双击**ArcToolbox>转换工具>Excel>Excel 转表**。
2. 选择准备好的excel文件。
3. **确定**即可，需稍作等待即有结果显示，但是此时采集点并没有显示到影像图上，仍需进一步操作。

### 3.3 采集点经纬度数据显示

1. 在**数据图层上右键>显示XY数据**。

![show-xy-values](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/show-xy-values.jpg){:.shadow} 

2. 指定**X字段（经度列）和Y字段（纬度列）**，确定后即可显示采集点。一般经纬度为大地坐标系（CGCS2000），如果之前选择的天地图类型不是该种，需要在**编辑**处选择对应的坐标系。

![show-xy-values-1](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/show-xy-values-1.jpg){:.shadow} 

![show-sample-sites](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/show-sample-sites.jpg){:.shadow} 

3. 如果采集点需要分组区别显示，可以按类别多次导入。同次导入的一批采集点可以统一设置外观，包括形状、颜色、大小等等。

![modity-symbols-of-sample-sites](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/modity-symbols-of-sample-sites.jpg){:.shadow} 

## 4. 采集示意图注释

各种注释内容均在ArcGis的布局视图下操作，进入**布局视图**后，可选择合适的大小模板，或者**双击采集图**本身，即可拖动调节大小，同时结合**放大、缩小、手形拖拽工具、比例尺窗口**调整所需的大小和比例。

![modify-layout-size](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/modify-layout-size.jpg){:.shadow} 

### 4.1 经纬度边框

经纬度边框以格网的方式设置，在采集图上**右键>属性>格网>新建格网**，然后调整各种设置，呈现自己想要的样式。

![add-grid](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/add-grid.jpg){:.shadow} 

### 4.2 比例尺和指北针

布局视图下，**在菜单栏>插入**处，即可添加**比例尺和指北针**，样式亦可自由调整。

![add-scale-and-compass](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/add-scale-and-compass.jpg){:.shadow} 

### 4.4 图例

同样在布局视图下，在**菜单栏>插入**处，可插入**图例**，图例的位置、说明文字内容（需通过更改数据图层名称实现）及其字体、边框颜色、背景颜色、边框圆角等等。

![add-legend](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/add-legend.jpg){:.shadow} 

调整到自己满意时，即可通过**文件>导出地图**，可选取各种格式和分辨率，下图是本次示例的大致效果。

![demo-my](https://qbycs.coding.net/p/qbycs_clone/d/qbycs_clone/git/raw/master/image/blog/2020-12-26-sample-map-of-small-geographical-scale/demo-my.jpg){:.shadow} 

注意到ArcGis中的图例似乎没有较为常用的透明度选项。所以可以导出不带图例的图片，自行在Photoshop或者PPT中调整，也较为方便。同时，这里的经度的**东**，纬度的**北**，都是使用的中文（应该是跟随软件语言），不适合英文期刊发表，也可导出pdf格式再使用类似的Adobe Acrobat Pro的pdf编辑器调整。自此，一张小地理范围的、带有地形图的、同时标注经纬度范围和比例尺的采样示意图就完成了（其实这只是我个人的需求）。