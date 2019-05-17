---
title: web端地图坐标拾取工具
date: 2019-05-17 05:41:47
tags:
- 地图
- Map
- 坐标拾取
- Coordination picking
- 工具
- tool
categories:
- 地图
---

## 摘要
Web端地图遍地开花，一些坐标拾取工具质量参差不齐，为了提高地理学科研人员的寻找坐标数据的效率，本文对当前的主流Web端地图：谷歌、高德、Bing地图的API进行了研究，通过建立定制化在线地图，仅调用其检索工具、地理坐标、高程函数，对地图的坐标数据进行提取，并以简介的界面呈现，从而实现了精简的坐标拾取小工具。


**关键词：谷歌地图、高德地图、BingMap、Web端、地理坐标、高程、拾取**


<!--More -->

## 前言
地图坐标是地理学工作研究重要的数据之一，近年来虽然出现了很多的地图开发商及软件，但他们大部分是商业应用型，兼顾了主流的消费需求，但限于个国家之间的政策，并没有很好地给出地图数据获取的方式，仅提供了一下接口，保留其科研性质。一些网络上的坐标拾取工具也由这些接口应用而生，但质量上良莠不齐，较好的会趋向收费，这不仅浪费了地理学科研人员寻找可靠数据的时间，而且增加了其成本，由此需要一个能够批量导出坐标拾取点数据的专业地图网站。

## 相关工作
网上的坐标拾取工具较多，但商业化严重，这里列举一些坐标拾取工具并简单介绍。
+ [奥维地图](http://www.gpsov.com/cn/main.php)是一个商业化的软件，采用谷歌和百度两种主流地图作为底图，在服务器端自架构了谷歌地图的自动提示检索模块，可以在GFW情况下提示检索关键词；给一些事业单位提供坐标服务，包含坐标的批量查询、导入、导出，GNSS定位存储。
+ [GPSspg](http://www.gpsspg.com/maps.htm)也是一个商业化软件，提供有偿数据服务，地图的地图杂糅了当前的谷歌、百度、腾讯、高德、图吧等主流地图，且提供IP、基站、身份证、手机号码等查询。
+ [去何地](http://haiba.qhdi.com)则是一个旅游者发烧友自建一个网站，以谷歌地图为地图，提供坐标查询。


## 开发原理
JavaScript/JS+CSS+HTML
这里就不过多讲述了，毕竟这只是本人的业余爱好项目。
概括一下是：HTML是整个网页的基础框架，其中有W3C的标准，主要包含：head、body两大部分，近些年来也开始支持HTML5了；CSS是整个HTML网页版面的布局样式文件，确定某一id、class元素的属性，布局在左上、右上、居中还是左下、右下、居中，更加深究一点就是是不是有阴影、圆角、SVG图等等；JS则是动态脚本，通过结合官方API,可以在线调用在官方服务器上的JS函数库，实现各种操作，当然请求这些函数库往往需要开发Key，这需要申请一个并激活。

## Web端地图生成
这里也不太过多讲述，下面给出一个流程图更加言简意赅。
流程大致如下：
+ 1）官网上申请地图开发密钥；
+ 2）浏览官网给出的样例Demo；
+ 3）熟悉参考手册的JS函数及回调结果数据结构；
+ 4）制定开发地图的页面布局及模块功能；
+ 5）在样例里找定制的模块功能代码、或者查找相关的博客借用其相关模块；
+ 6）编写地图Alpha版本并调试；
+ 7）调试通过后进行网页部署并测试；
+ 8）测试通过后正式发布Beta版本；
+ 9）后期升级、维护。

本实验调用了Google/高德/Bing等地图的API，提供坐标的拾取，检索，页面相对简洁，没有一点商业化的意图，仅提供给地理学科研人员，可以拾取经纬度、高程（仅Google）。

## 测试结果
Web端发布在三个平台，包括：github/gitee/coding.net。
+ github是国外最有名的代码托管平台；
+ gitee/coding.net则是国内模仿github的代码托管平台。
因为国外受限于GWF网络，所以选择了两个国内的备用。
在网页版和移动端均测试了其页面布局、操作响应等方面，均达到了可以发布的标准（我也不清楚啥标准）。
截图：

Google Map 截图
![](http://muchongimg.xmcimg.com/oss2/img/2018/0602/bw186h3459653_1527908688_401.png)

![](http://muchongimg.xmcimg.com/oss2/img/2018/0602/bw188h3459653_1527908701_650.png)

Gaode Map 截图
![](http://muchongimg.xmcimg.com/oss2/img/2018/0602/bw188h3459653_1527908699_307.png)
![](http://muchongimg.xmcimg.com/oss2/img/2018/0602/bw188h3459653_1527908699_569.png)


Bing Map 截图

![](http://muchongimg.xmcimg.com/oss2/img/2018/0602/bw188h3459653_1527908700_793.png)

## 总结

网页部署在github等代码托管平台的静态网页中，无需管理费等地图维护费用，相比于其他的坐标拾取网站，本实验不单节约了运营成本，简化了数据获取的流程，将有利于各地理学科研工作人员的数据获取。同时本实验将三个地图分开部署，会在一定程度上对数据的比较产生不便利。本实验中对数据现在仅能提高人工打点方式获取，工作量依然很大，后期可能会进行自动化的完善。坐标拾取也将会朝着自动化获取方向发展，只要用户输入几个关键词，工具批量下载其坐标数据。

更新后的大地图地址为（地图加载的框架文件较多，需要较长时间，请耐心等待）：

http://leaguecn.coding.me/maxmap/

2018-09-29,提供另外一个地图，基于AcrGIS JS API/HERE tile/GoogleMap tile

http://leaguecn.coding.me/GeoMap/

**欢迎批评指正，如有bug或者不满意，请邮件与我联系。**

---------------------

## 其他

找地图 
+ https://leaguecn.github.io/resume/

直连
+ Google: http://leaguecn.gitee.io/map/
+ Bing: https://leaguecn.github.io/bingmap/
+ 高德：http://leaguecn.coding.me/amaplite/

## 参考

+ http://muchong.com/t-12381369-1
+ http://lbsyun.baidu.com/index.php?title=jspopular
+ https://lbs.amap.com/api/javascript-api/summary
+ https://www.bing.com/api/maps/mapcontrol/isdk/
+ https://developers.google.com/maps/documentation/javascript/tutorial

