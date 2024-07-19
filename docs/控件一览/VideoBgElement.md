# VideoBgElement

## 控件说明

此控件用于循环播放视频，采用了 ffpmeg 组件的界面能力，先确保程序的根目录下的 ffpmeg 下有相应的文件，，解决了 WPF 本身 VideoPlayer 的过度闪烁的问题，一般作为背景的动画使用
>[notice}
>确保主程序的配置文件启用了ffpmeg能力，在TronSensingShow.dll.config种修改
```xml
  <appSettings>
    <add key="ProjectFolder" value="Shell"/>
    <add key="IsUseWebView" value="True"/>
    <add key="IsUseFFmpeg" value ="True"/>
    <add key="FFmpegFolder" value="C:\\ffmpeg"/>
    <add key="ProductName" value="SensingPlatform Main"/>
    <add key="ProjectName" value="SensingPlatform Main"/>
    <add key="SensingSiteUrl" value="http://58.214.31.206:2015/api/"/>
  </appSettings>
```
## 控件 UI 效果

![Placeholder](../images/PerspectiveWallElement.gif)

## 控件的配置

此控件时包控件，需要在 UIControlDict.xml 中先进行注册

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

整个配置分为两个大类，一个是视频源的配置，一个是 VideoRender 的配置。

### 视频源的配置

1.  和 ImageElement 中的 ImageSource 一样，可以配置绝对路径，Application 路径或者相对控件的目录

# UIControlDict.xml 添加循环播放视频控件

如果使用循环播放视频控件则需要在 UIControlDict.xml 中添加循环播放视频控件

```
  <Element ViewType="VideoBgElement" AssemblyFile="UI.VideoBg.dll" TypeName="UI.VideoBg.VideoBgControl, UI.VideoBg, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.VideoBg.dll" TypeName="UI.VideoBg.VideoBgControlViewModel, UI.VideoBg, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```
