# 视频滑块控件（VideoBannerElement）


## 控件作用

多个视频左右滑动，支持按钮触发左右滑动

## 控件UI效果
![Placeholder](../../images/VideoBannerElement.png)

![Placeholder](../../images/VideoBannerElement_number_index.png)

## 配置文件样例

```
<!--点点示例-->
<VideoBannerElement Name="videoPlayer">
    <UIDisplay Left="114" Top="582" Width="861" Height="519" IsShow="True" ZIndex="1" UsePercent="False" />
    <DataProvider>VideoData?CSTable={$sheet}</DataProvider>
    <Items>
        <Template Left="0" Top="0" Width="1169" Height="661" TemplateID="10001">
            <VideoSource UriKind="Application">Shell\Pages\HomePage\resource\证券基础知识\衍生品\视频\{$weizhi}\{$video}</VideoSource>
        </Template>
    </Items>
    <CustomerConfig>
        <PagerIndex VerticalAlignment="Bottom" Offset="-100" PageIndexColor="Gray" PageIndexSelectedColor="RED" />
    </CustomerConfig>
</VideoBannerElement>
```

```
<!--数字示例-->
<VideoBannerElement Name="videoPlayer">
    <UIDisplay Left="114" Top="582" Width="861" Height="519" IsShow="True" ZIndex="1" UsePercent="False" />
    <DataProvider>VideoData?CSTable={$sheet}</DataProvider>
    <Items>
        <Template Left="0" Top="0" Width="1169" Height="661" TemplateID="10001">
            <VideoSource UriKind="Application">Shell\Pages\HomePage\resource\证券基础知识\衍生品\视频\{$weizhi}\{$video}</VideoSource>
        </Template>
    </Items>
    <CustomerConfig>
        <NumberIndex VerticalAlignment="Bottom" Offset="-100">
            <XYContainerElement>
                <UIDisplay Left="0" Top="0" Width="800" Height="50" IsShow="True" ZIndex="1" UsePercent="False" />
                <Controls>
                    <TextElement Name="CURRENT_INDEX_TEXT">
                        <UIDisplay Left="280" Top="0" Width="100" Height="50" IsShow="True" ZIndex="2" UsePercent="False" />
                        <TextSource ForegroundColor="#324cc2" Family="黑体" Size="40" CultureInfo="zh-CN" Alignment="Right">1</TextSource>
                    </TextElement>
                    <TextElement Name="SPLIT">
                        <UIDisplay Left="385" Top="0" Width="30" Height="50" IsShow="True" ZIndex="2" UsePercent="False" />
                        <TextSource ForegroundColor="#324cc2" Family="黑体" Size="40" CultureInfo="zh-CN" Alignment="Center">/</TextSource>
                    </TextElement>
                    <TextElement Name="TOTAL_PAGE_TEXT">
                        <UIDisplay Left="420" Top="0" Width="100" Height="50" IsShow="True" ZIndex="2" UsePercent="False" />
                        <TextSource ForegroundColor="#324cc2" Family="黑体" Size="40" CultureInfo="zh-CN" Alignment="Left">100</TextSource>
                    </TextElement>
                </Controls>
            </XYContainerElement>
        </NumberIndex> -
    </CustomerConfig>
</VideoBannerElement>
```

## 按钮触发滑动
```
<!--上一页-->
<ImageButton>
    <UIDisplay Left="0" Top="0" Width="512" Height="512" IsShow="True" ZIndex="1" UsePercent="False" />
    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\last_btn.jpg</ImageSource>
    <ClickEvent>IndexChanged?TargetPageName=HomePage&amp;TargetControlName=videoBanner&amp;IndexString=Pre&amp;Index=-1</ClickEvent>
</ImageButton>
<!--下一页-->
<ImageButton>
    <UIDisplay Left="500" Top="0" Width="512" Height="512" IsShow="True" ZIndex="1" UsePercent="False" />
    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\next_btn.jpg</ImageSource>
    <ClickEvent>IndexChanged?TargetPageName=HomePage&amp;TargetControlName=videoBanner&amp;IndexString=Next&amp;Index=-1</ClickEvent>
</ImageButton>
```


## 配置说明
可以设置两种页码控件，其它NumberIndex可以包含一个XYContainerElement包含元素控件。

### PagerIndex参数说明
1. VerticalAlignment="Bottom" 垂直位置(Top | Center | Bottom)
2. Offset="-100"  垂直偏移
3. PageIndexColor="Gray" 点点颜色
4. PageIndexSelectedColor="RED" 点点选中颜色

### NumberIndex说明
1. VerticalAlignment="Bottom" 垂直位置(Top | Center | Bottom)
2. Offset="-100"  垂直偏移




