# 幻影墙控件（PerspectiveWallElement）

## 控件作用

幻影墙控件主要用来展示历史事件，使历史事件富有层级感，使人产生一种魔幻般的感觉。


## 控件UI效果
![Placeholder](../../images/PerspectiveWallElement.png)

## 配置文件样例

```
<PerspectiveWallElement Name="PWall">
	<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
	<DataProvider>
		PWallData?CSTable=PWall
	</DataProvider>
	<Items>
		<Template>
			<ImageButton>
				<UIDisplay Left="100" Top="100" Width="300" Height="225" IsShow="True" ZIndex="1" UsePercent="False" />
				<ImageSource UriKind="Absolute">
					{$ImagePath}
				</ImageSource>
				<ClickEvent>
					PopupEvent?X=300&amp;Y=300&amp;Height=630&amp;Width=1120&amp;EventID={$EventID}&amp;UriKind=Application&amp;EventPath={$EventDirection}
				</ClickEvent>
			</ImageButton>
		</Template>
	</Items>
	<CustomerConfig>
		<!-- MaxLayer纵深层数（可见为层数-1,最小不能小于2），MaxCountPerLayer每层的事件数（不能小于1），Distance层间距（最小不能少于ZoomStep的3倍，否则可能无法出现层次），Detal="300.0" Idle动画每祯位移 CardDistance事件间距（建议500不要修改），CardWidth事件宽度，CardHeight事件高度，ZoomStep层切换步进，OriginX和OriginY定义中心点 -->
		<PerspectiveWall MaxLayer="8" MaxCountPerLayer="4" Distance="600.0" CardDistance="500.0" Detal="300.0" CardWidth="600" CardHeight="400" ZoomStep="40.0" OriginX="960.0" OriginY="540.0" IdleAnimeStep="6" IdleTime="10000">
			<!-- 摄像机Z轴位置（可以为正，也可以为负值，但是数值建议不要更改），PositionX和PositionY摄像机平面位置，CameraField视角（相对于中心点的角度） -->
			<ViewCamera ViewingDistance="-1000.0" PositionX="0.0" PositionY="300.0" CameraField="120">
			</ViewCamera>
			<Surface SkipTime="50">
			</Surface>
			<!-- 是否自动播放，IdleTime为在规定时间内没人操作将进行自动播放，单位为毫秒，Step为速度，正值为从前向后，负值为从后向前 -->
			<AutoPlay IdleTime="10000" Step="-6">
			</AutoPlay>
		</PerspectiveWall>
	</CustomerConfig>
</PerspectiveWallElement>

```
```
<Root>
	<!-- Left为距左边框距离 Top距上边框距离 Width宽度 Height高度 -->
	<Rect Left="0.0" Top="0.0" Width="960" Height="540">
	</Rect>
	<Rect Left="960.0" Top="0.0" Width="960" Height="540">
	</Rect>
	<Rect Left="0.0" Top="540.0" Width="640" Height="540">
	</Rect>
	<Rect Left="640.0" Top="540.0" Width="640" Height="540">
	</Rect>
	<Rect Left="1280.0" Top="540.0" Width="640" Height="540">
	</Rect>
</Root>

```

## 配置说明

### 节点PerspectiveWall

	属性说明

		MaxLayer:  纵深层数（可见为层数-1,最小不能小于2）；

		MaxCountPerLayer：每层的事件数（不能小于1）；

		Distance：层间距最小不能少于ZoomStep的3倍，否则可能无法出现层次；

		Detal：Idle动画每祯位移；

		CardDistance：事件间距（建议500不要修改）；

		CardWidth：事件宽度；

		CardHeight：事件高度；

		ZoomStep：层切换步进；

		OriginX、OriginY：定义中心点。

### 节点ViewCamera

	属性说明

		ViewingDistance：摄像机Z轴位置（可以为正，也可以为负值，但是数值建议不要更改）;

		PositionX、PositionY: 摄像机平面位置;

		CameraField: 视角（相对于中心点的角度）。

		此外，需在此页面的同级目录下新建名为：PWall文件夹，在PWall文件夹下新建名为Template的文件夹，在Template文件夹下分别新建名为Template01.xml，在Template01.xml中放置配置文本样例中的样例2。


