# 3D互动墙控件（InteractiveWall3DElement）

## 控件作用

3D互动墙控件主要用于展示每个阶段发生的事件。

![Placeholder](../../images/InteractiveWall3DElement.png)

## 配置文件样例

```
<InteractiveWall3DElement>
	<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="false" IsUseCache="false" />
	<DataProvider>
		IntroductionData?CSTable=AboutUs
	</DataProvider>
	<CustomerConfig>
		<InteractiveWall3D>
			<Layout Per3DHeight="750" ItemSpan="150" />
			<Zoom ZoomValue="1.5" ZoomStatusAngle="-45" />
			<AnimationTime>
				1000
			</AnimationTime>
			<CardInfoLayout Width="500" Height="400" Left="1158" />
		</InteractiveWall3D>
	</CustomerConfig>
</InteractiveWall3DElement>

```

## 配置说明

节点InteractiveWall3D

	属性说明

		Per3DHeight:2D画面的多少像素对应3D的一个单位；

		ItemSpan：放大以后Wall的倾斜角度；

		ZoomValue：点击某个Card以后放大的3D距离；

		ZoomStatusAngle：放大以后Wall的倾斜度

### 节点AnimationTime

	动画间隔时间 。

### 节点CardInfoLayout

	点开后的每个面板中的详细信息（宽，高，左边间距）。
