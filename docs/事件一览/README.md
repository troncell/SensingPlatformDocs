## SensingPlatform 平台中的事件说明

事件配置和 Http 中 Url Request 类似，采用如下格式进行：
`Action?key1=value1&amp;key2=value2`

> [!NOTE]
> Action 为事件的名称，后面的 Query 为事件所需要的参数。在 XML 中，`&` 必须转义为 `&amp;`。各个事件所需的参数都不一样，理解事件的过程就是理解参数逻辑的过程。

系统默认的全局 Key 如下:

**1. EDelay=1000 : 表示配置的事件会延时 1000ms(毫秒)=1 秒，触发该事件**

**2. TargetControl=flipViewList : 表示配置的事件会触发给特定的 UI 控件，同时该组件有能力处理此事件，详细说明查看控件的具体配置**

**3. UriKind=Project : 表示配置的事件，会用到文件或者路径之类的参数，用于定于获取文件的路径方式，Relative(相对当前控件的目录，如有 Name 的话，会有对应的文件夹),Application(程序的启动目录),Project(具体工程目录，默认为 Shell 的文件夹下**

**4. ImageSource=trocell_logo.png : 表示配置的事件会用到图片，通常和 UriKind 参数一起使用，用于改变图片的显示，具体业务要去对应的控件上参考具体的配置功能，ImageElement 就支持**

**5. PathSource=troncell : 表示配置的事件会用到文件夹下的资源，通常和 UriKind 参数一起使用，用于改变资源的显示，具体业务要去对应的控件上参考具体的配置功能，FrameElement 就支持**

**6. Loop=2 : 表示该事件会循环调用一定次数，如果想要一直循环下去，就使用Loop=-1，如果想要停止这个循环，那就在任意事件后面加上StopLoop=True**

**7. Async=true : 表示该事件是异步发送的，一般是发送一些事件给后台的模块；false则是发给UI线程，是发给UI控件的，不配置默认是false**

> [!WARNING]
> 这些全局的 Key 不要在特定事件中用同样的 Key 名称

## 平台事件可以在 ImageButton 下的 ClickEvent 下配置

### Navigate (导航事件)

Navigate:点击图片，可以跳转到指定页面,此节点是按钮点击后触发事件的核心，也是框架配置项的核心。

在 ClickEvent 中根据不同的配置会做出不同的事件响应，以下配置文件样例中就是不同的响应效果；

**样例：**

```xml
<!-- 点图片跳页面-->
 <ImageButton>
                <UIDisplay Left="1291" Top="595" Width="441" Height="261" IsShow="True" ZIndex="1" UsePercent="False" />
                <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\知识产权.png</ImageSource>
                <ClickEvent>Navigate?Page=StarPWallPageA&TrackingData=知识产权</ClickEvent>
              </ImageButton>
```

**说明**

Navigate 为响应方式（页面跳转）

Page=StarPWallPageA 就是所跳到的目标页面；

TrackingData：追踪数据，用于行为统计。

### PopupEvent（弹出框）

```xml
<ImageButton>
			<UIDisplay Left="2000" Top="400" Width="180" Height="180" IsShow="True" ZIndex="1" UsePercent="False"/>
			<ImageSource UriKind="Application">Shell\Pages\dianzishu\resource\科创板按钮.png</ImageSource>
			<ClickEvent>PopupEvent?TargetPageName=dianzishu&TargetControlName=PopupShow&X=0&Y=0&Height=1080&Width=1920&EventID=EBookEvent9&UriKind=Application&EventPath=Shell\Pages\dianzishu\PopItems</ClickEvent>
		</ImageButton>

```

**说明**

PopupEvent：是响应方式(打开悬浮控件)，

TargetPageName：在指定页面使用悬浮控件

&amp;是&的转义字符：表示与、和、连接的意思

TagetControlName：为所需使用悬浮控件的名称，弹出窗口的名称

X：为距左边框距离； Y：距上边框距离 ；Width：宽度； Height：高度,

EventId ：为所要使用到的悬浮控件的模板，如果是对应表格里得字段 `EventID={$Photo}`，`Photo` 下得每一个在 PopItems 文件加下都对应一个文件夹和 xml

UriKind ：为配置路径的类型。`Relative` ：是相对于当前 xml 的位置；`Application`：是相对于整个 demo 的位置；`Absolute`是真实的物理路径，如`c:\Images\`。

EventPath ：为弹出框模板所在的路径位置，此处还可以向控件传递参数，如示例中的 PageName(多个之间&amp;连接)，以上为指定固定位置出现悬浮控件，若想使得所需弹出的悬浮控件在随着点击位置改变而改变则需加入 `LocationKind=Relative` 即可；

IsAllowMove：弹出框允许移动

IsAllowRotate：弹出框允许旋转

### ClosePopup（关闭指定弹框）

**样例：**

```xml
  <ImageButton>
      <UIDisplay Left="0" Top="130" Width="373" Height="111" IsShow="True" ZIndex="4" UsePercent="False" />
      <ImageSource UriKind="Application">Shell\Pages\daoshiPage\img\Search.png</ImageSource>
      <ClickEvent>
        <Event>ClosePopup?TargetPageName=HomePage&TargetControlName=StorePop&EffectName=ScaleClose&EventID=Store&UriKind=Application&EventPath=Shell\Pages\HomePage\CategoryPopItems&Filter=[LargeClassId={$Id}]</Event>
        <Event>PopupEvent?TargetPageName=HomePage&TargetControlName=CategoryPop&EffectName=ScaleClose&EventID=SeachStore&UriKind=Application&EventPath=Shell\Pages\HomePage\CategoryPopItems&C={$Id}</Event>
      </ClickEvent>
    </ImageButton>
```

**说明：**

ClosePopup:是响应方式（可以关闭目标页的弹窗）

TargetPageName：目标页面

TargetControlName：目标 PopupShowElement ， 如果TargetControlName=ALL，那么就可以关闭对应页面所有的PopupShow

EventID：为所要使用到的悬浮控件的模板,对应要关闭的弹窗 ID

me：关闭动画效果名称。

### ChangePopupState（修改 PopupShow 状态）

```xml

 <ImageButton>
        <UIDisplay Left="1765" Top="1000" Width="155" Height="80" IsShow="True" ZIndex="5" UsePercent="False" />
        <ImageSource UriKind="Application">Shell\Pages\CirclePage\resource\gohome.png</ImageSource>
        <ClickEvent>ChangePopupState?State=Close&Args=imageButton</ClickEvent>
      </ImageButton>
```

**说明**

ChangePopupState 是响应方式(改变悬浮控件的状态)

State=Close 关闭弹窗

State=Pin 固定弹窗，不可移动

State=Unpin 弹窗取消固定，可以移动

Args：附加参数，通常无需配置。

### Control（控制事件，一般用户控制动画，视频，PPT等播放和翻页之类的,还有通过事件触发一个按钮的事件,可以控制PopupShow的显示和隐藏）

```xml
<ImageButton Name="left">
	<UIDisplay Left="77" Top="470" Width="27" Height="51" IsShow="True" ZIndex="4" UsePercent="False" />
	<ImageSource UriKind="Application">Shell\Pages\qiyePage\resource\箭头2.png</ImageSource>
	<!--
	Control是个通用的事件，很多组件都可以处理此类事件，如动画帧组件，视频组件等
	Action: 控制的具体操作，如播放(Play),停止(Stop), 暂停(Pause),往前(Prev),往后（Next),特定位置(Index),Click(触发ImageButton的Click事件),Check(ToggleButton的Check、UnCheck事件)等。
	-->
	<ClickEvent>
  <Event>Control?Action=Play&Index=0&IndexString=Pre&TargetControlName=imageButton</Event>
  <!-- 触发按钮的事件，主要用于SignalR发送事件 -->
  <<Event>Control?TargetPageName=HomePage&amp;TargetControlName=Fenli&amp;Action=Click</Event>
  <!-- 触发对应togglebutton的check事件并且按钮会触发相关动画，也可以UnCheck -->
  <Event>Control?TargetPageName=SlidingScreen&amp;TargetGroup=A&amp;TargetControlName=2006&amp;Action=Check</Event>
  </ClickEvent>
</ImageButton>
```

**说明**

Control 是个通用事件，很多组件都可以处理，如动画帧组件、视频组件等。

Action：控制的具体操作。

- `Play`：播放。
- `Stop`：停止。
- `Pause`：暂停。
- `Prev`：往前。
- `Next`：往后。
- `Index`：跳转到特定位置。
- `Click`：触发 ImageButton 的 Click 事件。
- `Check` / `UnCheck`：触发 ToggleButton 的选中/取消选中事件。

TargetPageName：目标页面。

TargetControlName：目标控件名称。

TargetGroup：目标分组（部分控件如 SlidingScreen 使用）。

### IndexChanged(通过事件，使scrollviewer滚动到指定位置，或者让filpview翻页)

位置变化事件，如切上一张，下一张图片或者特定位置的图片

```xml
filpview 翻页
<ClickEvent>IndexChanged?TargetControlName=FlipView3&amp;Index=0&amp;IndexString=Pre&amp;Args=imageButton</ClickEvent>

<!-- 到第五个点位 -->
<!-- Move ：ToIndex：跳转到指定索引位置, Pre 前一个点位，Next：下一个点位 -->
 <Event>IndexChanged?TargetPageName=SlidingScreen&amp;TargetControlName=Items&amp;Move=ToIndex&amp;Index=5&amp;ToInput=false</Event>
```

**说明**

IndexChanged：响应方式（跳转对应索引图片）

TargetPageName：：目标页面

TargetControlName：目标控件名称 PopupShowElement

Index：跳转到具体某一页面

Next：下一张图片

Pre：前一张图片

### SourceChanged(展示源变化事件 用于改变图片，视频，帧动画文件夹，页面地址等的切换)

```xml
  <ImageButton Name="left">
	<UIDisplay Left="77" Top="470" Width="27" Height="51" IsShow="True" ZIndex="4" UsePercent="False" />
	<ImageSource UriKind="Application">Shell\Pages\qiyePage\resource\箭头2.png</ImageSource>
	<!--
	SourceChanged:是个通用的事件，很多组件都可以处理此类事件，如ImageElement,ImageButtonElement等
	UriKind: 找图片的途径参数，如Project，Application等。
	ImageSource: 新图片资源的地址，用于改变图片的控件
	VideoSource: 新视频资源的地址，用于改变视频的控件
	PathSource: 新文件夹的地址，用于需要文件夹的控件
	-->
	<ClickEvent>SourceChanged?UriKind=Project&TargetControlName=imageButton&ImageSource=Page\HomePage\CheckBg.png</ClickEvent>
</ImageButton>
```

**说明**

ChangeWebViewSource:响应方式（修改改变图片、视频、文件夹等展示源）

TargetPageName：目标页面

TargetControlName：目标控件名称 PopupShowElement

SourcePath：web资源路径

ImageSource：新的图片资源地址。

VideoSource：新的视频资源地址。

PathSource：新的文件夹资源地址。

### Transition(用户控制控件的动画，目前仅支持Translate位移动画的控制，若项目需要联系开发)

```xml
  <ImageButton Name="left">
	<UIDisplay Left="77" Top="470" Width="27" Height="51" IsShow="True" ZIndex="4" UsePercent="False" />
	<ImageSource UriKind="Application">Shell\Pages\qiyePage\resource\箭头2.png</ImageSource>
	<!--
	Transition:是个通用的事件，所有的框架提供的组件都支持，自己居于wpf写的组件不支持
	TransitionName: 对应组件的具体的Transition的名字，用于控制特定的动画。
	Action: 播放动画，目前仅支持播放与停止，Play/Stop
	Reverse: 动画中的开始位置和结束位置是否调换，这样的话，一个transiton就能事件实现往复运动
	-->
	<Event>Transition?TargetControlName=animation&amp;TransitionName=move&amp;Action=Play&amp;Reverse=True</Event>
</ImageButton>
```

**说明**

Transition：用于控制控件的位移动画（Translate）。

TransitionName：对应组件中具体 Transition 的名称，用于控制特定动画。

Action：动画操作，目前支持 `Play` / `Stop`。

Reverse：是否调换动画的开始位置和结束位置，这样可以实现往复运动。

TargetControlName：目标控件名称。

### ChangeWebViewSource(修改 webbview打开的html页面地址)

```xml
  <CameraData Name="CameraLocalData">
    <AutoFreshData Enable="False" IntervalTime="00:00:20"></AutoFreshData>
    <CustomerConfig>
      <Tables>
        <Table Name="Counters" IsRealtimeLoad="True">
          <DataQuery Value="select sum(increment) TotalCount,MonthCount,TodayCount from CounterEntity"></DataQuery>
        </Table>
      </Tables>
      <Game>
        <Port>5678</Port>
        <Debug>false</Debug>
        <ExitPhotoTime>30</ExitPhotoTime>
        <!--显示最近的签名天数-->
        <SignatureDay>360</SignatureDay>
        <!--每块屏的区间位置 cm -->
        <SecurityKey>8d76984284fd4107b09472bea921d067</SecurityKey>
        <!--Camera列表-->
        <Cameras>
          <Camera Ip="192.168.3.23" Port="2555"/>
        </Cameras>
        <Counters>
          <Counter>Counter 0</Counter>
        </Counters>
        <!--本地服务器    -->
        <LocalServer>http://localhost:5000</LocalServer>
        <settingPath>setting/GameSetting.xml</settingPath>
        <Start>Navigate?Page=StarPWallPage&IgnoreInput=False&TrackingData=合伙人介绍页面</Start>
        <Signature>ChangeWebViewSource?TargetPageName=StarPWallPage&TargetControlName=popChrome&SourcePath=\Shell\Pages\StarPWallPage\popChrome\wall\index.html?name={$FilePath}</Signature>
      </Game>
    </CustomerConfig>
  </CameraData>
```

**说明**

ChangeWebViewSource:响应方式（修改 WebView 打开的 HTML 页面地址）

TargetPageName：目标页面

TargetControlName：目标 PopupShowElement

SourcePath：web资源路径

### IndexChanged（位置变化事件，如切上一张，下一张图片或者特定位置的图片）

```xml
<ImageButton Name="left">
        <UIDisplay Left="77" Top="470" Width="27" Height="51" IsShow="True" ZIndex="4" UsePercent="False" />
        <ImageSource UriKind="Application">Shell\Pages\qiyePage\resource\箭头2.png</ImageSource>
        <ClickEvent>IndexChanged?TargetControlName=FlipView&Index=0&IndexString=Pre&Args=imageButton</ClickEvent>
      </ImageButton>
      <ImageButton Name="right">
        <UIDisplay Left="1818" Top="470" Width="27" Height="51" IsShow="True" ZIndex="4" UsePercent="False" />
        <ImageSource UriKind="Application">Shell\Pages\qiyePage\resource\箭头1.png</ImageSource>
        <ClickEvent>IndexChanged?TargetControlName=FlipView&Index=0&IndexString=Next&Args=imageButton</ClickEvent>
      </ImageButton
```

**说明**

IndexChanged：响应方式（跳转对应索引图片）

TargetPageName：：目标页面

TargetControlName：目标 PopupShowElement

Index：跳转到具体某一页面

Next：下一张图片

Pre：前一张图片

### ToDeviceDataEvent (发送数据到设备)

```xml
<Event>ToDeviceDataEvent?Id=001&amp;Protocol=UDP&amp;Data=right&amp;IsHex=False</Event>
```

说明
Id : 设备ID或者命令的ID
Protocol : 协议类型 UDP/TCP/SerialPort/SignalR
Data : 发送的数据内容
IsHex : 是否是16进制格式发送
SubKey : 目标设备的Subkey（部分协议需要）

### Shutdown (重启或关机)

```xml
 <Event>Shutdown?Type=Computer</Event>
```

**说明**
Type ：动作类型

- `Application`：关闭当前应用。
- `Computer`：关闭计算机。
- `Reboot`：重启计算机。

### WebViewDoRefresh（刷新浏览器页面）

```xml
<ClickEvent>WebViewDoRefresh?TargetPageName=HomePage&amp;TargetControlName=WebBrowser</ClickEvent>
```

**说明**

WebViewDoRefresh：刷新目标浏览器控件当前页面。

TargetPageName：目标页面。

TargetControlName：目标 WebBrowserElement 名称。

### WebViewCallToJS（向浏览器页面发送 JS 消息）

```xml
<ClickEvent>WebViewCallToJS?TargetPageName=HomePage&amp;TargetControlName=WebBrowser&amp;DoAction=showAlert&amp;JsonData=hello</ClickEvent>
```

**说明**

WebViewCallToJS：向目标浏览器控件中的 JavaScript 发送消息。

TargetPageName：目标页面。

TargetControlName：目标 WebBrowserElement 名称。

DoAction：JS 回调动作名称。

JsonData：传递给 JS 的数据。

### ChangeVideoSource（修改视频源）

```xml
<ClickEvent>ChangeVideoSource?TargetPageName=HomePage&amp;TargetControlName=VideoPlayer&amp;SourcePath=Shell\Videos\demo.mp4</ClickEvent>
```

**说明**

ChangeVideoSource：切换视频控件的播放源。

TargetPageName：目标页面。

TargetControlName：目标视频控件名称。

SourcePath：新的视频资源路径。

### ChangeInkCanvas（修改画板属性）

```xml
<ClickEvent>ChangeInkCanvas?TargetPageName=HomePage&amp;TargetControlName=PaintingBoard&amp;StrokeColor=Red</ClickEvent>
```

**说明**

ChangeInkCanvas：修改画板控件的画笔颜色等属性。

TargetPageName：目标页面。

TargetControlName：目标画板控件名称。

StrokeColor：画笔颜色。

### Rotate（旋转控件）

```xml
<ClickEvent>Rotate?TargetPageName=HomePage&amp;TargetControlName=RotateImage&amp;Target=90</ClickEvent>
```

**说明**

Rotate：控制旋转控件旋转到指定角度。

TargetPageName：目标页面。

TargetControlName：目标旋转控件名称。

Target：目标角度。

### LoadData（重新加载数据源）

```xml
<ClickEvent>LoadData?TargetDataSource=CameraLocalData&amp;Parameters=Param1=Value1</ClickEvent>
```

**说明**

LoadData：重新加载指定的数据源。

TargetDataSource：目标数据源名称。

Parameters：传递给数据源的参数。

### StartProcess（启动外部进程）

```xml
<ClickEvent>StartProcess?Path=C:\Windows\notepad.exe&amp;Name=notepad</ClickEvent>
```

**说明**

StartProcess：启动外部程序。

Path：可执行文件路径。

Name：进程名称。

### SpeakEvent（语音播报）

```xml
<ClickEvent>SpeakEvent?TargetPageName=HomePage&amp;TargetControlName=Speaker&amp;StartText=开始播报&amp;EndText=播报结束</ClickEvent>
```

**说明**

SpeakEvent：触发语音播报。

TargetPageName：目标页面。

TargetControlName：目标语音控件名称。

StartText：播报开始文本。

EndText：播报结束文本。
