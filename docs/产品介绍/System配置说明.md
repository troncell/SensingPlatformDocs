# 项目配置结构的介绍

System.xml文件在Shell的目录下，用于配置整个应用程序级别的；Pages.xml位于Shell/Pages目录下，用于配置这个应用程序所用到的页面。

## System.xml 参考示例

```xml
<?xml version="1.0" encoding="utf-8"?>
<System>
  <!--Resolution节点用于配置整个Demo的默认显示大小,所有页面配置的大小按照此大小进行配置，而最终呈现的大小由DisplayBound节点来配置，缩放比例将根据Resolution和DisplayBound的比例来确定-->
  <Resolution Width="1920" Height="1080" />
  <!-- 窗体的显示范围，包括起始位置和大小-->
  <DisplayBound Left="0" Top="0" Width="1920" Height="1080" />
  <!--CultureInfo用于配置Demo的语言设置-->
  <CultureInfo Value="zh-CN" />
  <!--设置是否为DebugMode，False表示不是Debug模式，True表示为是Debug模式，在Debug模式下，支持鼠标操作-->
  <DebugMode Value="True" />
  <!--设置屏保时间以及屏保页面,时间的格式为 hh:mm:ss，屏保页面要在Page.xml中真实存在, ToPage用于配置有人在屏保模式下，有人互动进入的页面，如果ToPage没配，进入最后一个进入屏保的页面，如果配置了，直接进入固定的页面-->
  <ScreenSaver WaitingTime="00:00:20" SaverPage="ScreenPage" ToPage="WelcomePage">
	<!--进入屏保执行的事件，可配置任意的事件和ImageButton的Click类似-->
	<Event>ToDeviceDataEvent?Id=001&amp;Protocol=UDP&amp;Data=right</Event>
  </ScreenSaver>
  <Shell>
    <!--MainRegion目前只能配置一个，以后可能会扩展-->
    <MainRegion>
      <!--<UIDisplay Left="0" Top="0.666" Width="0.5" Height="0.333" IsShow="True"  ZIndex="1" UsePercent="True"/>-->
      <UIDisplay Left="0" Top="0" Width="1" Height="1" IsShow="True" ZIndex="1" UsePercent="True" />
    </MainRegion>
    <!--CopyRegion暂时也只能配置一个-->
    <!--<CopyRegion>
    <UIDisplay Left="0" Top="0" Width="1" Height="0.666" IsShow="True"  ZIndex="1" UsePercent="True"/>
  </CopyRegion>-->
  </Shell>
  <!--InputDevice节点用于配置用户以何种方式操控CobonSensing应用
     1.目前可配置的参数为Mouse,Touch,NUI。默认方式为Touch
     2.如需要同时支持多种操作方式的话，配置项各单项的组合。例如：“Mouse|Touch|NUI”
  -->
  <InputDevice Value="Mouse, Touch"></InputDevice>
</System>
```

### 参数说明

参数说明，请参照示例示例中的注释说明

## Pages.xml 示例

```xml
<?xml version="1.0" encoding="utf-8"?>
<Pages>
  <!-- Name是你给页面所取的名字，Folder是Page的配置目录。
       1.Name是必须配置的，如果不配置或者为空的话，忽略当前页面配置。同时Name不应重复，是页面的唯一标识,如果重复只取最前的节点。
       2.Folder是可选的，当Folder不配置时，默认选用Name作为其默认值。如果Folder的路径不存在的话，当前Page会被忽略。
	     3.IsHome是可选的，当IsHome不配置时，默认值为False，如果所有的IsHome都没有配置的话，默认第一个页面节点为首页。
  -->
  <Page Name="StarPWallPage" Folder="StarPWallPage" />
  <Page Name="ScreenPage" Folder="ScreenPage" IsHome="True" />
</Pages>
```

