# 气泡控件（BubbleElement）

## 控件作用

气泡控件可分为连接数据库动态生成气泡个数，和用户自定义气泡个数，配置时只需要改变 Items 中的节点即可。

## 控件 UI 效果

![Placeholder](../images/BubbleElement.png)

## 配置文件样例

```
<!--Name 为控件在页面中的名字，为可选项-->
<BubbleElement Name="BubbleElement">
<!--参考控件公用片段CommonElement.md讲解中UIDisplay片段讲解-->
	<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
	<!--参考控件公用片段CommonElement.md讲解中DataProvide片段讲解-->
	<DataProvider>BubbleData?CSTable=Bubble</DataProvider>
	<Items>
		<Template TemplateID="10001">
		  <!-- 放置简单的控件ImageButton，如何配置控件请参考基本控件配置中ImageButton控件的配置方法 -->
			 <ImageButton>
            <UIDisplay Left="100" Top="100" Width="127" Height="207" IsShow="True" ZIndex="1" UsePercent="False"/>
            <ImageSource UriKind="Application">Shell\Pages\BubbleElement\resource\{$Bubble}</ImageSource>
            <ClickEvent>PopupEvent?TargetPageName=BubbleElement&TargetControlName=PopItems&X=0&Y=0&Height=841&Width=1604&EventID={$EventID}&UriKind=Application&EventPath=Shell\Pages\BubbleElement\tck</ClickEvent>
          </ImageButton>
		</Template>
<Item>
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

### 节点 BubbleConfig

    Bubble控件自身的一些特殊效果。

### 节点 NoiseBubble

    设置没有信息显示的小泡泡的配置。

#### 属性说明

    Count：小泡泡的数量；

    Image：小泡泡的显示图案；

    MinRadius：小泡泡的最小半径；

    MaxRadius：小泡泡的最大半径。

## UIControlDict.xml 添加气泡控件

如果使用气泡控件则需要在 UIControlDict.xml 中添加气泡控件

```
    <!--UI.Bubble控件包-->

  <Element ViewType="BubbleElement" AssemblyFile="UI.Bubble.dll" TypeName="UI.Bubble.BubbleControl, UI.Bubble, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Bubble.dll" TypeName="UI.Bubble.BubbleControlViewModel, UI.Bubble, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.Bubble End-->
```
