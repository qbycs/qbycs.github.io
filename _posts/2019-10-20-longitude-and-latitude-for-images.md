---
type: page
title: 根据照片和轨迹提取采集号经纬度流程
tags: 电脑知识
key: longitude-and-latitude-of-image
---

<!--more-->

```
准备工作：每日野外考察工作开始前，根据手机时间校对相机时间。
```

## 1. 获取照片和轨迹数据 
- 轨迹使用[两步路手机APP](http://www.2bulu.com/about/app_download2.htm?id=0)记录，可从手机应用商店下载。
## 2. 将轨迹的经纬度写入到照片属性
- 将两步路的KML格式的轨迹转为GPX格式，可使用以下两种方法：
1. 使用软件[RouteConverter](https://www.routeconverter.com/stable-releases/en)，该软件免安装，可直接使用，使用流程较为简单，打开轨迹后，直接在文件菜单下选择另存为即可。
![image](https://github.com/qbycs/qbycs.github.io/blob/master/image/blog/2019-10-20-longitude-and-latitude-for-images/snipaste_2019-08-06_17-50-38.jpg?raw=true)
![image](https://github.com/qbycs/qbycs.github.io/blob/master/image/blog/2019-10-20-longitude-and-latitude-for-images/snipaste_2019-08-06_17-49-24.jpg?raw=true)
2. 使用在线网站[kml2gpx](https://kml2gpx.com)直接转换
![image](https://github.com/qbycs/qbycs.github.io/blob/master/image/blog/2019-10-20-longitude-and-latitude-for-images/snipaste_2019-08-06_17-52-51.jpg?raw=true)
- 通过软件[GPicSync](https://sourceforge.net/projects/gpicsync/)将轨迹中的经纬度和海拔写入到照片属性 
![image](https://github.com/qbycs/qbycs.github.io/blob/master/image/blog/2019-10-20-longitude-and-latitude-for-images/snipaste_2019-08-07_09-06-19.jpg?raw=true)
1. 选择照片文件夹
2. 选择轨迹文件
3. 选择时区补偿，中国为UTC+8。
```
两步路app记载轨迹的时间格式为格林尼治时间加时区，但是转换格式的软件不会自动补偿为北京时间，此处加上时区补偿即可避免修改轨迹文件时间内容。
```
4. 指定照片轨迹匹配最大时间差，默认5分钟，轨迹记录时间和和照片拍摄时间查过该值则不予匹配，如果匹配效果差可以调大或调小。
5. 同步，同步速度较慢，需耐心。同步完成后，照片属性则出现经纬度和海拔信息，写入好经纬度信息如下：
![image](https://github.com/qbycs/qbycs.github.io/blob/master/image/blog/2019-10-20-longitude-and-latitude-for-images/snipaste_2019-08-07_09-33-05.jpg?raw=true)
## 3. 提取图片经纬度属性信息
```
需首先对照片进行重命名，重命名格式为**为物种编号（样方/样线编号+空格+三位数序号）+照片原始编号**
```
GPicSync完成后会在原文件夹生成一个doc.kml的记录文件，在该文件夹内有每张照片的经纬度和海拔信息，需从里面提取每张照片的经纬度和海拔信息。
具体实现方法如下：
- 使用记事本打开doc.kml文件，删除文件头和尾，仅剩下每张图片的位置描述，每个照片均有10行的描述说明（包括空行1行）
```
<Placemark>
<name>IMG_1674.JPG</name>
<description><![CDATA[<img src='img_1674.jpg' width='600' height='400'/>]]>
</description>
<styleUrl>#defaultStyle1</styleUrl><Style><IconStyle><Icon><href>thumbs/thumb_IMG_1674.JPG</href></Icon></IconStyle></Style>
<Point>
<coordinates>117.4579892,30.0474718,1726.3</coordinates>
</Point>
</Placemark>
```
- 需从上述文件中，批量提出第二行的文件名和第7行的经纬度信息。
- 方法如下，将上述描述块粘贴入word中，使用文字转表格功能，列宽为10即可，然后见所需列粘贴入excel中，删除<name>...</name>,<coordinates>...</coordinates>字段。
## 4. 将每张照片的信息列表缩减为每个采集号的列表
每个采集号常包含多张照片，此处仅保留每个采集号的首张照片，即可获得每个采集号的采集信息。
处理方式如下：

- 将每张照片的名字中的采集号进行分列提取，会得到一个仅含采集号的列，对该列使用Countif函数（=countif（$A$1：A1=A1)）进行计数，所有返回值大于1的行全部删除即可。