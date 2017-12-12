---
layout: post
title: 高德/百度地图路段车流速率抓取 Speed Scraping in Amap/Baidu Map
date: 2017-12-12
categories: blog
tags: [专业知识]
description: 
---

## 整体思路

百度地图和高德地图都提供了路径规划Web服务接口功能。该功能将用户输入的起点、终点经纬度坐标和路径规划方式（最短路，考虑路况的最短路等）等参数传入服务器，并在服务器中进行计算，最终返回以起终点经纬度所确定的路径的驾驶时耗以及路径长度等信息。根据路径长度及路径耗时信息，可以推断出某时刻下该路段上行车大致平均速率。


## 相关地图API

**批量算路服务API（百度地图）**

批量算路服务（又名Route Matrix API）是一套以HTTP/HTTPS形式提供的轻量级批量算路接口，用户可通过该服务，根据起点和终点，返回路线规划距离和行驶时间{\ref}。
<center>
<img src="https://fuerdi2.github.io/img/speedScraping/baiduPLSL.jpg" width = "50%">
图1：百度批量算路服务示意图
</center>

**路径规划API（高德地图）**

路径规划API是一套以HTTP形式提供的步行、公交、驾车查询及行驶距离计算接口，返回JSON 或 XML格式的查询数据，用于实现路径规划功能的开发{\ref}。 与百度地图类似，用户输入参数，系统返回计算的结果（规划距离、行驶时间等）。
<center>
<img src="https://fuerdi2.github.io/img/speedScraping/GDLJGH.jpg" width = "50%">
图2：高德地图路径规划服务示意图
</center>
 
## 基础数据准备

### 路网数据

在爬取互联网地图中路段车流速率之前，我们需要知道实际道路在百度/高德地图上的准确位置。在网络地图中，道路由多边形或者多段线构成，多段线的顶点以及多段线的端点坐标能够唯一确定一条道路。 

实际工作中，能够直接获取并使用的路网数据来源于国内外测绘部门与科研机构发布的cad文件或者是shp文件，这些路网的坐标系通常为WGS-84、CGS2000、Xian84等。基于这些坐标系测绘的路网数据通常不能直接用于互联网地图开发，因为高德地图采用的是基于WGS84坐标系加密的GCJ02坐标系，而百度地图在GCJ02坐标系上进行了再一次加密，其使用的坐标系为BD坐标系。

在使用路网数据之前，必须对路网经纬度进行适当的坐标转换，方能匹配至互联网地图中。

### 分段

车流密度及速度在道路上的分布是不均匀的，为了提高数据精度，我们需要将长路段分成多个采样片段。

<center>
<img src="https://fuerdi2.github.io/img/speedScraping/traffic_density.jpg" width = "50%">
图3：异侧车道流密度不均
</center>

<center>
<img src="https://fuerdi2.github.io/img/speedScraping/traffic_density2.jpg" width = "50%">
图4：同侧车道流密度不均
</center>

人为的在一条道路上确定若干个采样点（sample point），对道路进行分段操作。

<center>
<img src="https://fuerdi2.github.io/img/speedScraping/segment.jpg" width = "50%">
图5：采样点及道路分段
</center>

### 采样点纠偏

由于坐标转换误差及测量精度问题，采样点在互联网地图中的位置与实际位置可能会发生偏离。我们需要识别出这些误差点，将误差点匹配至正常位置。采样点纠偏通常有两种方法：路径长度校核法以及路径判断校核法。

**路径长度校对法**

通过比较两点间的路径在互联网地图上的长度与其实际长度（CAD文件提供），若两者差异较大，则判断采样点落在了错误的位置。

<center>
<img src="https://fuerdi2.github.io/img/speedScraping/WZPL.png" width = "50%">
图6：长度校对机制 图中当采样点发生偏移，车辆驾驶路径长度为发生较大变化
</center>

**路径判断校对法**

在爬取互联网地图中路段车流速率之前，我们需要知道路段的准确位置。在网络地图中，路段由多边形或者多段线构成。 路段的具体数据我们无从得知，但是我们能够获得测绘局提供的WGS-84坐标系下的某城市路网拓扑结构。这些路网由多段线构成，一般来说：线为道路，点为交叉口。这样，我们就可以根据现有的路网拓扑资料，经过互联网地图（百度地图、高德地图）提供的坐标转换API功能，将路网（线与点）与互联网地图匹配。
<center>
<img src="https://fuerdi2.github.io/img/speedScraping/WZPL.png" width = "50%">
图7：路径判断机制 图中当采样点发生偏移，车辆驾驶路径不为直线
</center>
### Web API批处理

对于采样点纠偏的两种方法，我们都能够进行Web编程，来快速识别出这些异常点。

**长度校核法**
通过Web请求，可以获得json/xml的路径规划数据。高德地图路径规划策略有多种，在这里我们选择路径最短策略（不考虑耗时）。
通常需要设置一个长度差距阈值，来作为异常点判断的准则。一般来说，城市道路中交叉口最短间距离约为70米，根据采样点实际应用中的密度（相邻采样点间距为50米），综合给出阈值为70米。程序将路径长度与实际长度距离差距大于70米的路径点识别出来。
<center>
<img src="https://fuerdi2.github.io/img/speedScraping/CDJD.png" width = "50%">
图8：长度关键词
</center>

**路径判断法**


通过Web请求，可以获得json/xml的路径规划数据。高德地图路径规划策略有多种，在这里我们选择路径最短策略（不考虑耗时）。提取请求返回结果中导航指引信息，判断路径是否存在绕路现象。从返回结果可知，判断路径是否绕路的关键信息为：返回结果中包含词语“掉头”。
<center>
<img src="https://fuerdi2.github.io/img/speedScraping/LJPD.png" width = "50%">
图9：路径关键词
</center>
