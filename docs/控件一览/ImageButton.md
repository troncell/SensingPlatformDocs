# **图片按钮控件（** **ImageButton** **）**

## 控件作用

在页面或者弹出框中直接显示图片,并且点击后有某种效果。

## 控件 UI 效果

![Placeholder](../images/ImageButton_1.png)

## 配置文件样例

```xml
<!-- 跳页面-->
<ImageButton>
    <UIDisplay Left="100" Top="150" Width="180" Height="180" IsShow="True"  ZIndex="1" UsePercent="False"/>
    <ImageSource UriKind="Relative">NavIcons\lianliankan.png</ImageSource>
    <ClickEvent>Navigate?Page=HomePage&Args=imageButton</ClickEvent>
</ImageButton>
```

```xml
<!-- 跳弹出框-->
<ImageButton>
    <UIDisplay Left="100" Top="150" Width="180" Height="180" IsShow="True"  ZIndex="1" UsePercent="False"/>
    <!--ImageSource若不配，相当于透明按钮，程序不会出错，也不会出现加载动画 -->
    <ImageSource UriKind="Relative">NavIcons\lianliankan.png</ImageSource>
    <ClickEvent>PopupEvent?TargetPageName=BriefingPage&TargetControlName=PageLeftSecondShow&X=0&Y=0&Height=841&Width=1604&EventID=PageHotBigBookShow&UriKind=Application&EventPath=Shell\Pages\BriefingPage\Items\PopupItems\SecondSho&PageName={$PageName}</ClickEvent>
</ImageButton>
```

```xml
<!-- 关弹出框-->
<ImageButton>
    <UIDisplay Left="100" Top="150" Width="180" Height="180" IsShow="True"  ZIndex="1" UsePercent="False"/>
    <ImageSource UriKind="Relative">NavIcons\lianliankan.png</ImageSource>
    <ClickEvent>ChangePopupState?State=Close&Args=imageButton</ClickEvent>
</ImageButton>
```

```xml
<!-- 发出两个事件-->
<ImageButton Name="turnoff">
    <UIDisplay Left="1865" Top="985" Width="50" Height="50" IsShow="True"  ZIndex="10" UsePercent="False"/>
    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\turnoff.png</ImageSource>
    <ClickEvent>
        <Event IsLocal="True" SyncType="Client">Navigate?Page=GraphicPage</Event>
        <Event IsLocal="True" SyncType="Client">Navigate?Page=SweepPanelPage</Event>
    </ClickEvent>
</ImageButton>
```

```xml
<!-- 弹出点击 -->
<ImageButton>
    <UIDisplay Left="228" Top="1413" Width="622" Height="163" IsShow="True" ZIndex="2" UsePercent="False" />
    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\FFZQHD\HDSP\非法证券活动按钮1高亮.png</ImageSource>
    <ClickEvent>PopupEvent?TargetPageName=HomePage&TargetControlName=FFZQHDSPPop&X=0&Y=0&SP=A2.mp4&Height=1080&Width=1920&EventID=FFZQHDSPEvent1&UriKind=Application&EventPath=Shell\Pages\HomePage\PopItems</ClickEvent>
    <CustomerConfig>
        <Button AutoClick="True" />
    </CustomerConfig>
</ImageButton>
```

## 配置说明

### 节点 ClickEvent

    此节点是按钮点击后触发事件的核心，也是框架配置项的核心。事件配置和Http中Request类似，采用如下格式进行： Action?key1=value1&value2=value2

    在ClickEvent中根据不同的配置会做出不同的事件响应，以上配置文件样例中就是三种不同的响应效果；

#### 第一种，打开一个悬浮控件(弹出窗口)

PopupEvent：是响应方式(打开悬浮控件)，

TargetPageName：在指定页面使用悬浮控件

&amp;是&的转义字符：表示与、和、连接的意思

TagetControlName：为所需使用悬浮控件的名称，弹出窗口的名称

X：为距左边框距离； Y：距上边框距离 ；Width：宽度； Height：高度,

EventId ：为所要使用到的悬浮控件的模板，如果是对应表格里得字段 EventID={$Photo}，photo 下得每一个在 PopItems 文件加下都对应一个文件夹和 xml

UriKind ：为配置路径的类型

Relative ：是相对于当前 xml 的位置

Application ：是相对于整个 demo 的位置。Absolute 是真实的物理路径，如 c:\Images\，EventPath 为模板所在的路径位置，此处还可以向控件传递参数，如示例中的 PageName(多个之间&amp;连接)，以上为指定固定位置出现悬浮控件，若想使得所需弹出的悬浮控件在随着点击位置改变而改变则需加入 LocationKind=Relative 即可；

#### 第二种，实现点击进行按钮页面间跳转的效果配置

Navigate 为响应方式（页面跳转）

HomePage 就是所跳到的目标页面；

#### 第三种，关闭悬浮控件(弹出窗口)

ChangePopupState 是响应方式(改变悬浮控件的状态)

State=Close 状态为关闭。

#### 第四种：其它

整个框架内的 Events 都可以由 ClickEvent 发出，同时在 EventFirers.xml 的用户自定义事件也可以

### 节点 Event

    此节点为2.0版本特有的属性，主要实现一个按钮点击之后实现两种效果，如上面配置文本样例中，同时跳转两个页面，或者也可以实现跳出两个弹出框，又或者是关闭自身的弹出框，同时弹出新弹出框。

    属性说明（以下属性主要针对两台机器通信时的状态）

    IsLocal：本地是否也实现这个事件；

    SyncType：该机器是server端还是Client端，与system中的设置匹配。

### 节点 CustomerConfig

    AutoClick：跳转页面默认选中点击。

# UIControlDict.xml 添加图片按钮控件

如果使用图片按钮控件则需要在 UIControlDict.xml 中添加图片按钮控件

```

<Element ViewType="ImageButton" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.ImageButtonControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.EventButtonViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```
