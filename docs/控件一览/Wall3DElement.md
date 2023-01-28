# 3D凹面墙控件（Wall3DElement）

## 控件作用

3D凹面墙主要将图片或视视频以3D的形式进行展示。

## 控件UI效果
![Placeholder](../images/Wall3DElement.png)

## 配置文件样例

```
<Wall3DElement>
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="false" IsUseCache="false" />
    <DataProvider>IntroductionData?CSTable=AboutUs</DataProvider>
    <Items>
        <Template  TemplateID="Image">
            <ImageElement  Name="Background">
                <UIDisplay Left="0" Top="0" Width="420" Height="540" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="True"/>
                <ImageSource UriKind="Absolute">{$FullName}</ImageSource>
            </ImageElement>
        </Template>
    </Items>
    <CustomerConfig>
        <Scenario3D>
            <Camera>
                <Default>
                    <FieldView>90</FieldView>
                    <Position>
                        <X>0</X>
                        <Y>0</Y>
                        <Z>4.6</Z>
                    </Position>
                    <LookDirection>
                        <X>0</X>
                        <Y>0</Y>
                        <Z>-1</Z>
                    </LookDirection>
                    <XAxisAngle>0</XAxisAngle>
                </Default>
                <Scaled>
                    <FieldView>90</FieldView>
                    <Position>
                        <X>0</X>
                        <Y>0</Y>
                        <Z>-3.2</Z>
                    </Position>
                    <LookDirection>
                        <X>0</X>
                        <Y>0</Y>
                        <Z>-1</Z>
                    </LookDirection>
                    <XAxisAngle>0</XAxisAngle>
                </Scaled>
                <FullView>
                    <FieldView>90</FieldView>
                    <Position>
                        <X>0</X>
                        <Y>0</Y>
                        <!--当3DWall变成一个圆筒时，摄像机会被拉远，Z轴最大为8.6-->
                        <Z>8.6</Z>
                    </Position>
                    <LookDirection>
                        <X>0</X>
                        <Y>0</Y>
                        <Z>-1</Z>
                    </LookDirection>
                    <XAxisAngle>80</XAxisAngle>
                </FullView>
            </Camera>
            <Model3D>
                <RadiusA>4.8</RadiusA>
                <RadiusB>5</RadiusB>
                <RadiusC>5</RadiusC>
                <Latitude>25</Latitude>
                <ItemMarginAngle>2</ItemMarginAngle>
                <SubItemMargin>2</SubItemMargin>
                <SubItemHeight>540</SubItemHeight>
                <SubItemWidth>420</SubItemWidth>
                <ShowRow>3</ShowRow>
                <ShowColumn>15</ShowColumn>
                <HasMirror>True</HasMirror>
            </Model3D>
        </Scenario3D>
        <Animation>
            <DefaultMoveInterval>2000</DefaultMoveInterval>
            <ScaledMoveInterval>500</ScaledMoveInterval>
            <ShrinkInterval>2000</ShrinkInterval>
        </Animation>
        <Source RootPath="Wall3D">
            <Extension>*.jpg</Extension>
        </Source>
    </CustomerConfig>
</Wall3DElement>

```

## 配置说明

### 节点Default

	摄像机默认设置。

### 节点FieldView

	摄像机默认视野。

### 节点Position

	摄像机的位置。

### 节点 LookDirection

	摄像机的朝向。

### 节点XAxisAngle

	摄像机绕X轴旋转的角度。

### 节点Scaled

	点击放大，拉近摄像机时摄像机的属性。

### 节点FullView

	当3DWall变成一个圆筒时摄像机的属性。

### 节点XAxisAngle

	摄像机绕X轴的最大角度，旋转80度后就不能继续旋转了。

### 节点Model3D

	属性说明

		RadiusA、RadiusB、RadiusC：椭球的三个轴，在3D坐标系中，RadiusA为x轴，RadiusB为Z轴，RadiusC为Y轴；

		Latitude：纬度；

		ItemMarginAngle：每个Item之间的夹角；

		SubItemMargin：每个Item的子元素间的间距；

		SubItemHeight：每个Item的子元素间的高度；

		SubItemWidth：每个Item的子元素间的宽度；

		ShowRow：3DWall的展示行数；

		ShowColumn：3DWall的展示列数；

### 节点Animation

	属性说明

	DefaultMoveInterval：放大SubItem的动画时间；

	ScaledMoveInterval：点击放大后的SubItem移动到中间的动画时间；

	ShrinkInterval：预留节点；

     

 

 

 

 

 

 

 

 

 

 

 

