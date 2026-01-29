数字控件（NumberElement）

## 控件作用

数字滚动动画（类似于抽奖机、计时器或者游戏分数那样滚动出最终数字）

## 控件 UI 效果

![Placeholder](../images/shuzi.mp4)

## 配置文件样例

```xml
<NumberElement>
	<UIDisplay Left="0" Top="0" Width="300" Height="300" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1"/>
	<CustomerConfig>
		<Shu Number="1234567" Speed="100" Delay="5000"/>
	</CustomerConfig>
</NumberElement>

```

## 配置说明

## Shu

    Number：最终要显示的数字
    Speed：数字滚动的快慢，数值越小，滚动越快；数值越大，滚动越慢
    Delay：整个动画的统一延迟，即多长时间后开始加载动画，单位为毫秒


## UIControlDict.xml 添加数字控件

如果使用数字控件则需要在 UIControlDict.xml 中添加数字控件，并且启用SensingData模块，并且通过AppPod配置软件

```
  <!-- 数字 -->
  <Element ViewType="NumberElement" AssemblyFile="UI.ShuZi.dll" TypeName="UI.ShuZi.ShuZiControl, UI.ShuZi, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
	  <DataContext AssemblyFile="UI.ShuZi.dll" TypeName="UI.ShuZi.ShuZiControlViewModel, UI.ShuZi, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```


