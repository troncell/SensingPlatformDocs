# VideoBgElement

## 1.控件说明

循环播放视频控件用于在页面背景或指定区域循环播放单个视频文件。基于 Unosquare.FFME（ffme.win）实现，解决了 WPF 原生 `MediaElement` 播放视频时可能出现的闪烁问题，常用于背景动画、氛围视频等场景。

## 2.适用场景

- 页面背景循环视频
- 展厅氛围动画
- 需要稳定、无闪烁循环播放的视频展示

## 3.前置依赖

使用循环播放视频控件前，必须满足以下条件：

1. 项目目录中存在 `UI.VideoBg.dll` 及 `ffme.win.dll`；
2. 程序可访问 FFmpeg 原生库（默认位于 `Common\ffmpeg\`，或通过配置指定路径）；
3. 在 `SysConfig/UIControlDict.xml` 中注册 `VideoBgElement`。

### 3.1FFmpeg 运行时配置

采用了 ffpmeg 组件的界面能力，先确保程序的根目录下的 ffpmeg 下有相应的文件，，解决了 WPF 本身 VideoPlayer 的过度闪烁的问题，一般作为背景的动画使用

> [!WARNING]
> 确保主程序的配置文件启用了ffpmeg能力，在TronSensingShow.dll.config种修改， IsUseFFmpeg的值为True

```xml
  <appSettings>
    <add key="ProjectFolder" value="Shell"/>
    <add key="IsUseWebView" value="True"/>
    <add key="IsUseFFmpeg" value ="True"/>
    <add key="FFmpegFolder" value="C:\\ffmpeg"/>
    <add key="ProductName" value="SensingPlatform Main"/>
    <add key="ProjectName" value="SensingPlatform Main"/>
    <add key="SensingSiteUrl" value="http://58.214.31.206:2015/api/"/>
  </appSettings>
```

- `IsUseFFmpeg`：是否启用 FFmpeg；
- `FFmpegFolder`：FFmpeg 原生库所在目录，需包含 `avcodec`、`avformat`、`avutil` 等依赖。

## 4.控件 UI 效果

![Placeholder](../images/PerspectiveWallElement.gif)

## 5.配置文件样例

页面的配置范例如下

```xml
<VideoBgElement Name="bgVideo">
    <UIDisplay Left="900" Top="0" Width="960" Height="540" IsShow="True" ZIndex="1" UsePercent="False" />
    <!-- 视频文件的地址，跟ImageSource的配置一样，
    UriKind：视频文件的跟目录类型，是居于Application的，还是居于Project项目的文件夹，或者是Absolute的绝对目录
    里面的值为具体的视频文件，确保视频文件是存在的
    -->
    <VideoSource UriKind="Application">Shell\Pages\HomePage\Resources\report-bg.mp4</VideoSource>
      <CustomerConfig>
        <VideoRender Type="EVR" IsDeeperColor="False" IsLoop="True" />
    </CustomerConfig>
</VideoBgElement>
```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)

## 7.配置讲解

整个配置分为两个大类，一个是视频源的配置，一个是 VideoRender 的配置。

### 7.1视频源的配置

1. 和 ImageElement 中的 ImageSource 一样，可以配置绝对路径，Application 路径或者相对控件的目录

## 8.VideoSource 参数说明

`VideoSource` 为直接子节点，用于指定要播放的视频文件路径。

| 属性      | 必填 | 类型     | 默认值     | 说明               |
| --------- | ---- | -------- | ---------- | ------------------ |
| `UriKind` | 否   | `string` | `Relative` | 视频路径解析方式。 |
| 节点值    | 是   | `string` | —          | 视频文件路径。     |

### 8.1UriKind 说明

| 取值          | 路径基准                     | 示例                                           |
| ------------- | ---------------------------- | ---------------------------------------------- |
| `Relative`    | 当前 XML 文件所在目录        | `report-bg.mp4`                                |
| `Application` | 应用根目录                   | `Shell\Pages\HomePage\Resources\report-bg.mp4` |
| `Project`     | `Shell` 文件夹               | `Pages\HomePage\Resources\report-bg.mp4`       |
| `Absolute`    | 物理磁盘绝对路径             | `C:\Videos\report-bg.mp4`                      |
| `Web`         | 网络地址，会先映射到本地缓存 | `http://example.com/video.mp4`                 |
| `AppPod`      | 应用数据目录                 | —                                              |

## 9.CustomerConfig 参数说明

### 9.1VideoRender 节点

`CustomerConfig` 内可选配置 `VideoRender` 节点，用于控制视频渲染与循环行为。

| 属性            | 必填 | 类型     | 默认值  | 说明                                                    |
| --------------- | ---- | -------- | ------- | ------------------------------------------------------- |
| `Type`          | 否   | `string` | `EVR`   | 视频渲染器类型，当前代码中已解析但未实际影响渲染。      |
| `IsDeeperColor` | 否   | `bool`   | `False` | 是否启用深色彩，当前代码中已解析但未实际使用。          |
| `IsLoop`        | 否   | `bool`   | `True`  | 是否循环播放。`True` 循环播放，`False` 播放一次后暂停。 |

## 10.UIControlDict.xml 添加循环播放视频控件

如果使用循环播放视频控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<Element ViewType="VideoBgElement" AssemblyFile="UI.VideoBg.dll" TypeName="UI.VideoBg.VideoBgControl, UI.VideoBg, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.VideoBg.dll" TypeName="UI.VideoBg.VideoBgControlViewModel, UI.VideoBg, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 11.部署说明

1. 确认项目目录中存在 `UI.VideoBg.dll` 与 `ffme.win.dll`；
2. 确认 FFmpeg 原生库可访问（默认 `Common\ffmpeg\` 或通过 `FFmpegFolder` 配置）；
3. 在 `TronSensingShow.dll.config` 中设置 `IsUseFFmpeg=True` 并配置 `FFmpegFolder`；
4. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
5. 准备视频文件；
6. 在页面 XML 中使用 `VideoBgElement`，配置 `UIDisplay`、`VideoSource` 与可选的 `CustomerConfig`。

## 12常见问题

### 视频不播放

- 检查 `UI.VideoBg.dll` 与 `ffme.win.dll` 是否存在于应用根目录；
- 检查 FFmpeg 原生库是否完整且路径正确；
- 检查 `TronSensingShow.dll.config` 中 `IsUseFFmpeg` 是否为 `True`；
- 检查 `VideoSource` 的 `UriKind` 和路径是否正确；
- 确认视频文件真实存在且格式受支持。

### 视频闪烁或花屏

- 确认已启用 FFmpeg（`IsUseFFmpeg=True`）；
- 检查 FFmpeg 版本与 `ffme.win.dll` 是否匹配；
- 尝试调整 `VideoRender` 的 `Type` 或 `IsDeeperColor`（当前版本保留字段）。

### 视频无法循环

- 检查 `CustomerConfig/VideoRender` 的 `IsLoop` 是否为 `True`；
- 检查视频文件是否完整，损坏的视频可能导致播放结束后无法重播。

### 视频遮挡其他控件点击

- 循环播放视频控件默认 `IsHitTestVisible="False"`，不会拦截触摸/鼠标事件；
- 如果仍被遮挡，检查 `ZIndex` 配置是否合理。

## 13.注意事项

- 当前实现基于 Unosquare.FFME（ffme.win），运行时需要 FFmpeg 原生库；
- `VideoRender` 节点中的 `Type` 与 `IsDeeperColor` 已在 ViewModel 中解析，但当前控件初始化时未实际使用；
- 控件默认循环播放（`IsLoop=True`）；
- 控件卸载或页面停止时会自动停止并关闭视频，释放资源；
- 事件 URL 中的 `&` 必须转义为 `&amp;`。
