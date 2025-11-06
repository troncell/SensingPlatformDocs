# 旋转控件（CircularItemsElement）

## 控件作用

旋转控件主要作用就是使配置内容围绕某个中心点旋转。

## 控件 UI 效果

<img style="width:200px;height:350px" src="image/CircularItemsElement/1762413423947.png" alt="输入图片说明" />

## 配置文件样例

```
<CircularItemsElement >
	<UIDisplay Left="200" Top="700" Width="1600" Height="1600" IsShow="True" ZIndex="4" UsePercent="false" />
	<Items IsCacheUI="True">
      <!-- Items下支持现有的XYContainerElement、ImageButton、TextElement等控件 -->
			<XYContainerElement>
				<UIDisplay Left="0" Top="0" Width="461" Height="460" />
				<Controls>
					<ImageButton>
						<UIDisplay Left="0" Top="0" Width="461" Height="460" IsShow="True" ZIndex="1" UsePercent="False"/>
						<ImageSource UriKind="Application">Shell\Pages\AllPage\resource\社会责任.png</ImageSource>
						<ClickEvent>
							<Event>Navigate?Page=FirstPage</Event>
						</ClickEvent>
					</ImageButton>
				</Controls>
			</XYContainerElement>

			<XYContainerElement>
				<UIDisplay Left="0" Top="0" Width="461" Height="460" />
				<Controls>
					<ImageButton>
						<UIDisplay Left="0" Top="0" Width="461" Height="461" IsShow="True" ZIndex="2" UsePercent="False"/>

						<ImageSource UriKind="Application">Shell\Pages\AllPage\resource\文化风貌.png</ImageSource>

						<ClickEvent>
							<Event>Navigate?Page=SecondPage</Event>
						</ClickEvent>
					</ImageButton>
				</Controls>
			</XYContainerElement>

			<XYContainerElement>
				<UIDisplay Left="500" Top="0" Width="461" Height="460" />
				<Controls>
					<ImageButton>
						<UIDisplay Left="0" Top="0" Width="661" Height="661" IsShow="True" ZIndex="1" UsePercent="False"/>

						<ImageSource UriKind="Application">Shell\Pages\AllPage\resource\主要业绩介绍.png</ImageSource>

						<ClickEvent>
							<Event>Navigate?Page=ThirdPage</Event>
						</ClickEvent>
					</ImageButton>
				</Controls>
			</XYContainerElement>
			<XYContainerElement>
				<UIDisplay Left="600" Top="600" Width="461" Height="460"/>
				<Controls>
					<ImageButton>
						<UIDisplay Left="0" Top="0" Width="460" Height="460" IsShow="True" ZIndex="1" UsePercent="False"/>

						<ImageSource UriKind="Application">Shell\Pages\AllPage\resource\实体模型互动.png</ImageSource>

						<ClickEvent>
							<Event>Navigate?Page=FourPage</Event>
						</ClickEvent>
					</ImageButton>
				</Controls>
			</XYContainerElement>
	</Items>
	<CustomerConfig>
    <!-- 背景图片(旋转的底图) -->
		<BackgroundImage UriKind="Project" Directory="Pages\AllPage\resource\组 11.png"></BackgroundImage>
    <!-- 自动旋转相关 -->
		<AutoRotate IsAutoPlay="True" MaxEllapsedTime="2000" RotationSpeed="10" />
    <!-- 配置旋转元素的中心点及阻尼 -->
		<CircularConfig Damping="0.1" Debug="True" CenterX="0.5" CenterY="0.5" />
	</CustomerConfig>

</CircularItemsElement>

```

## 配置说明

## AutoRotate

    IsAutoPlay：是否自动旋转
    MaxEllapsedTime：加载多久之后或手动旋转停止多久之后开始自动旋转
    RotationSpeed：旋转速度

## CircularConfig

    Damping：阻尼系数(0-1)，系数越大，手动旋转松手之后转动距离越短
    Debug：是否要查看中心位置
    CenterX：圆心的横坐标，0.5为圆心位置
    CenterY：圆心的纵坐标，0.5为圆心位置

# UIControlDict.xml 添加旋转控件

如果使用旋转控件则需要在 UIControlDict.xml 中添加图片旋转控件

```
  <Element ViewType="CircularItemsElement" AssemblyFile="UI.CircularPanel.dll" TypeName="UI.CircularPanel.CircularItemsControl, UI.CircularPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.CircularPanel.dll" TypeName="UI.CircularPanel.CircularItemsElementViewModel, UI.CircularPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"/>
  </Element>

```
