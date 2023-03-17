# 时间控件（DateTimesElement）

## 控件作用

时间控件自动显示本台计算机上面的时间。

## 控件UI效果
![Placeholder](../images/DataTimesElement.png)

## 配置文件样例

```
<DateTimesElement>
	<UIDisplay Left="500" Top="0" Width="600" Height="110" IsShow="True" ZIndex="5" UsePercent="false" />
      <CustomerConfig>
        <Date Foreground="#FFFFFFFF" Family="微软雅黑" FontSize="30" CultureInfo="zh-CN" Alignment="Center" Left="0" Top="0" Format="yyyy-MM-dd"></Date>
        <Week Foreground="#FFFFFFFF" Family="微软雅黑" FontSize="30" CultureInfo="zh-CN" Alignment="Center" Left="200" Top="0" Format="dddd"></Week>
        <Time Foreground="#FFFFFFFF" Family="微软雅黑" FontSize="30" CultureInfo="zh-CN" Alignment="Center" Left="300" Top="0" Format="HH:mm:ss"></Time>
      </CustomerConfig>
</DateTimesElement>


```

## 配置说明

### 节点Date/Week/Time

	属性说明

		Foreground：字体的颜色；

		Family：放大倍数； 

		FontSize：字体样式；
		FontWeight：默认值为normal,
		Left/Top:相对于当前控件的位置
		Culture：显示不同国家的日期格式，中文为 zh-CN，美国为 en-US
		Format为显示的格式： yyyy表示当前的年份，如2023，MM表示当前时间的月份，如03月，dd表示为本月的天数，如 17日， dddd表示当天是星期几，HH/mm/ss分别表示时/分/秒，更详细的信息可以在线查找时间格式的文档 [详细格式说明](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings)
	


 



 


