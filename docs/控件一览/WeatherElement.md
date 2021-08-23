# 天气控件（WeatherElement）

## 控件作用

天气控件自动显示中国天气网中当时的天气。

## 控件UI效果
![Placeholder](../../images/WeatherElement.png)

## 配置文件样例

```
<WeatherElement>
    <UIDisplay Left="500" Top="400" Width="500" Height="254" IsShow="True" ZIndex="5" UsePercent="false" />
    <CustomerConfig>
        <WeatherSet CityName="上海" Ratio="1" ForegroundColor="#FFFFFF00" Size="16" Family="微软雅黑" CityIsShow = "False" />
    </CustomerConfig>
</WeatherElement>
```

## 配置说明

### 节点WeatherSet

	属性说明

		CityName:所在城市；

		Ratio：放大倍数；

		ForegroundColor：字体的颜色；

		Size：字体大小；

		Family：字体样式；

		CityIsShow：是否显示城市的名称。


