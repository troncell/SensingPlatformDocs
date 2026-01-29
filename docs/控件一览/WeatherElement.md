天气控件（WeatherElement）

## 控件作用

天气控件自动显示中国天气网中当时的天气。

## 控件 UI 效果

![Placeholder](../images/weather.png)

## 配置文件样例

```xml
<WeatherElement>
	<UIDisplay Left="0" Top="0" Width="500" Height="254" IsShow="True" ZIndex="5" UsePercent="false" />
	<CustomerConfig>
				<WeatherImage Left="40" Top="20" Width="96" Height="96" IsShow="true" ZIndex="5"/>
				<Temperature Left="160" Top="45" Width="180" Height="70" Size="56" ForegroundColor="#FFFFFFFF" Family="微软雅黑" IsShow="true" ZIndex="4" />
				<City Left="60" Top="130" Width="240" Height="40" Size="28" ForegroundColor="#FFFFFFFF" Family="微软雅黑" ShowText="无锡" Value="无锡" />		
	</CustomerConfig>
</WeatherElement>

```

## 配置说明

## WeatherImage(对应的天气图标)

    Left、Top：位置属性
    Width、Height：大小属性
    IsShow：是否显示
    ZIndex：显示优先级
    天气图标存储于根目录的\Resource\Weather下，里面有文件夹day(白天的天气图标)、night(晚上的天气图标)、undefined.png(没有查询到天气数据时的默认显示图标)
    其中7:00-18:00为白天，其他为晚上

## Temperature(对应的温度)

    Left、Top：位置属性
    Width、Height：大小属性
    IsShow：是否显示
    ZIndex：显示优先级
    Size：字体大小
    ForegroundColor：字体颜色
    Family：字体样式

## City

    eft、Top：位置属性
    Width、Height：大小属性
    IsShow：是否显示
    ZIndex：显示优先级
    Size：字体大小
    ForegroundColor：字体颜色
    Family：字体样式
    ShowText：页面上显示的名称
    Value：要查询的城市

## UIControlDict.xml 添加天气控件

如果使用天气控件则需要在 UIControlDict.xml 中添加天气控件，并且启用SensingData模块，并且通过AppPod配置软件

```
  <!-- 天气 -->
  <Element ViewType="WeatherElement" AssemblyFile="UI.BdWeather.dll" TypeName="UI.BdWeather.WeatherInfoControl, UI.BdWeather, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
	  <DataContext AssemblyFile="UI.BdWeather.dll" TypeName="UI.BdWeather.WeatherInfoViewModel, UI.BdWeather, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```


