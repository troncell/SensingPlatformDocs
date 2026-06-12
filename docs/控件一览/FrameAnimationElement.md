# 帧动画控件（FrameAnimationElement）

## 1.控件作用

帧动画控件以序列帧的方式播放动画。它支持 PNG 透明图片的动画播放，适合小尺寸动画效果。对于大图片序列帧，可能会对性能产生影响，建议谨慎使用或采用视频控件替代。

## 2.适用场景

- 需要播放透明背景动画的效果
- 小尺寸循环动画，如粒子、光效、角色动作等
- 不支持视频格式但需要动态展示的场景
- 由设计师导出为序列帧图片的动画效果

## 3.前置依赖

使用帧动画控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `FrameAnimationElement`；
3. 准备好序列帧图片资源，建议按顺序命名并放在同一文件夹中。

## 4.控件 UI 效果

![输入图片说明](https://sensingstore.oss-cn-shanghai.aliyuncs.com/Troncell/SensingPlatfrom/FrameAnimation2.gif)

## 5.配置文件样例

```xml
<FrameAnimationElement>
      <UIDisplay Left="100" Top="100" Width="515" Height="292" IsShow="True" ZIndex="1" UsePercent="false" IsUseCache="True" />
      <!-- PathSource帧动画资源路径:
        UriKind: 资源路径类型，Application表示应用内路径，Absolute表示绝对路径，Relative表示相对路径，Project表示工程路径
        Filter: 资源过滤器，支持多个格式，用逗号分隔
      -->
      <PathSource UriKind="Application" Filter="*.png,*.jpg,*.bmp">Shell\Pages\StarPWallPage\仙鹤序列帧</PathSource>
      <CustomerConfig>
        <!-- 帧的Image控制展示:
          AutoHeight: 是否自适应高度
          Stretch: 图片拉伸方式，None表示不拉伸，Fill表示填充，Uniform表示等比例缩放，UniformToFill
           -->
        <Image AutoHeight="true" Stretch="None"/>
        <!-- Frame控制帧率:
          Interval: 帧率间隔，单位ms
          Repeat: 重复次数，Forever表示无限循环
          AutoPlay:是否加载后自动播放动画，默认是自动播放
           -->
        <Frame Interval="50" Repeat="1" AutoPlay="False" />
      </CustomerConfig>
    </FrameAnimationElement>
```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对帧动画控件：

- `Width` / `Height`：定义动画的显示区域大小；
- `IsUseCache`：建议设为 `True`，预加载序列帧可提升播放流畅度；
- `ZIndex`：注意动画与其他控件的层级关系；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`。

## 7.PathSource 参数说明

| 属性      | 必填 | 说明                               | 示例                |
| --------- | ---- | ---------------------------------- | ------------------- |
| `UriKind` | 是   | 资源路径类型                       | `Application`       |
| `Filter`  | 否   | 文件过滤器，支持多个格式用逗号分隔 | `*.png,*.jpg,*.bmp` |

### 7.1UriKind 说明

| 取值          | 路径基准              | 示例                                   |
| ------------- | --------------------- | -------------------------------------- |
| `Application` | 应用根目录            | `Shell\Pages\StarPWallPage\仙鹤序列帧` |
| `Absolute`    | 绝对路径              | `C:\Animations\仙鹤序列帧`             |
| `Relative`    | 当前 XML 文件所在目录 | `仙鹤序列帧`                           |
| `Project`     | `Shell` 文件夹        | `Pages\StarPWallPage\仙鹤序列帧`       |

### 7.2Filter 说明

`Filter` 用于过滤文件夹中需要播放的图片。例如 `*.png` 只播放 PNG 图片，`*.png,*.jpg` 播放 PNG 和 JPG 图片。

## 8.CustomerConfig 参数说明

### 8.1Image 节点

| 属性         | 必填 | 说明                   | 示例   |
| ------------ | ---- | ---------------------- | ------ |
| `AutoHeight` | 否   | 是否根据图片自适应高度 | `true` |
| `Stretch`    | 否   | 图片拉伸方式           | `None` |

### 8.2Stretch 取值说明

| 取值            | 说明                         |
| --------------- | ---------------------------- |
| `None`          | 不拉伸，按图片原始尺寸显示   |
| `Fill`          | 填充整个显示区域，可能变形   |
| `Uniform`       | 等比例缩放，保持完整显示     |
| `UniformToFill` | 等比例填充，可能裁剪部分内容 |

### 8.3Frame 节点

| 属性       | 必填 | 说明                                               | 示例           |
| ---------- | ---- | -------------------------------------------------- | -------------- |
| `Interval` | 否   | 每帧切换间隔，单位毫秒                             | `50`           |
| `Repeat`   | 否   | 重复次数，`Forever` 表示无限循环，整数表示具体次数 | `1`、`Forever` |
| `AutoPlay` | 否   | 加载后是否自动播放，默认 `True`                    | `False`        |

### 8.4属性说明

- **Interval**：帧与帧之间的时间间隔。数值越小动画越快，数值越大动画越慢。
- **Repeat**：动画播放次数。`Forever` 表示循环播放，整数表示播放指定次数后停止。
- **AutoPlay**：控件加载后是否立即播放动画。设为 `False` 时，需要通过 `Control` 事件手动触发播放。

## 9.支持的事件

帧动画控件支持 `Control` 事件，用于控制动画的播放、暂停和停止。

### 9.1事件格式

```xml
<ClickEvent>Control?Action=Play</ClickEvent>
```

### 9.2Action 取值

| 取值    | 说明     |
| ------- | -------- |
| `Play`  | 播放动画 |
| `Pause` | 暂停动画 |
| `Stop`  | 停止动画 |

### 9.3示例

```xml
<ImageButton>
    <UIDisplay Left="0" Top="0" Width="100" Height="100" IsShow="True" ZIndex="2" />
    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\play.png</ImageSource>
    <ClickEvent>Control?Action=Play</ClickEvent>
</ImageButton>
```

## 10.UIControlDict.xml 添加帧动画控件

如果使用帧动画控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<!--UI.Common 控件包-->
<Element ViewType="FrameAnimationElement" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.FrameAnimationControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.FrameAnimationElementViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
<!--UI.Common End-->
```

## 11.部署说明

1. 确认项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 将序列帧图片按顺序命名并放入同一文件夹；
4. 在页面 XML 中使用 `FrameAnimationElement`，配置 `UIDisplay`、`PathSource` 和 `CustomerConfig`；
5. 如需手动控制，添加触发 `Control` 事件的按钮。

## 12.常见问题

### 动画不显示

- 检查 `PathSource` 的路径和 `UriKind` 是否正确；
- 检查文件夹中是否存在匹配 `Filter` 的图片文件；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`。

### 动画不播放

- 检查 `Frame` 的 `AutoPlay` 是否为 `True`；
- 检查 `Repeat` 是否设置正确；
- 检查是否通过 `Control` 事件正确触发了播放。

### 动画播放卡顿

- 减小序列帧图片的尺寸和数量；
- 将 `IsUseCache` 设为 `True` 以预加载资源；
- 考虑使用视频控件替代大图片序列帧。

### 图片顺序不对

- 确保序列帧图片按播放顺序命名，如 `0001.png`、`0002.png`、...；
- 检查 `Filter` 是否正确过滤了不需要的文件。

### 透明效果异常

- 确保使用支持透明的图片格式，如 PNG；
- 检查 `Stretch` 设置是否导致透明区域显示异常。

## 注意事项

- 帧动画控件适合小尺寸、短时长动画；
- 大量大图片序列帧会占用较多内存并影响性能；
- 建议将序列帧图片尺寸控制在合理范围内；
- 长时间循环播放的动画建议使用视频控件替代。
