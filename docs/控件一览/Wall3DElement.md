# 3D 凹面墙控件（Wall3DElement）

## 控件作用

3D 凹面墙主要将图片或视视频以 3D 的形式进行展示。

## 控件 UI 效果

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
             <!--摄像机默认设置-->
                <Default>
                 <!--摄像机的视野-->
                    <FieldView>90</FieldView>
                     <!--摄像机的位置-->
                    <Position>
                        <X>0</X>
                        <Y>0</Y>
                        <Z>4.6</Z>
                    </Position>
                       <!--摄像机的朝向-->
                    <LookDirection>
                        <X>0</X>
                        <Y>0</Y>
                        <Z>-1</Z>
                    </LookDirection>
                     <!--摄像机绕X轴旋转的角度-->
                    <XAxisAngle>0</XAxisAngle>
                </Default>
                 <!--点击放大,拉近摄像机时摄像机的属性-->
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
                 <!--当3dWall变成一个圆筒时摄像机的属性-->
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
                         <!--当3dWall变成一个圆筒时 摄像机会被拉远，Z轴最大为8.6-->
                        <Z>-1</Z>
                    </LookDirection>
                    <!--摄像机绕X轴的最大角度 旋转80度后就不能继续旋转了-->
                    <XAxisAngle>80</XAxisAngle>
                </FullView>
            </Camera>
            <Model3D>
             <!--RadiusA,RadiusB,RadiusC 椭球的3个轴。在3D坐标系中 RadiusA:x轴 ，RadiusB:Z轴 ，RadiusC:y轴-->
                <RadiusA>4.8</RadiusA>
                <RadiusB>5</RadiusB>
                <RadiusC>5</RadiusC>
                 <!--纬度-->
                <Latitude>25</Latitude>
                     <!--每个Item之间的夹角-->
                <ItemMarginAngle>2</ItemMarginAngle>
                        <!--每个Item的子元素间的间距-->
                <SubItemMargin>2</SubItemMargin>
                  <!--每个Item的子元素的高度-->
                <SubItemHeight>540</SubItemHeight>
                 <!--每个Item的子元素的宽度-->
                <SubItemWidth>420</SubItemWidth>
                    <!--3DWall 展示的行数-->
                <ShowRow>3</ShowRow>
                <!--3DWall 展示的列数-->
                <ShowColumn>15</ShowColumn>
                <HasMirror>True</HasMirror>
            </Model3D>
        </Scenario3D>
        <Animation>
          <!--放大SubItem的动画时间-->
            <DefaultMoveInterval>2000</DefaultMoveInterval>
             <!--点击放大后的SubItem，SubItem移动到中间的动画时间-->
            <ScaledMoveInterval>500</ScaledMoveInterval>
              <!--预留节点-->
            <ShrinkInterval>2000</ShrinkInterval>
        </Animation>
        <!--图片资源-->
        <Source RootPath="Wall3D">
            <Extension>*.jpg</Extension>
        </Source>
    </CustomerConfig>
</Wall3DElement>

```

## 配置说明

### 节点 Default

    摄像机默认设置。

### 节点 FieldView

    摄像机默认视野。

### 节点 Position

    摄像机的位置。

### 节点 LookDirection

    摄像机的朝向。

### 节点 XAxisAngle

    摄像机绕X轴旋转的角度。

### 节点 Scaled

    点击放大，拉近摄像机时摄像机的属性。

### 节点 FullView

    当3DWall变成一个圆筒时摄像机的属性。

### 节点 XAxisAngle

    摄像机绕X轴的最大角度，旋转80度后就不能继续旋转了。

### 节点 Model3D

    属性说明

    	RadiusA、RadiusB、RadiusC：椭球的三个轴，在3D坐标系中，RadiusA为x轴，RadiusB为Z轴，RadiusC为Y轴；

    	Latitude：纬度；

    	ItemMarginAngle：每个Item之间的夹角；

    	SubItemMargin：每个Item的子元素间的间距；

    	SubItemHeight：每个Item的子元素间的高度；

    	SubItemWidth：每个Item的子元素间的宽度；

    	ShowRow：3DWall的展示行数；

    	ShowColumn：3DWall的展示列数；

        HasMirror：3DWall的展示的图片的镜像倒影，True为有镜像，False为没有镜像；

### 节点 Animation

    属性说明

    DefaultMoveInterval：放大SubItem的动画时间；

    ScaledMoveInterval：点击放大后的SubItem移动到中间的动画时间；

    ShrinkInterval：预留节点；

# UIControlDict.xml 添加 3D 凹面墙控件

如果使用 3D 凹面墙控件则需要在 UIControlDict.xml 中添加 3D 凹面墙控件

```
 <!--UI.Wall3D 控件包-->
  <Element ViewType="Wall3DElement" AssemblyFile="UI.Wall3D.dll" TypeName="UI.Wall3D.Wall3DControl, UI.Wall3D, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.SweepPanel.dll" TypeName="UI.Wall3D.Wall3DControlViewModel, UI.Wall3D, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```
