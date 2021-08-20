# 电子书控件（BookElement）

## 控件作用

电子书控件以翻书的交互方式展示一系列图片。

![Placeholder](../../images/BookElement.png)

## 配置文件样例

```
<BookElement>
	<UIDisplay Left="165" Top="280" Width="1396" Height="588" IsShow="True" ZIndex="3" UsePercent="False" />
	<DataProvider>
		EBookData?CSTable=TEduBook5
	</DataProvider>
	<Items>
		<Item>
			<ImageButton>
				<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1" UsePercent="False" />
				<ImageSource UriKind="Application">
					Shell\Data\KPIRedA.png
				</ImageSource>
				<ClickEvent>
					Navigate?Page=HomePage&Args=imageButton
				</ClickEvent>
			</ImageButton>
		</Item>
	</Items>
	<CustomerConfig>
		<Book IsCacheUI="True" ShadowLevel="0.6" Width="865" Height="665">
			<TouchSurface>
				<TouchRect Left="0.0" Top="0.0" Height="0.5" Width="0.2" BookState="LT2RT">
				</TouchRect>
				<TouchRect Left="0.0" Top="0.5" Height="0.5" Width="0.2" BookState="LB2RB">
				</TouchRect>
				<TouchRect Left="0.8" Top="0.0" Height="0.5" Width="0.2" BookState="RT2LT">
				</TouchRect>
				<TouchRect Left="0.8" Top="0.5" Height="0.5" Width="0.2" BookState="RB2LB">
				</TouchRect>
			</TouchSurface>
		</Book>
	</CustomerConfig>
</BookElement>



```

## 配置说明

### 节点Book

#### 属性说明

      IsCaCheUI:  是否预加载，就是是否在刚进入放电子书的页面时就加载所有页面，True为是，False为否；

      ShadowLevel：阴影的宽度；

      这里的Width、Height指的是书本的大小；

      TouchSurface：定义点击范围的边界。

