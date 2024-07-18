# **图片控件**（**ImageElement**）

## 控件作用

在页面或者弹出框中直接显示图片。

## 控件 UI 效果

![Placeholder](../images/imageelement_1.png)

## 配置文件样例

```
<ImageElement  Name="Background">
    <!--参考控件公用片段的讲解中UIDdisplay片段讲解-->
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="True"/>
    <!--参考控件公用片段的讲解中ImageSource片段讲解-->
    <ImageSource UriKind="Application">Shell\Pages\CirclePage\test.jpg</ImageSource>
</ImageElement>
```

## 配置说明

1.ImageSource 中 UriKind 是配置路径的类型，Relative 是相对于当前 xml 的位置，Application 是相对于整个 demo 的位置，Absolute 是真实的物理路径，如 c:\Images\

示例：

```

<ImageSourceUriKind="Application">Shell\Pages\CirclePage\test.jpg </ImageSource>
```

ImageElement>是相对于整个 demo 的路径

```
<ImageSourceUriKind="Relative"> lianliankan.png </ImageSource>
```

是相对于当前 xml 文件所在的相对路径下的文件夹，此文件是与当前 xml 文件同级文件夹下

## 可接受的事件

1. SourceChanged, 用户动态变更此ImageElement的图片

# UIControlDict.xml 添加图片控件

如果使用图片控件则需要在 UIControlDict.xml 中添加图片控件

```

  <Element ViewType="ImageElement" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.ImageControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.ImageElementViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```
