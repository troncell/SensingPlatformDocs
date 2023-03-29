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
    <td rowspan="11">UI.Common</td>
        <td> CustomerElement</td>
        <td> 自定义控件</td>
        <td>利用工具制作动画或功能进行引用</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/CustomerElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>ImageElement</td>
        <td>图片控件</td>
        <td>在页面或者弹出框中添加图片显示</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/ImageElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td> ImageButton</td>
        <td> 图片按钮控件</td>
        <td>图片按钮，添加点击事件，跳转页面或弹出框</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/ImageButton.md"> 详细说明</td>
    </tr>
     <tr>
        <td> ScrollViewerElement</td>
        <td> 滚动条控件</td>
        <td>无法一页显示的图片或文字增加滚动条向下滚动观看</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/ScrollViewerElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td> TextElement</td>
        <td> 文字控件</td>
        <td>在页面或者弹出框中添加文字显示</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/TextElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td> VideoPlayerElement</td>
        <td> 视频控件</td>
        <td>在页面或者弹出框中播放视频</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/VideoPlayerElement.md"> 详细说明</td>
    </tr> 
    <tr>
        <td>XYContainerElement</td>
        <td> 相对布局控件</td>
        <td>将多个基本控件组合成一个基本的控件</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/XYContainerElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>XamlElement</td>
        <td> 包动画控件</td>
        <td>使用工具Blend for Visual Studio 或者Visual Studio 制作一些背景动画，用动画来展示页面</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/XamlElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>ToggleButton</td>
        <td>支持两种状态的图片按钮控件</td>
        <td>支持两种状态的图片按钮控件</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/ToggleButton.md"> 详细说明</td>
    </tr>
    <tr>
        <td>RotateControlElement</td>
        <td>图片旋转控件</td>
        <td>拖动图片旋转</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/RotateControlElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>LongPressButton</td>
        <td>长按按钮控件</td>
        <td>长按按钮执行事件</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/LongPressButton.md"> 详细说明</td>
    </tr>
    <tr>
        <td>UI.AlbumLibrary</td>
        <td>AlbumElement</td>
        <td>飞图控件</td>
        <td>在页面中自动浮动，展示一系列图片或视频</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/AlbumElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>UI.BubbleElement</td>
        <td> BubbleElement</td>
        <td> 气泡控件</td>
        <td>动态生成气泡</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/BubbleElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>UI.SweepPanel.dll</td>
        <td> CircleElement</td>
        <td> 环形卡片控件</td>
        <td>以360度环绕滑块的方式展示图片</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/CircleElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td></td>
        <td> DanceingBubbleElement</td>
        <td> 跳动图片控件</td>
        <td>可以使图片跳动，以跳动的方式来突出图片或按钮</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/DanceingBubbleElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>UI.EBook.dll</td>
        <td> EBookElement</td>
        <td> 电子书控件</td>
        <td>电子书控件以翻书的交互方式展示一系列图片。</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/BookElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>UI.FishEyes</td>
        <td> FishEyeElement</td>
        <td> 鱼眼控件</td>
        <td>可自定义鱼眼个数，根据操作让图片变大缩小，主要用于展示图片集合</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/FishEyeElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>UI.FlipView</td>
        <td> FlipViewElement</td>
        <td> 卡片型滑块控件</td>
        <td>卡片型滑块控件以翻日历的交互方式展示一系列图片</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/FlipViewElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td></td>
        <td> InteractiveWall3DElement</td>
        <td> 3D互动墙控件</td>
        <td>以3D的效果来展示图片</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/InteractiveWall3DElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>UI.FlipView</td>
        <td> PagerElement</td>
        <td> 长图文滑块控件</td>
        <td>可以上下滑动长图文</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/PagerElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td></td>
        <td> PerspectiveWallElement</td>
        <td>幻影墙控件</td>
        <td>使图片看起来有层次感，使人身临其境的感觉</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/PerspectiveWallElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>UI.SweepPanel.dll</td>
        <td> PopupShowElement</td>
        <td> 弹出框控件</td>
        <td>弹出框控件主要用于更加详细地介绍页面中的内容。</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/PopupShowElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td>UI.SweepPanel</td>
        <td> SequenceItemsElement</td>
        <td> 滑块控件/时间轴控件</td>
        <td>在页面中滑动图片，支持水平滑动和垂直滑动</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/SequenceItemsElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td></td>
        <td> Square3DElement</td>
        <td> 正方体控件</td>
        <td>以3D的效果展示图片，排列成正方体的样式</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/Square3DElement.md"> 详细说明</td>
    </tr>
  <tr>
        <td></td>
        <td> VideoBannerElement</td>
        <td> 视频滑块控件</td>
        <td>多个视频可以左右滑动</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/VideoBannerElement.md"> 详细说明</td>
    </tr>
<tr>
        <td>UI.VideoBg</td>
        <td> VideoBgElement</td>
        <td> 循环播放视频控件</td>
        <td>背景可以循环播放视频</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/VideoBgElement.md"> 详细说明</td>
    </tr>  
    <tr>
        <td></td>
        <td> Wall3DElement</td>
        <td> 3D凹面墙控件</td>
        <td>以3D凹陷的效果展示图片</td>
        <td>是</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/Wall3DElement.md"> 详细说明</td>
    </tr> 
    <tr>
        <td></td>
        <td> WeatherElement</td>
        <td> 天气控件</td>
        <td>自动显示中国天气网中当时的天气</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/WeatherElement.md"> 详细说明</td>
    </tr> 
 <tr>
        <td>UI.SensingWebBrowser</td>
        <td> WebBrowserElement</td>
        <td> 浏览器控件</td>
        <td>用于嵌入浏览器以提供一些网络信息</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/WebBrowserElement.md"> 详细说明</td>
    </tr>
     <tr>
        <td> UI.Qrcode.dll</td>
        <td>QrcodeElement</td>
        <td>二维码控件</td>
        <td>在页面中展示二维码</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/QrCodeElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td></td>
        <td>PaintElement</td>
        <td>画图控件</td>
        <td>在页面中画图</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/AlbumElement.md"> 详细说明</td>
    </tr>
      <tr>
        <td></td>
        <td>ShadowControl</td>
        <td>阴影控件</td>
        <td>在页面中的文字，图片等显示阴影</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/AlbumElement.md"> 详细说明</td>
    </tr>
    <tr>
        <td></td>
        <td>SliderBar</td>
        <td>滑动杆控件</td>
        <td>选择范围区间，可以是多个</td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/AlbumElement.md"> 详细说明</td>
    </tr>
        <tr>
        <td></td>
        <td>PrinterPanelElement</td>
        <td></td>
        <td></td>
        <td>否</td>
        <td> <a href="https://github.com/troncell/SensingPlatformDocs/blob/master/docs/%E6%8E%A7%E4%BB%B6%E4%B8%80%E8%A7%88/AlbumElement.md"> 详细说明</td>
    </tr>




</table>