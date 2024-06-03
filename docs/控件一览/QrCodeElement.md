# 二维码控件（QrCodeElement）

## 控件作用

在页面中显示二维码。

## 控件 UI 效果

![Placeholder](../images/QrCodeElement.png)

## 配置文件样例

```
<QrCodeElement>
	<UIDisplay Left="500" Top="500" Width="300" Height="300" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1"/>
	<CustomerConfig>
        <QrCode LightBrush="#FFFFFFFF" DarkBrush="#FF000000" IsGrayImage="True"  Text="https://troncell.com"></QrCode>
	</CustomerConfig>
</QrCodeElement>


```

## 配置说明

### 节点 CustomerConfig

    属性说明

        LightBrush：调整二维码白色部分的颜色；

        DarkBrush：调整二维码黑色部分的颜色；

        IsGrayImage：灰度图片，True或Flase，为True时不能调整颜色，只能调整亮度，为Flase时可以调整颜色；

        Text：填写想要生成二维码的url；

# UIControlDict.xml 添加二维码控件

如果使用二维码控件则需要在 UIControlDict.xml 中添加二维码控件

```
  <!--UI.QrCode 控件包-->
  <Element ViewType="QrCodeElement" AssemblyFile="UI.QrCode.dll" TypeName="UI.QrCode.QrCodeControl, UI.QrCode, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.QrCode.dll" TypeName="UI.QrCode.QrCodeControlViewModel, UI.QrCode, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.QrCode END-->
```
