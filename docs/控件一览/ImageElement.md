# **图片控件**（**ImageElement**）

## 控件作用

在页面或者弹出框中直接显示图片。


## 控件UI效果
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

1. 以上节点均已在别的配置文件中详细介绍，这里就不再重复了。
