## SensingPlatform 简介

SensingPlatform是居于Windows平台的一套低代码平台，采用Xml作为配置文件，以Page(页面)作为最小呈现单元，集成了丰富的针对大屏的UI展示库，同时支持动态数据源(本地数据，数据库，HTTP接口数据等)作为UI的数据源，提供了无缝对接SensingStore云端接口。同时支持实时相应事件，对接了UDP，串口，SignalR接口，开箱即用。

整套框架居于组件模式进行开发，简单复用！
 
##  控件介绍

<table>
    <tr style="font-weight: bold">
        <td> 包名 </td>
        <td>控件</td>
        <td> 名称</td>
        <td>说明</td>
        <td> 是否是GroupView</td>
        <td>使用说明</td>
    </tr>
        <tr>
        <td rowspan="3">UI.Common</td>
        <td>ImageElement</td>
        <td>图片控件</td>
        <td>在页面或者弹出框中直接显示图片</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/ImageElement.md"> 详细说明</td>
    </tr>
   <tr>
        <td> ImageButton</td>
        <td> 图片按钮控件</td>
        <td>图片按钮，添加点击事件，跳转页面或弹出框。在页面或者弹出框中直接显示图片,并且点击后有某种效果</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/ImageButton.md"> 详细说明</td>
    </tr>
  <tr>
        <td> TextElement</td>
        <td> 文字控件</td>
        <td>在页面或者弹出框中直接显示文字</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/TextElement.md"> 详细说明</td>
    </tr>


</table>