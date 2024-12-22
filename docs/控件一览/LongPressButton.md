# 长按按钮控件（LongPressButton）

## 控件作用

一般作为一张透明图片，长按按钮三秒触发事件，可以配置序列帧，长按可以触发动画效果，动画效果结束触发事件。

## 控件 UI 效果

![Placeholder](../images/LongPressButton.gif)

## 配置文件样例

```

<LongPressButton>
    <UIDisplay Left="0" Top="0" Width="300" Height="300" IsShow="True" ZIndex="4" UsePercent="False" Opacity="1"/>
    <ImageSource UriKind="Project" Interval="20">Pages\HomePage\resource\圈\分离</ImageSource>
    <ClickEvent>Navigate?Page=HomePage</ClickEvent>
</LongPressButton>



```

## 配置说明

### 节点 UIDisplay

    1. 以上节点均已在别的配置文件中详细介绍，这里就不再重复了。

# UIControlDict.xml 添加长按按钮控件

如果使用长按按钮控件则需要在 UIControlDict.xml 中添加长按按钮控件

```
 <Element ViewType="LongPressButton" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.LongPressButton, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
 <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.LongPressButtonViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```
