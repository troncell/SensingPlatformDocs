# 相对布局控件（XYContainerElement）

## 控件作用

相对布局控件可以将多个基本控件组合成一个基本的控件，当一个配置下只能放置一个控件，且这个控件要实现多个功能时就需要将多个基本控件组合成一个控件。

## 配置文件样例

```
<XYContainerElement>
    <UIDisplay Left="0" Top="0" Width="0.5" Height="1" IsShow="True"  ZIndex="1" UsePercent="True"/>
    <Controls>
        <ImageButton>
            <UIDisplay Left="0" Top="0" Width="180" Height="180" IsShow="True"  ZIndex="1" UsePercent="false"/>
            <ImageSource UriKind="Relative">NavIcons\bubble.png</ImageSource>
            <ClickEvent>PopupEvent?TargetPageName=HomePage&TargetControlName=VideoElement&X=100&Y=100&Height=100&Width=200&EventID=PC03.wmv&EventPath=</ClickEvent>
        </ImageButton>
    </Controls>
</XYContainerElement>

```
