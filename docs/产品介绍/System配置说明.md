# 项目配置结构的介绍

System.xml 文件在 Shell 的目录下，用于配置整个应用程序级别的；Pages.xml 位于 Shell/Pages 目录下，用于配置这个应用程序所用到的页面。

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
	<Event>ToDeviceDataEvent?Id=001&Protocol=UDP&Data=right</Event>
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
    <!-- 音频节点，用于配置应用中的背景音乐 -->
  <!-- 配置项说明：Name 别名，发送播放事件的时候用，IsDefault 是否为默认背景音乐，IsLoop 是否循环播放，UriKind 背景音乐的资源路径类型，值是文件路径
 -->
  <Audios>
    <Audio Name="A" IsDefault="false" IsLoop="true" UriKind="Application">AudioSource/音频1.mp3</Audio>
    <Audio Name="A" IsDefault="false" IsLoop="true" UriKind="Application">AudioSource/音频2.mp3</Audio>
  </Audios>
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

1.对 DEMO 所实用到所有页面要进行注册配置，目的是将 demo 中涉及到的所有页面注册到系统中

2.打开 Troncell 平台文件，找到 Shell 下 Pages 文件夹，在该文件夹下打开 Pages.xml 文件，使用编辑工具打开

```xml
<?xml version="1.0" encoding="utf-8"?>
<Pages>
  <!-- Name是你给页面所取的名字，Folder是Page的配置目录。
       1.Name是必须配置的，如果不配置或者为空的话，忽略当前页面配置。同时Name不应重复，是页面的唯一标识,如果重复只取最前的节点。
       2.Folder是可选的，为对应文件夹名称，当Folder不配置时，默认选用Name作为其默认值。如果Folder的路径不存在的话，当前Page会被忽略。
	     3.IsHome是可选的，当IsHome不配置时，默认值为False，如果所有的IsHome都没有配置的话，默认第一个页面节点为首页。
  -->
  <Page Name="StarPWallPage" Folder="StarPWallPage" />
  <Page Name="ScreenPage" Folder="ScreenPage" IsHome="True" />
</Pages>
```

3. Pages.xml 添加好后，需要对每个页面进行详细的配置

**例子：**

A.Pages.xml 里添加 page，如：

```
  <Page Name="TextPage" Folder="TextPage" />

```

B.打开 Troncell 平台文件，找到 Shell 下 Pages 文件夹，并在该文件夹下新建一个文件夹，名称为：TextPage

C.在新建的文件夹下新建和文件夹相同名称的 xml 文件 TextPage.xml

D.使用编辑器打开新建的 xml 文件，（这里是打开 TextPage.xml 文件），写入如下代码(一般情况下只需改动 `<SysPage Name=" TextPage">`)：

```

<!--SysPage中的Name值应与所在文件夹名字相同-->
<SysPage Name=" TextPage">
<!--<UIDisplay Left为距左边框距离 Top距上边框距离 Width宽度 Height高度 IsShow是否显
示值为True表示显示False表示不显示 ZIndex表示所在的层级，值为1表示层级最低在最底层
层 UsePercent是否根据页面的比例配置，如果值为True则是按照比例配置，若为False则不
是按照比例配置，是按照页面的实际像素大小/>-->
<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1"
UsePercent="False"/>
```
