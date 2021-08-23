# 滚动条控件（ScrollViewerElement）

## 控件作用

滚动条控件主要作用就是将无法在一页中全部显示的图片或者文字用滚动条的作用向下滚动翻看。

## 控件UI效果

![Placeholder](../../images/ScrollViewerElement.png)

## 配置文件样例

```
<ScrollViewerElement>
    <UIDisplay Left="500" Top="600" Width="200" Height="400" IsShow="True" ZIndex="10" UsePercent="False" />
    <XYContainerElement>
        <UIDisplay Left="0" Top="0" Width="800" Height="500" />
        <Controls>
            <ImageElement>
                <UIDisplay Left="-20" Top="10" Width="965" Height="667" IsShow="True" ZIndex="2" UsePercent="False" />
                <ImageSource UriKind="Application">Shell\Pages\IntroPage\Items\Item1\resource\公司简介.png</ImageSource>
            </ImageElement>
        </Controls>
    </XYContainerElement>
    <CustomerConfig>
        <ThumbImage UriKind="Application" Width="33" Height="38">Shell\Pages\HomePage\resource\thumb.png</ThumbImage>
        <!-- thumb.png为滚动条上面的可拖动的图标，可根据具体的设计来更改 ></CustomerConfig></ScrollViewerElement>
```
## 配置说明

### 节点ThumbImage

        thumb.png为滚动条上面的可拖动的图标，可根据具体的设计来更改。

