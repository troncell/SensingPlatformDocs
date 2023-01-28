# 环形卡片控件（CircleElement）

## 控件作用

环形卡片控件以360度环绕滑块的方式展示图片的列表。

## 控件UI效果
![Placeholder](../images/CircleElement.png | width=500)

## 配置文件样例

```
<CircleElement Name="CircleElement">
	<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="3" UsePercent="False" />
	<DataProvider>
		CirclePanelData?CSTable=Circle
	</DataProvider>
	<Items>
		<Template>
			<ImageButton Name="TestPageNav">
				<UIDisplay Left="100" Top="100" Width="150" Height="113" IsShow="True" ZIndex="1" UsePercent="False" />
				<ImageSource UriKind="Absolute">
					{$ImagePath}
				</ImageSource>
				<ClickEvent>
					Navigate?Page=TestPage&amp;Args=imageButton
				</ClickEvent>
			</ImageButton>
		</Template>
	</Items>
	<!-- 放置CustomerConfig片段 -->
	<CustomerConfig>
		<!-- 放置CirClePanel片段 -->
		<CirClePanel>
			<!-- 一放圈多少个 -->
			<MaxItemCount>
				17
			</MaxItemCount>
			<!-- 环形圈半径 -->
			<Radius>
				500
			</Radius>
			<!-- 倾斜角度 -->
			<CameraAngle>
				45
			</CameraAngle>
			<!-- 梯形角度 -->
			<ZoomAngle>
				0
			</ZoomAngle>
			<!-- 中心点位置 -->
			<Center X="800" Y="500">
			</Center>
			<!-- 配置滑块倒影是否显示 -->
			<ShowShadow>
				true
			</ShowShadow>
			<!-- 放置CirClePanel片段用户没有交互时，自动滚动时间间隔 -->
			<AutoScrollTime>
				00:00:14
			</AutoScrollTime>
			<!-- 滑动模式 横向：Horizontal，纵向：Vertical -->
			<ArrangeMode>
				Horizontal
			</ArrangeMode>
			<!-- 放置ClickSensity片段，配置点击灵明度 -->
			<ClickSensity>
				<!-- 最大响应时间，单位为毫秒 -->
				<MaxTime>
					800
				</MaxTime>
				<!-- 最小相应时间，单位为毫秒 -->
				<MinTime>
					2
				</MinTime>
			</ClickSensity>
		</CirClePanel>
	</CustomerConfig>
</CircleElement>

```

## 配置说明

### 节点CirClePanel

	该节点主要设置整个环形360的形态。

		属性说明

			MaxItemCount:放几个圈；

			Radius:环形圈的半径；

			CameraAngle：整个环形圈的倾斜角度；

			ZoomAngle：环形圈的梯形角度；

			Center：环形圈的中心点位置；

			ShowShadow：环形圈的倒影是否显示；

			AutoScrollTime： 用户没有交互时，自动滚动时间间隔，若不需要自动滚动，则将该属性去掉即可；

			ArrangeMode：滑动模式， 横向：Horizontal，纵向：Vertical；

### 节点ClickSensity

	设置环形圈的点击灵敏度。

		属性说明

			MaxTime：最大响应时间，单位为毫秒


 


