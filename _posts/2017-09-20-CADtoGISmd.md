## CAD图纸转换为Shp

### 背景
计算机辅助设计（CAD）和地理信息系统（GIS）在工程设计，交通规划等领域应用广泛。在应用范围上，CAD主要应用于工程制图，建筑设计，项目规划设计；在交通规划中，城市控制性规划图、道路交通改进方案图等主要由CAD完成。而GIS系统在水文分析、地理分析、路径规划等领域中应用广泛。
 CAD和GIS在应用领域上的不同，体现了两者设计哲学的差异：

* CAD主要用于对客观还不存在的物体进行设计；
* GIS是对客观已经存在的物体进行建模，以理解、分析管理资源和实施。

在交通规划工作中，现状分析及规划评价过程涉及GIS设计哲学，而在创建规划客体这一过程中，则体现了CAD的设计哲学。

。

一个优秀的交通规划作品涉及大量的资料分析及数据分析。在交通规划过程中需要从大量的文件中提取出规划工作所需要的数据。其中，与交通相关数据一个重要来源渠道就是各级政府部门提供的城市道路规划图纸，城市土地规划图纸。这类图纸基本由CAD制作生成，通常只具备展示意义。由于CAD系统中分析功能存在的局限性，在CAD中想要对这类信息进行深度分析恐怕会非常困难。然而，各级部门现有的资料绝大多数为CAD文件，因此，我们需要将CAD文件中重要的数据提取成GIS系统所支持的格式，通过GIS强大的分析功能，得到我们需要的结果。

### DWG/DXF to Shp

CAD系统中，数据主要以*.dwg、*.dxf等二进制文件格式存储。通过计算机图形技术将文件中存储的二进制绘图命令绘制成图像，通过图层的形式表现出来（类似于Photoshop）。DWG是Autodesk公司发行的Autocad软件专用格式，而DXF格式为通用CAD图形格式。

较于CAD系统，GIS系统中的数据则是空间数据库，以关系数据形式存储着点、线、面等形状数据，着重体现数据的空间性。凭借GPS技术、互联网技术及数据库技术的发展，人们可以轻松的获取存储海量级别的空间地理数据。利用巨大的数据资源优势，GIS得到了长足的发展，并且衍生了多种分析技术：空间地理分析技术、空间行为分析技术等。目前，应用最广泛的GIS软件是ERSI公司研发的Arcgis套件，空间数据在其中主要以*.shp文件格式存储。

由于两种系统的组织数据方式的差异（也体现在存储文件格式差异上），CAD文件


### 



