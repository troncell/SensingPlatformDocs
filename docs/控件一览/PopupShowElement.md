# 弹出框控件（PopupShowElement）

## 控件作用

弹出框控件主要用于更加详细地介绍页面中的内容。

## 控件UI效果

![Placeholder](../../images/PopupShowElement.png)

## 配置文件样例

```
（页面中）

<PopupShowElement Name="PopItems">
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

### 节点LayoutManager

    属性说明

        LayoutType：PopupShowLayout，弹出框特有的属性，一般情况都无需改变；

        CanContraint：是否为可变，True/false；

        BounceRect.X、 BounceRect.Y：弹出框出现的位置；

        BounceRect.Width：碰撞宽度；

        BounceRect.Height：碰撞高度；

        MaxScale：放大最大倍数；

        MinScale：缩小最大倍数；

        ScaleMode：缩小到小于最小倍数的样式，Disppear 缩小消失， Normal  无控制缩放， Bounce 缩放弹。




