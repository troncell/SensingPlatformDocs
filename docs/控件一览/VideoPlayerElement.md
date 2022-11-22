# 视频控件（VideoPlayerElement）

## 控件作用

在页面或者弹出框中播放视频。

## 控件UI效果

![Placeholder](../../images/VideoPlayerElement.png)

## 配置文件样例

```xml

<VideoPlayerElement>
    <UIDisplay Left="43" Top="60" Width="780" Height="505" IsShow="True"  ZIndex="2" UsePercent="False"/>
    <!-- 视频播放结束事件 -->
    <FinishEvent>Navigate?Page=HomePage&amp;Args=imageButton</FinishEvent>
    <CustomerConfig>
        <!--PlayModel : AutoPlay,ManualPlay播放方式，手动OR自动。-->
        <!--LoopModel : One,Forever 播放次数-->
        <VideoPlayer PlayMode="AutoPlay" LoopMode="One">
            <Player>
                <!-- UIDisplay : 视频所要放置在控件中的位置-->
                <UIDisplay Left="0" Top="0" Width="780" Height="505" IsShow="True"  ZIndex="1" UsePercent="False"/>
                <!-- 视频文件放置的位置-->
                <VideoSource UriKind="Application">Shell\Pages\Common\test.wmv</VideoSource>
            </Player>
            <Controller>
                <!-- UIDisplay : 控制视频播放暂停功能块所放的位置-->
                <UIDisplay Left="0" Top="507" Width="700" Height="48" IsShow="True"  ZIndex="1" UsePercent="False"/>
                <PlayButton>
                    <!-- UIDisplay : 控制视频播放功能所放的位置-->
                    <UIDisplay Left="0" Top="0" Width="48" Height="48" IsShow="True"  ZIndex="1" UsePercent="False"/>
                    <!--控制视频播放功能图片所放的位置-->
                    <ImageSource UriKind="Application">Shell\Pages\icon-Play.png</ImageSource>
                </PlayButton>
                <PauseButton>
                    <!-- UIDisplay : 控制视频暂停功能所放的位置-->
                    <UIDisplay Left="0" Top="0" Width="48" Height="48" IsShow="True"  ZIndex="1" UsePercent="False"/>
                    <!--控制视频暂停功能图片所放的位置-->
                    <ImageSource UriKind="Application">Shell\Pages\icon-Pause.png</ImageSource>
                </PauseButton>
                <StopButton>
                    <!-- UIDisplay : 控制停止功能所放的位置-->
                    <UIDisplay Left="50" Top="0" Width="48" Height="48" IsShow="False"  ZIndex="1" UsePercent="False"/>
                    <!--控制视频停止功能图片所放的位置-->
                    <ImageSource UriKind="Application">Shell\Pages\icon-Stop.png</ImageSource>
                </StopButton>
                <Slider>
                    <!-- UIDisplay :视频播放进度条所在的区域-->
                    <UIDisplay Left="70" Top="15" Width="623" Height="16" IsShow="True"  ZIndex="1" UsePercent="False"/>
                    <Track>
                        <!-- UIDisplay :视频播放整进度条图片-->
                        <ImageSource UriKind="Application">Shell\Pages\SliderMid.png</ImageSource>
                    </Track>
                    <Thumb>
                        <!-- UIDisplay :视频进度点图片-->
                        <ImageSource UriKind="Application">Resource\SliderMid.png</ImageSource>
                    </Thumb>
                </Slider>
            </Controller>
        </VideoPlayer>
    </CustomerConfig>
</VideoPlayerElement>

```
## 配置说明

### FinishEvent
视频结束事件， 不用可以不写

### 节点VideoPlay

    播放属性

    属性说明

    PlayModel：播放方式，AutoPlay OR ManualPlay，手动OR自动；

    LoopModel：播放次数，One OR Forever，一次或者一直循环播放。

### 节点Player

    整段视频的一些属性

### 节点Controller

    除了视频本身，其他一些细小属性，如播放按钮，进度条，暂停按钮等

### PlayButton

    播放按钮的一些属性

### PauseButton

    暂停按钮的一些属性

### StopButton

    停止播放按钮的一些属性

### Slider

    整个进度条的一些属性

### Track

    进度条的属性

### Thumb

    进度条上面的进度点的属性
