# 弹出框控件（PopupShowElement）

## 控件作用

弹出框控件主要用于更加详细地介绍页面中的内容。

通常情况每个页面的悬浮控件所使用的格式都是相同的(是否可以移动，是否可以改变大小)，所以一般会把悬浮控件的内容抽象出来放到公共的 xml 中，如果页面使用到悬浮控都会使用一段引用代码来引用控件的配置文件，引用代码写在调用悬浮控件的页面中.

可以接受事件Control 使页面可以隐藏与显示

## 控件 UI 效果

![Placeholder](../images/PopupShowElement.png)

## 配置文件样例

```
<PopupShowElement Name="PopItems">
<!--使用IncludeTemplate 表示使用引用控件 FileSource为所引用的文件，具体含义请参考控件公用片段的讲解中FileSource片段讲解-->
    <IncludeTemplate>
        <FileSource UriKind="Application">Resource\ CanMovePopup\PopupShow.xml</FileSource>
    </IncludeTemplate>
</PopupShowElement>
```

```
（在上述FileSource指定的文件夹下新建上述指定名称的xml文件，这里是PopupShow.xml，分为固定型和可改变型，第一种为可改变型，第二种为固定型）

<Template>
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"  ZIndex="6" UsePercent="False"/>
    <CustomerConfig>
        <!--参考CanContraint是否为可变True/false BounceRect.X, BounceRect.Y为弹出框出现的位置，BounceRect.Width为碰撞宽度，BounceRect.Height为碰撞高度，MaxScale为放大最大倍数，MinScale为缩小最大倍数，ScaleMode为缩小到小于最小倍数的样式Disppear为消失  -->
        <LayoutManager LayoutType="PopupShowLayout" CanContraint="True" BounceRect.X="0" BounceRect.Y="0" BounceRect.Width="1920"  BounceRect.Height="1080" MaxScale="2" MinScale="0.45" ScaleMode="Disppear"></LayoutManager>
    </CustomerConfig>
</Template>
<Template >
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"  ZIndex="6" UsePercent="False"/>
    <CustomerConfig>
        <LayoutManager  CanMove="False" CanScale="False" MaxItemCount="1"></LayoutManager>
        <HotShowMappings></HotShowMappings>
    </CustomerConfig>
</Template>


```

## 配置说明

### 节点 LayoutManager

    属性说明

    LayoutType：PopupShowLayout，弹出框特有的属性，一般情况都无需改变；

    CanContraint：是否为可变，True/false；

    BounceRect.X、 BounceRect.Y：弹出框出现的位置；

    BounceRect.Width：碰撞宽度；

    BounceRect.Height：碰撞高度；

    MaxScale：放大最大倍数；

    MinScale：缩小最大倍数；

    ScaleMode：缩小到小于最小倍数的样式，Disppear 缩小消失， Normal  无控制缩放， Bounce 缩放弹。

## 调用弹框

配置好弹出框的模式以后就要在调用弹出框的使用中配置他的样式，正常是使用。

ImageButton 中 ClickEvent 属性进行调用弹出框，ClickEvent 中的参数属性请参照简单控件中 ImageButton 控件的配置中的属性，下面是截取一段 ClickEvent 进行说明

```
<ClickEvent>PopupEvent?TargetPageName=BriefingPage&TargetControlName=PageLeftSecondShow&;X=0&Y=0&Height=841&Width=1604&EventID=PageHotBigBookShow&UriKind=Application&EventPath=Shell\Pages\BriefingPage\Items\PopupItems\SecondSho&PageName={$PageName}ClickEvent>

```

代码中蓝色区域为调用弹出框的样式，其中 UrlKind 为调用的路径模式，在以上的 FileSource 配置中已经说明，此处不再做说明，EventPath 为所配置的弹出框的配置文件所在位置，EventID 为弹出框的名称，需要在刚刚指定的位置下新建与 EventID 的相同的名称的文件夹，在新建的文件夹下新建名与文件夹相同的 XML 文件

**在新建的 xml 文件夹下加入如下方得样例代码：**
具体可参考 ImageButton 里得打开关闭弹框

```
<Template>
<SysPage>
<!--参考控件公用片段的讲解中UIDisplay片段讲解-->
<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"
ZIndex="1" UsePercent="False"/>
<Controls>
<!--放置简单的控件ImageButton用于关闭弹出框，如何配置控件请参考基本控件配置中
ImageButton控件的配置方法-->
<ImageButton>
<UIDisplay Left="1480" Top="950" Width="158" Height="42" IsShow="True" ZIndex="5" UsePercent="False"/>
<ImageSource UriKind="Application">Resource\Picture\Others\close.png</ImageSource> 创思感知技术文档 2014.7 对应主版本：V1.2
<ClickEvent>ChangePopupState?State=Close&amp;Args=imageButton</ClickEvent>
</ImageButton>
</Controls>
</SysPage>
</Template>
```

# UIControlDict.xml 添加弹出框控件

如果使用弹出框控件则需要在 UIControlDict.xml 中添加弹出框控件

```

  <Element ViewType="PopupShowElement" AssemblyFile="UI.SweepPanel.dll" TypeName="UI.SweepPanel.PopupControl.PopupShowControl, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.SweepPanel.dll" TypeName="UI.SweepPanel.PopupControl.PopupShowElementViewModel, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```
