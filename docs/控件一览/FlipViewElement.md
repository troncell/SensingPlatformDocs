# 卡片型滑块控件（FlipViewElement）

## 控件作用

卡片型滑块控件以翻日历的交互方式展示一系列图片。可接受IndexChanged事件。

## 控件 UI 效果

![Placeholder](../images/FlipViewElement.png)

## 配置文件样例

```
<FlipViewElement Name="resource">
	<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" />
	<DataProvider>
		AboutServiceData?CSTable=AboutService
	</DataProvider>
	<Items IsCacheUI="True">
		<Template Left="0" Top="0" Width="1920" Height="1080" TemplateID="10001">
			<XYContainerElement>
				<UIDisplay Left="0" Top="0" Width="1920" Height="1080" />
				<Controls>
					<ImageElement Name="resource">
						<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="True" />
						<ImageSource UriKind="Application">Shell\Pages\AboutServicePage\resource\{$ImageName}</ImageSource>
					</ImageElement>
					<ImageButton Name="resource">
						<UIDisplay Left="7" Top="474" Width="61" Height="102" IsShow="True" ZIndex="2" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="True" />
						<ImageSource UriKind="Application">Shell\Pages\AboutServicePage\resource\2.png</ImageSource>
						<ClickEvent>IndexChanged?Index={$LeftImage}&amp;Args=imageButton</ClickEvent>
					</ImageButton>
					<ImageButton Name="resource">
						<UIDisplay Left="1852" Top="474" Width="61" Height="102" IsShow="True" ZIndex="2" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="True" />
						<ImageSource UriKind="Application">Shell\Pages\AboutServicePage\resource\1.png</ImageSource>
						<ClickEvent>IndexChanged?Index={$RightImage}</ClickEvent>
					</ImageButton>
				</Controls>
			</XYContainerElement>
		</Template>
	</Items>
	<CustomerConfig>
		<FlipView SliderFactor="0.2" Orientation="Horizontal">
		</FlipView>
	</CustomerConfig>
</FlipViewElement>

```

```
     <FlipViewElement Name="FlipView">
        <UIDisplay Left="228" Top="265" Width="1466" Height="499" IsShow="True" ZIndex="1" UsePercent="False" />
        <DataProvider>qiyechanpinData?CSTable=zhinengyingjian</DataProvider>
        <Items IsCacheUI="True">
          <Template Left="0" Top="0" Width="1466" Height="499" TemplateID="10003">
            <ImageElement>
              <UIDisplay Left="30" Top="10" Width="1466" Height="499" IsShow="True" ZIndex="1" UsePercent="False" />
              <ImageSource UriKind="Application">Shell\Pages\qiyePage\resource\xinxifabu\智能硬件\{$TP}</ImageSource>
            </ImageElement>
          </Template>
        </Items>
        <CustomerConfig>
          <FlipView SliderFactor="0.2"></FlipView>
        </CustomerConfig>
      </FlipViewElement>
```

## 配置说明

### 节点 FlipView

    属性说明

    	SliderFactor="0.2"表示当一个页面滑动整个页面的五分之一的时候，它就会自动滑到下一个页面，该值越小该控件的灵敏度越高，若该控件中去掉该片段，则默认SliderFactor="0.5"，即只有滑至整个页面的二分之一时才能滑动。

    	Orientation:Horizontal(水平滑动)\Vertical(垂直滑动)

		IsLoop : True\False 是否循环播放

		SelectedIndex：默认为0 默认选中项
		
		CanAutoPlay：True\False 是否自动播放

		IdleTime ： 10000 默认10秒，自动播放时间间隔

		PageReload：True\False 是否在翻页时重新加载



# UIControlDict.xml 添加卡片型滑块控件

如果使用卡片型滑块控件则需要在 UIControlDict.xml 中添加卡片型滑块控件

````

<!--UI.FlipView 控件包-->
  <Element ViewType="FlipViewElement" AssemblyFile="UI.FlipView.dll" TypeName="UI.FlipView.FlipViewControl, UI.FlipView, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.FlipView.dll" TypeName="UI.FlipView.FlipViewViewModel, UI.FlipView, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.FlipView End-->
```
````
