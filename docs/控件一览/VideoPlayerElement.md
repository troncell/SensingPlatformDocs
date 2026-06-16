# 视频控件（VideoPlayerElement）

## 1.控件作用

视频控件用于在页面或弹出框中播放视频。支持自动/手动播放、单次/循环播放、播放控制栏（播放/暂停/停止/进度/音量/全屏）、视频结束事件以及通过数据绑定动态加载视频列表。

## 2.适用场景

- 页面内嵌视频播放
- 弹出框中的宣传视频
- 需要播放控制栏的交互式视频
- 视频列表随机播放

## 3.前置依赖

使用视频控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `VideoPlayerElement`。

## 4.控件 UI 效果

![Placeholder](../images/VideoPlayerElement.png)

## 5.配置文件样例

```xml

<VideoPlayerElement>
    <UIDisplay Left="43" Top="60" Width="780" Height="505" IsShow="True"  ZIndex="2" UsePercent="False"/>
    <!-- 视频播放结束事件 -->
    <FinishEvent>Navigate?Page=HomePage&Args=imageButton</FinishEvent>
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

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。

## 7.配置说明

### 7.1FinishEvent：视频结束事件， 不用可以不写

`FinishEvent` 为 `VideoPlayerElement` 的直接子节点，用于配置视频播放结束时触发的事件。可包含一个或多个 `Event` 子节点，也可直接写事件字符串。

```xml
<FinishEvent>Navigate?Page=HomePage&Args=imageButton</FinishEvent>
```

## 8.CustomerConfig 参数说明

### 8.1VideoPlayer 节点

| 属性       | 必填 | 类型                  | 默认值     | 说明                                                           |
| ---------- | ---- | --------------------- | ---------- | -------------------------------------------------------------- |
| `PlayMode` | 否   | `AutoPlay` / `Manual` | `AutoPlay` | 播放方式。`AutoPlay` 加载后自动播放，`Manual` 需手动点击播放。 |
| `LoopMode` | 否   | `One` / `Forever`     | `One`      | 循环模式。`One` 播放一次，`Forever` 循环播放。                 |
| `Volumn`   | 否   | `double`              | `0.5`      | 初始音量，取值范围 `0` ~ `1`。                                 |

### 8.2节点 Player:整段视频的一些属性

| 子节点        | 必填 | 说明                                                                               |
| ------------- | ---- | ---------------------------------------------------------------------------------- |
| `UIDisplay`   | 是   | 视频画面在控件中的位置与大小。                                                     |
| `VideoSource` | 是   | 默认播放的视频源。                                                                 |
| `VideoPath`   | 否   | 可选的多视频路径集合，内部包含多个 `FileSource` 节点，用于 `RandomPlay` 随机播放。 |

### 8.3Controller 节点

| 属性         | 必填 | 类型     | 默认值      | 说明           |
| ------------ | ---- | -------- | ----------- | -------------- |
| `Background` | 否   | `string` | `#55000000` | 控制栏背景色。 |

| 子节点             | 说明                                                                                          |
| ------------------ | --------------------------------------------------------------------------------------------- |
| `UIDisplay`        | 控制栏整体位置与大小。                                                                        |
| `PlayButton`       | 播放按钮，包含 `UIDisplay` 与 `ImageSource`。                                                 |
| `PauseButton`      | 暂停按钮，包含 `UIDisplay` 与 `ImageSource`。                                                 |
| `StopButton`       | 停止按钮，包含 `UIDisplay` 与 `ImageSource`。当前界面中默认隐藏（`Visibility="Collapsed"`）。 |
| `TimeText`         | 剩余时间文本，包含 `UIDisplay`。                                                              |
| `VolumeButton`     | 音量按钮，包含 `UIDisplay` 与 `ImageSource`。                                                 |
| `MuteButton`       | 静音按钮，包含 `ImageSource`。                                                                |
| `VolumeSlider`     | 音量滑块，包含 `UIDisplay`。                                                                  |
| `Slider`           | 播放进度条，包含 `UIDisplay`、`Thumb/ImageSource`，以及 `Fill`、`ProgressFill` 属性。         |
| `FullScreenButton` | 全屏按钮，包含 `UIDisplay` 与 `ImageSource`。                                                 |
| `NormalizeButton`  | 退出全屏按钮，包含 `ImageSource`。                                                            |

### 8.4Slider 节点

| 属性           | 必填 | 类型     | 默认值      | 说明             |
| -------------- | ---- | -------- | ----------- | ---------------- |
| `Fill`         | 否   | `string` | `#88000000` | 进度条背景色。   |
| `ProgressFill` | 否   | `string` | `White`     | 已播放进度颜色。 |

| 子节点              | 说明               |
| ------------------- | ------------------ |
| `UIDisplay`         | 进度条位置与大小。 |
| `Thumb/ImageSource` | 进度条滑块图片。   |

## 9.DataProvider 与 Items

视频控件支持通过 `DataProvider` 绑定数据源动态加载视频列表。数据源中的每一行会生成一个视频项，用于播放列表。

```xml
<DataProvider>VideoData?CSTable=Movies</DataProvider>
<Items>
    <Template Left="0" Top="0" Width="780" Height="505" TemplateID="video">
        <VideoSource UriKind="Application">Shell\Pages\Common\{$FileName}</VideoSource>
    </Template>
</Items>
```

## 10.可接受的事件

### 10.1Control 事件

外部可通过 `Control` 事件远程控制视频播放。

```xml
<ClickEvent>Control?TargetPageName=HomePage&TargetControlName=videoPlayer&Action=Play</ClickEvent>
```

| 参数                | 说明                                            | 示例          |
| ------------------- | ----------------------------------------------- | ------------- |
| `TargetPageName`    | 目标页面名称                                    | `HomePage`    |
| `TargetControlName` | 目标视频控件名称                                | `videoPlayer` |
| `Action`            | 操作类型：`Play`、`Pause`、`Stop`、`RandomPlay` | `Play`        |

### 10.2VideoSourceChanged 事件

通过 `VideoSourceChanged` 事件可动态切换当前播放的视频源。

```xml
<ClickEvent>VideoSourceChanged?TargetPageName=HomePage&TargetControlName=videoPlayer&Source=Shell\Pages\Common\new.wmv</ClickEvent>
```

## 11.UIControlDict.xml 添加视频控件

如果使用视频控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<Element ViewType="VideoPlayerElement" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.VideoPlayer, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.VideoPlayerViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 12.部署说明

1. 确认项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 准备视频文件与控制按钮图片资源；
4. 在页面 XML 中使用 `VideoPlayerElement`，配置 `UIDisplay`、`FinishEvent`、`CustomerConfig`；
5. 如需动态视频列表，配置 `DataProvider` 与 `Items/Template`。

## 13.常见问题

### 视频不播放

- 检查 `UIControlDict.xml` 中是否已注册 `VideoPlayerElement`；
- 检查 `VideoSource` 的 `UriKind` 和路径是否正确；
- 确认视频文件真实存在且格式受 WPF MediaElement 支持；
- 检查 `PlayMode` 是否为 `AutoPlay`，或手动点击播放按钮。

### 控制按钮不显示

- 检查对应按钮的 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查 `ImageSource` 的 `UriKind` 和路径是否正确；
- 检查 `ZIndex` 是否被其他控件遮挡。

### 进度条不更新

- 确认视频已正确加载（触发 `MediaOpened` 事件后 `_bufferingDone` 才为 `True`）；
- 检查 `Slider` 的 `UIDisplay` 是否配置正确；
- 检查 `Fill` 与 `ProgressFill` 颜色是否可见。

### 视频结束事件不触发

- 检查 `FinishEvent` 是否作为 `VideoPlayerElement` 的直接子节点配置；
- 检查 `LoopMode` 是否为 `One`（`Forever` 循环播放不会触发结束事件）；
- 确认事件 URL 中的 `&` 已转义为 `&amp;`。

## 14.注意事项

- 当前实现基于 WPF 原生 `MediaElement`，支持 `.wmv`、`.mp4` 等常见格式；
- `StopButton` 在界面中默认隐藏（`Visibility="Collapsed"`），配置后也不会显示；
- `LoopMode` 为 `Forever` 时视频播放结束后会自动从头播放，不会触发 `FinishEvent`；
- 全屏播放会新建一个 `VideoWindow` 窗口；
- 控件卸载或页面离开时会自动停止并关闭视频；
- 事件 URL 中的 `&` 必须转义为 `&amp;`。
