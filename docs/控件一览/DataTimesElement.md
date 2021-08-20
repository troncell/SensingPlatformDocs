# 时间控件（DataTimesElement）

## 控件作用

时间控件自动显示本台计算机上面的时间。


![Placeholder](../../images/DataTimesElement.png)

## 配置文件样例

```
<DateTimesElement>
	<UIDisplay Left="500" Top="0" Width="600" Height="110" IsShow="True" ZIndex="5" UsePercent="false" />
	<CustomerConfig>
		<!-- LineStyle：ALine/TwoLine -->
		<TimeStyle ForegroundColor="#FFFFFF" Family="微软雅黑" Ratio="1" LineStyle="ALine" />
	</CustomerConfig>
</DateTimesElement>


```

## 配置说明

### 节点TimeStyle

	属性说明

		ForegroundColor：字体的颜色；

		Ratio：放大倍数； 

		Family：字体样式；

		LineStyle：一行显示还是分两行显示。


 



 


