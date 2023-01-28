# 滑块控件（SequenceItemsElement）

## 控件作用

滑块控件以滑块的方式展示图片的列表,支持水平和垂直的布局!

## 控件UI效果

![Placeholder](../images/SequenceItemsElement.png)

## 配置文件样例

```xml
<SequenceItemsElement>
    <UIDisplay Left="500" Top="800" Width="920" Height="100" IsShow="True"  ZIndex="6" UsePercent="False"/>
    <DataProvider>SequenceData?CSTable=Sequence</DataProvider>
    <Items>
        <Template>
            <ImageButton>
                <UIDisplay Left="0" Top="0" Width="90" Height="90" IsShow="True"  ZIndex="3" UsePercent="False"/>
                <ImageSource UriKind="Application">Shell\Pages\{$PhotoName}</ImageSource>
                <ClickEvent>PopupEvent?TargetPageName=VideoPage&amp;X=0&amp;Y=0&amp;Height=1080&amp;Width=1920&amp;EventID=Animal-1&amp;UriKind=Application&amp;EventPath=Shell\Pages\Innovate</ClickEvent>
            </ImageButton>
        </Template>
    </Items>
    <CustomerConfig>
        <LayoutManager LayoutType="HorizontalListLayout" Margin="0" Align="Left" />
        <Data DataName="SequenceData" ListDataName="Sequence" Cycle="False" />
        <SequenceConfig IsCacheUI="True" IsCombineTemplate="False" IsAutoSweep="False" SweepInterval="15" MaxEllapsedTime="2000" SweepDelta.X="0" SweepDelta.Y="0" />
    </CustomerConfig>
</SequenceItemsElement>

```
```xml
<SequenceItemsElement>
    <UIDisplay Left="0" Top="250" Width="1920" Height="476" IsShow="True"  ZIndex="6" UsePercent="False"/>
    <Items>
        <Item>
            <ImageButton>
                <UIDisplay Left="0" Top="0" Width="286" Height="476" IsShow="True"  ZIndex="3" UsePercent="False"/>
                <ImageSource UriKind="Application">Shell\Pages\VideoPage\CardIcon\AIRTRAIN.png</ImageSource>
                <ClickEvent>PopupEvent?TargetPageName=VideoPage&amp;X=0&amp;Y=0&amp;Height=1080&amp;Width=1920&amp;EventID=Animal-1&amp;UriKind=Application&amp;EventPath=Shell\Pages\ Innovate</ClickEvent>
            </ImageButton>
        </Item>
        <Item Left="0" Top="0" Width="261" Height="476"  >
            <ImageButton>
                <UIDisplay Left="0" Top="0" Width="261" Height="476" IsShow="True"  ZIndex="3" UsePercent="False"/>
                <ImageSource UriKind="Application">Shell\Pages\VideoPage\CardIcon\LAS.png</ImageSource>
                <ClickEvent>PopupEvent?TargetPageName=VideoPage&amp;X=0&amp;Y=0&amp;Height=1080&amp;Width=1920&amp;EventID=Animal-1&amp;UriKind=Application&amp;EventPath=Shell\Pages\Innovate</ClickEvent>
            </ImageButton>
        </Items>
        <CustomerConfig>
            <LayoutManager LayoutType="HorizontalListLayout" Margin="0" Align="Left" />
            <SequenceConfig IsCacheUI="True" IsCombineTemplate="False" IsAutoSweep="False" SweepInterval="15" MaxEllapsedTime="2000" SweepDelta.X="0" SweepDelta.Y="0" />
        </CustomerConfig>
    </SequenceItemsElement>

```
## 配置说明

### 节点LayoutManager

    属性说明
        LayoutType：滑块方向
            水平单一滑动：HorizontalCardLayout；
            垂直单一滑动：VerticalCardLayout；
            水平滑动：HorizontalListLayout；
            垂直滑动：VerticalListLayout；
            环形滑块：CircleListLayout；
            缩放模块：GraphicLayout
                这是一种较为特殊的方式，在Item里面控制缩放的大小边界，若要控制缩放图的大小，则CanScale必须为"True"，
                然后通过MaxScale及MinScale控制缩放的大小边界，
                ScaleMode为碰到边缘时的反应，
                Normal就是正常的情况，
                Bounce就是超出最小和最大值范围后，手松开后会自动弹回来，
                Disppear就是超出最小值，直接关闭

        Margin：相邻卡片间的间距，单位为：像素；    
        Align：对齐方式：Left/Center/Right；
        Row: 显示几行，在水平布局的时候有效;
        Column: 显示几列，在垂直布局的时候有效;

        $${\color{red}在Type为CircleListLayout的时候有一下几个参数可额外进行配置，在此用例的时候，推荐使用CircleElement进行配置}$$

        Radius:环绕到中心点的半径；
        Center.X/Center.Y: 环绕的中心点位置
        SpeedRatio: 环绕的速率

### 节点Data
    此节点的数据值必须与DataProvider的保持一致，第一个参数为数据源的名称，第二个参数为Table的名称!
    属性说明

        DataName：与此控件相连的数据库的名字；

        ListDataName：运用到的数据库中表的名字；

        Cycle：是否循环显示。

### 节点SequenceConfig

    属性说明

        IsCacheUI：是否预加载，值为True/False；

        IsAutoSweep：是否自动默认循环滑动，值为True/False；

        SweepInterval：多久移动一次，单位为毫秒，为自动滑动使用；

        MaxEllapsedTime：为进入自动滑动的时间，单位为毫秒(场景如下，一段时间无人操作后，进入自动滑动模式)；

        SweepDelta.X：左右移动的距离，单位为像素，负数为向左.
        SweepDelta.Y：上下移动的距离，单位为像素，负数为向右.
