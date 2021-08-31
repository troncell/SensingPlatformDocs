# 视频滑块控件（VideoBannerElement）

## 控件作用

多个视频左右滑动

## 控件UI效果
![Placeholder](../../images/VideoBannerElement.png)


## 配置文件样例
```
<VideoBannerElement Name="videoPlayer">
                <UIDisplay Left="114" Top="582" Width="861" Height="519" IsShow="True" ZIndex="1" UsePercent="False" />
                <DataProvider>VideoData?CSTable={$sheet}</DataProvider>
                <Items>
                    <Template Left="0" Top="0" Width="1169" Height="661" TemplateID="10001">
                        <VideoSource UriKind="Application">Shell\Pages\HomePage\resource\证券基础知识\衍生品\视频\{$weizhi}\{$video}</VideoSource>
                    </Template>
                </Items>
                <CustomerConfig></CustomerConfig>
            </VideoBannerElement>
```


<!-- ## 配置说明
1. 节点BgType: Type:是否配置背景，1为显示，0为不显示，然后配置背景图片所在的位置即可；

2. 节点Fold:配置资源文件夹所在的路径；

3. 节点 IsFoldBarVisible False 表示下方分类文件夹是否显示，False 表示不显示，True则表示显示。 -->


