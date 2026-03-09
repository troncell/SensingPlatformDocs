画图控件（PaintElement）

## 控件作用

在页面中生成绘画板画图。（目前不支持自定义配置背景板、颜色、保存路径等）

## 控件 UI 效果

![Placeholder](../images/Paint.png)

## 配置文件样例

```xml
<PaintElement>
	<UIDisplay Left="-100" Top="0" Width="300" Height="300" IsShow="True" ZIndex="7" UsePercent="False" Opacity="1"/>

	<CustomerConfig>
		 <!--整体画布背景（颜色或图片）--> 
		<Background Type="Color" Value="Red" />

		 <!--墨迹区域（InkCanvas）位置与默认画笔--> 
		<InkPanel>
			<DefaultPen Color="#FF000000" Width="6" Height="6" Pressure="0.35" />
		</InkPanel>

		 <!--清空按钮--> 
		<ClearButton IsShow="True" ZIndex="100">
			<Position Left="Auto" Right="30" Top="20" />
			<Size Width="100" Height="45" />
			<Style
			  Content="清空画布"
			  FontSize="16"
			  FontFamily="微软雅黑"
			  Background="#FFE8E8E8"
			  Foreground="#FF333333"
			  BorderThickness="1"
			  BorderColor="#FF999999"/>
		</ClearButton>

		 <!--保存按钮--> 
		<SaveButton IsShow="True" ZIndex="100">
			<Position Left="Auto" Right="30" Top="80" />
			<Size Width="100" Height="45" />
			<Style
			  Content="保存签名"
			  FontSize="16"
			  FontFamily="微软雅黑"
			  Background="#FFD0F0D0"
			  Foreground="#FF006600"
			  BorderThickness="1"
			  BorderColor="#FF88CC88"/>
		</SaveButton>

		 <!--保存设置--> 
		<SaveSettings>
			<Folder>Desktop\画板签名</Folder>
			<FilePrefix>签名_</FilePrefix>
			<Extension>.png</Extension>
			<ShowMessageAfterSave>true</ShowMessageAfterSave>
		</SaveSettings>

	</CustomerConfig>
</PaintElement>

```

## 配置说明

## Background(画板背景)
	Type：支持Color和Image
	Value：Color 支持名称/#ARGB，Image 是文件路径

## InkPanel(墨迹)
	DefaultPen：默认画笔，可以配置Color(颜色)、Width(画笔水平宽度)、Height(画笔垂直高度)、Pressure(影响粗细变化)

## ClearButton/SaveButton(清除/保存按钮)
	IsShow：是否显示
### Position
	Left左定位（Auto=不设置）
	Right右定位
	Top上定位
### Size
	Content按钮文字
	FontSize字体大小
	FontFamily字体
	Background按钮背景色
	Foreground文字颜色
	BorderThickness边框粗细
	BorderColor边框颜色

## SaveSettings
	Folder保存文件夹
	FilePrefix文件名前缀
	Extension文件扩展名
	ShowMessageAfterSave保存后是否弹出提示	


## UIControlDict.xml 添加画图控件

如果使用画图控件则需要在 UIControlDict.xml 中添加画图控件，并且启用SensingData模块，并且通过AppPod配置软件

```
  <!-- 画图 -->
  <Element ViewType="PaintElement" AssemblyFile="UI.Paint.dll" TypeName="UI.Paint.PaintControl, UI.Paint, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
	  <DataContext AssemblyFile="UI.Paint.dll" TypeName="UI.Paint.PaintControlViewModel, UI.Paint, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```


