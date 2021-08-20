# 气泡控件（BubbleElement）

## 控件作用

气泡控件可分为连接数据库动态生成气泡个数，和用户自定义气泡个数，配置时只需要改变Items中的节点即可。


![Placeholder](../../images/BubbleElement.png)

## 配置文件样例

```
<BubbleElement Name="BubbleElement">
	<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
	<DataProvider>
		BubbleData?CSTable=Bubble
	</DataProvider>
	<Items>
		<Template>
			<ImageButton>
				<UIDisplay Left="100" Top="100" Width="250" Height="243" IsShow="True" ZIndex="1" UsePercent="False" />
				<ImageSource UriKind="Application">
					{$IconPath}
				</ImageSource>
				<ClickEvent>
					{$EventAction}?X=300&amp;Y=300&amp;Height=630&amp;Width=1120&amp;EventID={$EventID}&amp;UriKind=Application&amp;EventPath={$EventPath}
				</ClickEvent>
			</ImageButton>
		</Template>
		<Item>
			<!-- 放置简单的控件ImageButton，如何配置控件请参考基本控件配置中ImageButton控件的配置方法 -->
			<ImageButton>
				<UIDisplay Left="100" Top="100" Width="250" Height="243" IsShow="True" ZIndex="1" UsePercent="False" />
				<ImageSource UriKind="Application">
					Shell\Data\Bubble.png
				</ImageSource>
				<ClickEvent>
					PopupEvent?X=300&amp;Y=300&amp;Height=630&amp;Width=1120&amp;EventID=0001&amp;UriKind=Application&amp;EventPath=Shell\Data\BubbleData\PopupEvents\
				</ClickEvent>
			</ImageButton>
		</Item>
	</Items>
	<!-- 放置CustomerConfig片段 -->
	<CustomerConfig>
		<!-- 放置BubbleConfig片段 -->
		<BubbleConfig>
			<!-- 放置NoiseBubble片段，进行没有信息显示的小泡泡的配置，Count是小泡泡的数量，Image为小泡泡的显示图案，MinRadius是小泡泡的最小半径，MaxRadius是小泡泡的最大半径 -->
			<NoiseBubble Count="10" Image="" MinRadius="10" MaxRadius="40">
			</NoiseBubble>
		</BubbleConfig>
	</CustomerConfig>
</BubbleElement>

```


## 配置说明

### 节点BubbleConfig

	Bubble控件自身的一些特殊效果。

### 节点NoiseBubble

	设置没有信息显示的小泡泡的配置。

#### 属性说明    

		Count：小泡泡的数量；

		Image：小泡泡的显示图案；

		MinRadius：小泡泡的最小半径；

		MaxRadius：小泡泡的最大半径。

 


