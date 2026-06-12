# 长按按钮控件（LongPressButton）

## 1.控件作用

一般作为一张透明图片，长按按钮控件用于响应用户的长按操作。用户长按按钮一定时间（通常约 3 秒）后触发事件。控件支持配置序列帧动画，在长按时播放动画效果，动画结束时触发配置的 `ClickEvent`。

## 2.适用场景

- 需要防止误触的重要操作按钮
- 返回首页、退出等需要长按确认的功能
- 需要配合动画反馈的交互按钮
- 透明热区触发隐藏功能

## 3.前置依赖

使用长按按钮控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `LongPressButton`；
3. 准备好序列帧图片资源（如需要长按动画效果）。

## 4.控件 UI 效果

![Placeholder](../images/LongPressButton.gif)

## 5.配置文件样例

```xml

<LongPressButton>
    <UIDisplay Left="0" Top="0" Width="300" Height="300" IsShow="True" ZIndex="4" UsePercent="False" Opacity="1"/>
     <!--PathSource：序列帧动画资源路径
        UriKind: 路径类型
        Interval: 帧切换间隔，单位毫秒
    -->
    <PathSource UriKind="Project" Interval="20">Pages\HomePage\resource\圈\分离</PathSource>
    <ClickEvent>Navigate?Page=HomePage</ClickEvent>
</LongPressButton>
```

## 6.PathSource 参数说明

| 属性       | 必填 | 说明                   | 示例      |
| ---------- | ---- | ---------------------- | --------- |
| `UriKind`  | 是   | 序列帧图片路径解析方式 | `Project` |
| `Interval` | 否   | 帧切换间隔，单位毫秒   | `20`      |

### 6.1UriKind 说明

| 取值          | 路径基准              | 示例                                    |
| ------------- | --------------------- | --------------------------------------- |
| `Application` | 应用根目录            | `Shell\Pages\HomePage\resource\圈\分离` |
| `Project`     | `Shell` 文件夹        | `Pages\HomePage\resource\圈\分离`       |
| `Relative`    | 当前 XML 文件所在目录 | `resource\圈\分离`                      |
| `Absolute`    | 绝对路径              | `C:\Resources\圈\分离`                  |

### 6.2序列帧要求

- 序列帧图片应按播放顺序命名，如 `0001.png`、`0002.png` 等；
- 所有序列帧图片应放在同一文件夹中；
- 建议使用 PNG 格式以支持透明背景。

## 7.ClickEvent 说明

`ClickEvent` 在用户长按达到指定时间后触发。如果配置了序列帧动画，通常在动画播放完成后触发事件。

```xml
<ClickEvent>Navigate?Page=HomePage</ClickEvent>
```

### 触发时机

- 用户按下按钮并保持不移动；
- 达到长按时间阈值（通常约 3 秒，具体以控件实现为准）；
- 如果配置了序列帧动画，动画播放完成后触发 `ClickEvent`；
- 如果用户在达到阈值前松开或移动超出阈值，则不触发事件。

## 8.CustomerConfig 参数说明

部分版本的长按按钮控件可能支持以下配置：

| 参数              | 说明                         | 示例    |
| ----------------- | ---------------------------- | ------- |
| `LongPressTime`   | 长按触发时间，单位毫秒       | `3000`  |
| `MobileThreshold` | 移动距离阈值，超过则取消长按 | `20`    |
| `Loop`            | 序列帧是否循环播放           | `False` |

> 以上参数以实际版本为准。

## 9.UIControlDict.xml 添加长按按钮控件

如果使用长按按钮控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<Element ViewType="LongPressButton" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.LongPressButton, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.LongPressButtonViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 10.部署说明

1. 确认项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 准备序列帧图片资源（如需要动画效果）；
4. 在页面 XML 中使用 `LongPressButton`，配置 `UIDisplay`、`PathSource` 和 `ClickEvent`。

## 11.常见问题

### 长按按钮不触发事件

- 检查是否按够了触发时间（通常约 3 秒）；
- 检查 `ClickEvent` 是否配置正确；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查手指或鼠标是否在按下时移动过大导致取消长按。

### 序列帧动画不播放

- 检查 `PathSource` 的路径和 `UriKind` 是否正确；
- 检查文件夹中是否存在序列帧图片；
- 检查 `Interval` 是否设置合理。

### 按钮不可见

- 如果不配置 `PathSource`，按钮为透明热区，可能看不到但可响应长按；
- 检查 `Opacity` 是否设置过低；
- 检查 `ZIndex` 是否被其他控件遮挡。

### 动画播放完成但事件未触发

- 检查 `ClickEvent` 是否正确配置；
- 检查事件 URL 中的特殊字符是否已转义；
- 检查是否有异常导致事件处理中断。

### 长按过程中断

- 检查是否设置了 `MobileThreshold`，手指移动超过阈值会取消长按；
- 检查是否有上层控件拦截了触摸事件。

## 12.注意事项

- 长按按钮适合需要防止误触的场景，但长按时间不宜过长，以免影响用户体验；
- 透明按钮作为热区时，建议在实际设备上测试长按响应区域；
- 序列帧动画文件建议控制大小，避免影响加载和播放性能；
- 不同版本的长按按钮触发时间和配置参数可能不同。
