---
layout: post
title: GeoServer基础要点
date: 2018-1-04
categories: blog
tags: [专业知识]
description: 
---

## 简介

GeoServer是 OpenGIS Web 服务器规范的 J2EE 实现，利用 GeoServer 可以方便的发布地图数据，允许用户对特征数据进行更新、删除、插入操作，通过 GeoServer 可以比较容易的在用户之间迅速共享空间地理信息。目前最新版本为2.12.1

## 安装（Windows为例）

>在安装之前，请确保计算机中已经安装好了JRE（Java运行环境）。GeoServer需要Java 8.0版本的运行环境。你可以在Oracle网站中下载[JRE8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)。

*目前GeoServer不支持Java 9，要了解更多关于Java版本的问题请参阅[Java Considerations](http://docs.geoserver.org/stable/en/user/production/java.html#production-java)*

1.进入GeoServer[下载界面](http://geoserver.org/download/)选择安装版本。如果不确定具体安装的版本，请选择[稳定版](http://geoserver.org/release/stable/)。
2.下载完后，双击打开安装文件，进入欢迎界面，点击下一步
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_welcome.png" width="60%">
欢迎界面
</center>

3.阅读条款，点击确定
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_license.png" width="60%">
许可条款
</center>

4.选择安装目录，如果C盘空间不紧张，建议使用默认路径
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_installdir.png" width="60%">
选择GeoServer的安装目录
</center>

5.点击下一步
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_startmenu.png" width="60%">
点击下一步
</center>

6.选择JRE安装主目录。一般来说GeoServer会自动检测JRE的安装目录，若未检测到JRE安装目录，请手动输入JRE的安装目录。

*务必选择JRE安装文件夹。通常，JRE安装文件夹为：C:\Program Files (x86)\Java\jre8；而不是：C:\Program Files (x86)\Java\jre8\bin\java.exe：*

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_jre.png" width="60%">
选择JRE安装文件夹
</center>

7.输入GeoServer数据存放文件夹，如果你是第一次使用GeoServer，请选择默认的数据文件夹
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_datadir.png" width="60%">
数据存放文件夹
</center>

8.设置GeoServer管理员用户名和密码。该用户名和密码用来登录GeoServer的**网页管理界面**（稍后有详解）

*默认用户名：admin；默认密码为：geoserver。建议修改默认用户名与密码并牢记它。*

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_creds.png" width="60%">
设置账号密码
</center>

9.选择GeoServer服务端口

*默认端口为8080。你可以设置任意未被占用的端口，比如：10000、9999等。*

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_port.png" width="60%">
设置端口
</center>

10.选择安装方式。

*Run manually：需要手动打开运行GeoServer，只有当前用户才能使用;Install as service:GeoServer将被注册成系统服务，任何用户都能使用。建议选择Install as service，以便管理。*
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_service.png" width="60%">
选择安装方式
</center>


11.确定，点击安装并完成安装
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/win_review.png" width="60%">
点击安装
</center>

## 网页管理界面

>Geoserver可以通过网页管理页面来管理配置GeoServer，包括添加数据、图层发布、设置服务等。

打开浏览器，在地址栏输入
>http:// *host*:*port*/geoserver
>其中host为安装GeoServer的地址，port为端口。一般为http:// localhost:8080/geoserver。

1.进入欢迎界面
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/web-admin.png" width="60%">
欢迎界面
</center>

2.输入安装GeoServer时设置的用户名和密码
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/login-page.png" width="60%">
登陆
</center>

### 图层预览

在图层预览页面中，您能够快速的预览发布的图层

1.点击**Layer Preview**，进入图层预览页面
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/layer-preview.png" width="60%">
图层预览
</center>

2.在这个页面，你可以通过点击**OpenLayers**来对某个图层进行预览。当点击**OpenLayers**后，图层会显示在浏览器的新窗口中。
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/openlayers.png" width="60%">
预览某个图层
</center>

### 发布shapefile文件

#### 数据准备

将待发布的*.shp文件（如果有prj投影文件，也一起放入其中）复制到GeoServer数据存放文件夹中（这里以street.shp文件为例）。数据存放文件夹默认为 /data_dir/data/。


#### 创建工作区

>一个工作区是组织某一类相似图层的容器。

1.进入网页管理页面。进入**数据**-**工作区**
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/workspace.png" width="60%">
工作区
</center>

2.点击**新建工作区**按钮。你需要输入名称及名称空间URL
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/create-workspace.png" width="60%">
新建工作区
</center>

3.输入名称nyc_roads,及名称空间URL地址http:// zuojh.com/nyc_roads。名称空间地址并不需要真实可用的地址
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/namespace.png" width="60%">
名称及名称空间
</center>

#### 添加数据存储

>工作区创建完毕后，我们需要添加数据存储。数据存储将“告知”GeoServer如何与shapefile文件进行连接。

1.进入网页管理页面。进入**数据**-**数据存储**
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/data-store.png" width="60%">
数据存储
</center>

2.点击**添加新的数据存储**按钮，选择**Shapefile**
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/new-data-source.png" width="60%">
添加新的数据存储
</center>

3.在下拉菜单选择工作区，给数据源命名。并选择存放在文件夹中的sreet.shp文件。
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/select-data-source.png" width="60%">
配置数据存储
</center>
点击保存。

4.在弹出的新建图层页面中，点击**发布**
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/new-layer.png" width="60%">
新建图层
</center>

5.编辑图层信息。编写简介、定义坐标、计算坐标范围等信息。

*若shp文件中定义了投影，则本机SRS中会自动显示坐标系统类型。若未定义坐标系统，则需要人为设定坐标。各类坐标的EPSG编码请参阅[spatial reference list](http://spatialreference.org/ref/epsg/?page=1)。*

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/edit-layer.png" width="60%">
编写简介信息
</center>

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/edit-layer2.png" width="60%">
定义坐标系以及计算坐标范围
</center>

6.点击页面顶部的**发布按钮**，设置发布样式。
*这里由于street.shp为多段线shp，所以样式中选择默认样式line。更多的样式规则请见[Stylng](http://docs.geoserver.org/stable/en/user/styling/)*
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/edit-publish.png" width="60%">
选择样式
</center>

点击保存按钮，保存发布的图层。

#### 预览发布的图层

为了验证图层是否发布成功，进入图层预览界面，点击**OpenLayers**预览图层。可以看到图层已经成功发布。
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/previewing-layer.png" width="60%">
预览发布的图层
</center>

## 数据库连接

在实际业务中，通常使用数据库系统来组织管理空间数据。因此需要将GeoServer与数据库进行连接，以便其能够访问数据库中的空间数据。这里以GeoServer连接Oracle数据库为例。

### 安装Oracle插件

由于许可问题，GeoServer中并未自带Oracle数据库连接工具。为了使GeoServer能够支持Oracle数据库连接，需要下载Oracle插件。

1.从[插件下载页面]()下载Oracle插件

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/extension-download.png" width="60%">
插件下载
</center>

2.将下载好的插件解压到GeoServer安装目录的**WEB-INF/lib**文件夹。并将racle数据库安装文件夹中的Oracle JDBC驱动（例如ojdbc8.jar）也复制到**WEB-INF/lib**文件夹

### 添加Oracle数据存储

1.Oracle插件安装完之后，新建数据源界面中就会多出连接Oracle数据库的选项
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/oracle-connected.png" width="60%">
oracle连接选项
</center>

2.点击添加**Oracle NG**数据存储，填写用于连接Oracle数据库的用户名，密码和端口号等信息。点击保存，完成Oracle数据库的连接。
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/oracle_conf.png" width="60%">
oracle连接配置
</center>

## SQL Views

从GeoServer 2.1.0版本开始，GeoServer就提供了SQL Views功能。SQL Views功能避免了在数据库中创建视图的繁琐。

### 创建SQL View

点击新建图层，在添加图层下拉框中选择连接的数据库
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/create-sqlview.png" width="60%">
创建SQL View页面
</center>

>数据库中目前存放着名为STREETNETWORK空间数据文件，该表具有**NAME**，**TYPE**等属性
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/table-view.png" width="60%">
STREETNETWORK表一览
</center>

点击配置新的SQL视图，进入SQL视图创建界面。

现在考虑这样一个实际场景：给定一个TYPE值，在图层中显示出具有该TYPE值的所有要素。我们在SQL语句中引入一个参数名'TYPE_CODE'，并设置默认值：比如3。确认空间参考系SRID是否正确，若不正确则需要手动修改。

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/sqlview-conf.png" width="60%">
参数化视图配置
</center>

设置完成后点击保存。

## 样式

图层中仅有线条还不够，你可能还想其能体现更多的信息，或者是让地图变得更加漂亮。这样，GeoServer的**样式**功能就发挥作用了。

### 样式文件说明

GeoServer中支持多种样式格式：
* Styled Layer Descriptor(SLD):OGC为地理信息系统制定的样式标准。
* Cascading Style Sheets(CSS):CSS样式，需要[插件](http://docs.geoserver.org/latest/en/user/styling/css/index.html#css)支持。
* YSLD:类似于SLD样式，提高了安全新，需要[ysld插件](http://docs.geoserver.org/latest/en/user/styling/ysld/index.html#ysld-styling)支持。
* MBStyle:基于json语法的样式，增强了兼容性，需要[mbstyle](http://docs.geoserver.org/latest/en/user/styling/mbstyle/index.html#mbstyle-styling)支持。

### 颜色

最典型的应用就是通过不同颜色，来表示道路的类型。这里以SLD格式为例，为地图设置样式。

1.点击**Styles**，进入新建样式界面
<center>
<img src="https://fuerdi2.github.io/img/GeoServer/style-page.png" width="60%">
新建样式界面
</center>

2.将样式命名为COLOR，选定工作区，在Style Editor中键入样式规则

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/style-edit.png" width="60%">
样式编辑
</center>

详细规则请参考[Styles](http://docs.geoserver.org/2.12.1/user/styling/sld/cookbook/lines.html)
```xml
<?xml version="1.0" encoding="ISO-8859-1"?>
<StyledLayerDescriptor version="1.0.0" 
    xsi:schemaLocation="http://www.opengis.net/sld StyledLayerDescriptor.xsd" 
    xmlns="http://www.opengis.net/sld" 
    xmlns:ogc="http://www.opengis.net/ogc" 
    xmlns:xlink="http://www.w3.org/1999/xlink" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <NamedLayer>
    <Name>COLOR-based line</Name>
    <UserStyle>
      <Title>COLOR</Title>
   <FeatureTypeStyle>
     <Rule>
       <Name>1</Name>
       <ogc:Filter>
         <ogc:PropertyIsEqualTo>
           <ogc:PropertyName>TYPE</ogc:PropertyName>
           <ogc:Literal>1</ogc:Literal>
         </ogc:PropertyIsEqualTo>
       </ogc:Filter>
       <LineSymbolizer>
         <Stroke>
           <CssParameter name="stroke">#009933</CssParameter>
         </Stroke>
       </LineSymbolizer>
     </Rule>
   </FeatureTypeStyle>
   <FeatureTypeStyle>
     <Rule>
       <Name>2</Name>
       <ogc:Filter>
         <ogc:PropertyIsEqualTo>
           <ogc:PropertyName>TYPE</ogc:PropertyName>
           <ogc:Literal>2</ogc:Literal>
         </ogc:PropertyIsEqualTo>
       </ogc:Filter>
       <LineSymbolizer>
         <Stroke>
           <CssParameter name="stroke">#0055CC</CssParameter>
         </Stroke>
       </LineSymbolizer>
     </Rule>
   </FeatureTypeStyle>
   <FeatureTypeStyle>
     <Rule>
     <Name>3</Name>
       <ogc:Filter>
         <ogc:PropertyIsEqualTo>
           <ogc:PropertyName>TYPE</ogc:PropertyName>
           <ogc:Literal>3</ogc:Literal>
         </ogc:PropertyIsEqualTo>
       </ogc:Filter>
       <LineSymbolizer>
         <Stroke>
           <CssParameter name="stroke">#FF0000</CssParameter>
         </Stroke>
       </LineSymbolizer>
     </Rule>
   </FeatureTypeStyle>
      <FeatureTypeStyle>
     <Rule>
     <Name>4</Name>
       <ogc:Filter>
         <ogc:PropertyIsEqualTo>
           <ogc:PropertyName>TYPE</ogc:PropertyName>
           <ogc:Literal>4</ogc:Literal>
         </ogc:PropertyIsEqualTo>
       </ogc:Filter>
       <LineSymbolizer>
         <Stroke>
           <CssParameter name="stroke">#00008b</CssParameter>
         </Stroke>
       </LineSymbolizer>
     </Rule>
   </FeatureTypeStyle>
      <FeatureTypeStyle>
     <Rule>
     <Name>5</Name>
       <ogc:Filter>
         <ogc:PropertyIsEqualTo>
           <ogc:PropertyName>TYPE</ogc:PropertyName>
           <ogc:Literal>5</ogc:Literal>
         </ogc:PropertyIsEqualTo>
       </ogc:Filter>
       <LineSymbolizer>
         <Stroke>
           <CssParameter name="stroke">#9400d3</CssParameter>
         </Stroke>
       </LineSymbolizer>
     </Rule>
   </FeatureTypeStyle>
  </UserStyle>
  </NamedLayer>
</StyledLayerDescriptor>
```
点击**图层**，选中之前发布的命名为street的图层，点击**发布**，将Default Style选定为COLOR，点击保存。再对该图层进行预览，发现样式已经生效

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/previewing-layer.png" width="40%"><img src="https://fuerdi2.github.io/img/GeoServer/style-preview.png" width="40%">
Before——After
</center>

### 比例尺图层

当图层比例尺缩小时，密集的路网将影响视觉效果。我们希望在小比例尺情况下，某些“类型”的道路不予显示，只展示路网的主要轮廓。我们需要在SLD样式文件中加入比例尺控制条件。

>规则：当比例尺小于1 : 273K时，不显示TYPE为4或5的道路。只需要在道路等级为4或5的Rule之中加入
```xml
<MaxScaleDenominator>273000</MaxScaleDenominator>
```
表示当比例尺大于1:273K时，该规则才起作用。相关的道路才会被绘制在地图中。

<center>
<img src="https://fuerdi2.github.io/img/GeoServer/scale-layer.png" width="40%"><img src="https://fuerdi2.github.io/img/GeoServer/scale-layer2.png" width="40%">
1:545K——1:273K
</center>

## 高性能缓存