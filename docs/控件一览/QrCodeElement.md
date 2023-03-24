# 二维码控件（QrCodeElement）

## 控件作用

在页面中显示二维码。

## 控件UI效果

![Placeholder](../../images/QrCodeElement.png)

## 配置文件样例

```
（页面中）

   <QrCodeElement>
	  	<UIDisplay Left="500" Top="500" Width="300" Height="300" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1"/>
	  	 <CustomerConfig>
          <QrCode LightBrush="#FFFFFFFF" DarkBrush="#FF000000" IsGrayImage="True"  Text="https://troncell.com"></QrCode>
		  </CustomerConfig>
  	</QrCodeElement>


```
## 配置说明

### 节点CustomerConfig

    属性说明

        LightBrush：调整亮度；

        DarkBrush：调整暗度；

        IsGrayImage：；

        Text：填写想要生成二维码的url；

        




