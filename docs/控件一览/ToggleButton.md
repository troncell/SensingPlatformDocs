# 支持两种状态的图片按钮控件（ToggleButton）

## 控件作用

支持两种状态的图片按钮控件,点击图片按钮触发事件。

## 控件UI效果

![Placeholder](../images/ToggleButton.gif)

## 配置文件样例

```
<ToggleButton>
	<UIDisplay Left="523" Top="878" Width="300" Height="90" IsShow="True" ZIndex="4" UsePercent="False" />
	<CustomerConfig>
		<ImageSource UriKind="Application">Shell\Pages\img\独孤九剑.png</ImageSource>
		<ImageSourceChecked UriKind="Application">Shell\Pages\img\独孤九剑高亮.png</ImageSourceChecked>
		  <ClickEvent>Navigate?Page=HomePage</ClickEvent>
		  <GroupName>img</GroupName>
		  <Button AutoClick="True" />
		  <IsChecked>False</IsChecked> 
	</CustomerConfig>
</ToggleButton>



```
## 配置说明

### 节点CustomerConfig

   属性说明

        GroupName：给按钮分组，样例中的组名为img，若多个ToggleButton为同一个组，ToggleButton之间可以交互。

        Button AutoClick：自动按钮，True或False

        IsChecked：进入页面中图片的点击状态，True或False，True为已被点击，False为未被点击。

        




