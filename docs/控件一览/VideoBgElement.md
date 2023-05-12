# VideoBgElement

## 控件说明
此控件用于循环播放视频，采用了ffpmeg组件的界面能力，先确保程序的根目录下的ffpmeg下有相应的文件，解决了WPF本身VideoPlayer的过度闪烁的问题，一般作为背景的动画使用


## 控件UI效果
![Placeholder](../images/PerspectiveWallElement.gif)


## 控件的配置

此控件时包控件，需要在UIControlDict.xml中先进行注册
```xml
<Element ViewType="VideoBgElement" AssemblyFile="UI.VideoBg.dll" TypeName="UI.VideoBg.VideoBgControl, UI.VideoBg, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.VideoBg.dll" TypeName="UI.VideoBg.VideoBgControlViewModel, UI.VideoBg, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```
页面的配置范例如下

```xml
<VideoBgElement Name="bgVideo">
    <UIDisplay Left="900" Top="0" Width="960" Height="540" IsShow="True" ZIndex="1" UsePercent="False" />
    <VideoSource UriKind="Application">Shell\Pages\HomePage\Resources\report-bg.mp4</VideoSource>
</VideoBgElement>
```

## 配置讲解

整个配置分为两个大类，一个是视频源的配置，一个是VideoRender的配置。
### 视频源的配置
1.  和ImageElement中的ImageSource一样，可以配置绝对路径，Application路径或者相对控件的目录
