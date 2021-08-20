# **图片按钮控件（**  **ImageButton** **）**

## 控件作用

在页面或者弹出框中直**接显示**图片,并且点击后有某种效果。

## 控件UI效果

![Placeholder](../../images/ImageButton_1.png)

## 配置文件样例

```
<ImageButton>

<UIDisplay Left="100" Top="150" Width="180" Height="180" IsShow="True"  ZIndex="1" UsePercent="False"/>

<ImageSource UriKind="Relative">NavIcons\lianliankan.png</ImageSource>

<ClickEvent>Navigate?Page=HomePage&Args=imageButton</ClickEvent>

</ImageButton>

l  <ImageButton>

<UIDisplay Left="100" Top="150" Width="180" Height="180" IsShow="True"  ZIndex="1" UsePercent="False"/>

<ImageSource UriKind="Relative">NavIcons\lianliankan.png</ImageSource>

<ClickEvent>PopupEvent?TargetPageName=BriefingPage&TargetControlName=PageLeftSecondShow&X=0&Y=0&Height=841&Width=1604&EventID=PageHotBigBookShow&UriKind=Application&EventPath=Shell\Pages\BriefingPage\Items\PopupItems\SecondSho&PageName={$PageName}</ClickEvent>

</ImageButton>

l  <ImageButton>

<UIDisplay Left="100" Top="150" Width="180" Height="180" IsShow="True"  ZIndex="1" UsePercent="False"/>

<ImageSource UriKind="Relative">NavIcons\lianliankan.png</ImageSource>

<ClickEvent>ChangePopupState?State=Close&Args=imageButton</ClickEvent>

</ImageButton>

l  <ImageButton Name="turnoff">

      <UIDisplay Left="1865" Top="985" Width="50" Height="50" IsShow="True"  ZIndex="10" UsePercent="False"/>

      <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\turnoff.png</ImageSource>

  <ClickEvent>

     <Event IsLocal="True" SyncType="Client">Navigate?Page=GraphicPage</Event>

     <Event IsLocal="True" SyncType="Client">Navigate?Page=SweepPanelPage</Event>

   </ClickEvent>

 </ImageButton>

<ImageElement  Name="Background">
    <!--参考控件公用片段的讲解中UIDdisplay片段讲解-->
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="True"/>
    <!--参考控件公用片段的讲解中ImageSource片段讲解-->
    <ImageSource UriKind="Application">Shell\Pages\CirclePage\test.jpg</ImageSource>
</ImageElement>
```

## 配置说明

4.1 节点ClickEvent

此节点是按钮点击后触发事件的核心，也是框架配置项的核心。事件配置和Http中Request类似，采用如下格式进行： Action**?key1**=value1&value2=value2

在ClickEvent中根据不同的配置会做出不同的事件响应，以上配置文件样例中就是三种不同的响应效果；

第一种，打开一个悬浮控件(弹出窗口)，PopupEven是响应方式(打开悬浮控件)，TargetPageName在指定页面使用悬浮控件，&amp;是&的转义字符，表示与、和、连接的意思，TagetControlName为所需使用悬浮控件的名称，弹出窗口的名称，X**为距左边框**距离
Y距上边框距离 Width宽度
Height高度,**EventId**为所要使用到的悬浮控件的模板，UriKind为配置路径的类型，Relative是相对于当前xml的位置，Application是相对于整个demo的位置，Absolute是真实的物理路径，如c:\Images\，EventPath为模板所在的路径位置，**此处还**可以向控件传递参数，如示例中的PageName(多个之间&amp;连接)，以上为指定固定位置出现悬浮控件，若想使得所需弹出的悬浮控件在随着点击位置改变而改变则需加入LocationKind=Relative即可；

第二种，实现点击进行按钮页面间跳转的效果配置
，Navigate为响应方式（页面跳转），HomePage就是所跳到的目标页面；

第三种，关闭悬浮控件(弹出窗口)，ChangePopupState是响应方式(改变悬浮控件的状态)State=Close状态为关闭。

4.2  节点Event

此节点为2.0版本特有的属性，主要实现一个按钮点击之后实现两种效果，如上面配置文本样例中，同时跳转两个页面，或者也可以实现跳出两个弹出框，又或者是关闭自身的弹出框，同时弹出新弹出框。

```
        4.2.1 属性说明（以下属性主要针对两台机器通信时的状态）


                   **IsLocal**：本地是否也实现这个事件；


                  **SyncType**：该机器是server**端还是**Client端，与system中的设置匹配。
```
