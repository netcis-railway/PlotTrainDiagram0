# 十分格列车运行图绘制和相关代码

<p align="center">
    <img width="110" height="110" alt="logoNew_small" src="https://github.com/user-attachments/assets/82bdd376-cead-42fc-b33c-dfcb58b2e92c" />
</p>    
<p align="center">
    <a href="https://www.mathworks.com/products/matlab.html">
        <img src="https://img.shields.io/badge/MATLAB-R2020b+-orange.svg?logo=mathworks&logoColor=white" alt="MATLAB" />
    </a>
    <a href="https://www.python.org/">
        <img src="https://img.shields.io/badge/Python-3.8+-blue.svg" alt="Python" />
    </a>
    <a href="Private">
        <img src="https://img.shields.io/badge/License-Proprietary-lightgrey.svg" alt="License" />
    </a>
</p>

## 仓库链接:

HTTPS链接：[https://github.com/netcis-railway/PlotTrainDiagram.git](https://github.com/netcis-railway/PlotTrainDiagram.git)

SSH链接：[git@github.com:netcis-railway/PlotTrainDiagram.git](git@github.com:netcis-railway/PlotTrainDiagram.git)



参考《列车运行图编制管理规则》（中国铁道出版社 2008年）、《铁路线路设计规范》、《铁路技术管理规程》等行业管理性文件、技术标准与管理办法， 绘制十分格列车运行图的作图代码。

[![京沪高铁运行图示例](figures/京沪高铁运行图示例.png)

横轴为一天内的时刻（秒），纵轴为沿线路排列的车站；下行列车以红色表示，上行列车以蓝色表示。

## 代码功能描述
读取V3f版Excel列车时刻表数据，绘制十分格列车运行图。
核心程序是DrawTrainDigramFunctionV3f.m，用于读取车站及列车到发时刻、线路信息和Seq顺序信息，识别列车运行方向，计算各相邻车站间的等效间距，并绘制指定线路的运行图背景、列车运行线及车次标注。绘图入口通过本文件返回的函数句柄调用。


### 典型调用流程：
读取时刻表 -> 确定时间范围及列车方向 -> 计算站间距 -> 绘制背景坐标 -> 绘制线路运行线 -> 标注车次。详细参数及返回值见各子程序注释。

### 核心子程序：
- DrawTrainDigramFunctionV3f  创建函数接口并注册可调用的子程序。

-  ReadTrainSchedule           读取V3f格式Excel时刻表，返回原始数据及列车、车站数量。

-   GetTrainTimeSegment         根据有效到发时刻确定运行图的起止小时。

-   JudgeUpOrDown               根据相邻车站的时刻先后判断各列车的运行方向。

-   GetStationInterval          统计各相邻车站区间的最小运行时间，供纵轴间距计算使用。

-   DrawBackground              按线路筛选车站，生成车站坐标并绘制运行图网格和坐标轴。

-   DrawDigram                  按时刻绘制全部列车运行线。

-   DrawLineDigram              按指定线路绘制运行线；有Seq时按其排序，否则按时刻排序，并生成图例。

-   MarkTrainNumber             在指定线路的列车起点附近标注车次。

-   parseTime                   将数值或文本格式的时刻转换为秒。

-   IsStationOnLine             判断车站的线路信息是否包含指定线路号。


## 改进计划

@龙麟 计划调整图vs基本图代码（蓝色基本图，红色调度调整计划图）， 保持原有基于v3f版的基础作图程序，补充到DrawTrainDigramFunctionV3f版目录下，也放到这个子目录下，新建一个代码文件(比如 plotTTScheduledvsBase.m)

@王骞 v4版的作图程序，新建目录 DrawTrainDiagramV4
