# Controls Reference

Every control must be registered in `SysConfig/UIControlDict.xml` before use. Below is the catalog of known controls.

## Legend

- **GroupView** = `True` if the control acts as a container with `<Items>` or `<Controls>` children.
- **Assembly** = the DLL that hosts the control implementation. Most are in `UI.Common.dll` unless noted.
- **Docs** = whether the control has a dedicated `.md` file in the docs site (rich vs stub-level).

## Control catalog

| ViewType | Chinese name | Assembly | GroupView | Docs |
|---|---|---|---|---|
| `AlbumElement` | 飞图控件 | `UI.Common.dll` | Yes | Rich |
| `ImageElement` | 图片控件 | `UI.Common.dll` | No | Rich | ImageSource, UriKind — #1 cause of missing assets |
| `ImageButton` | 图片按钮控件 | `UI.Common.dll` | No | Rich | ImageSource, ClickEvent, UriKind critical |
| `TextElement` | 文字控件 | `UI.Common.dll` | No | Rich |
| `VideoPlayerElement` | 视频控件 | `UI.Common.dll` | Yes | Rich |
| `FlipViewElement` | 卡片型滑块控件 | `UI.FlipView.dll` | Yes | Rich |
| `Wall3DElement` | 3D凹面墙控件 | `UI.Wall3D.dll` | Yes | Rich |
| `PopupShowElement` | 弹出框控件 | `UI.SweepPanel.dll` | Yes | Rich |
| `WebBrowserElement` | 浏览器控件 | `UI.SensingWebBrowser.dll` | No | Rich | Edge (WebView2) / Chrome (CEF); JS↔WPF two-way bridge |
| `XYContainerElement` | 相对布局控件 | `UI.Common.dll` | Yes | Rich | Groups child controls via `<Controls>`; children move/scale as a unit |
| `CustomerElement` | 自定义控件 | `UI.Common.dll` | Yes | Rich | Host custom .NET 10 WPF controls; drop DLL into app folder |
| `ScrollViewElement` | 滚动条控件 | `UI.Common.dll` | Yes | Rich |
| `BubbleElement` | 气泡控件 | `UI.Common.dll` | No | Rich |
| `BookElement` | 电子书控件 | `UI.Common.dll` | No | Rich |
| `CircleElement` | 环形卡片控件 | `UI.Common.dll` | No | Rich |
| `DataTimesElement` | 时间控件 | `UI.Common.dll` | No | Rich |
| `FishEyeElement` | 鱼眼控件 | `UI.Common.dll` | No | Rich |
| `PerspectiveWallElement` | 幻影墙控件 | `UI.SweepPanel.dll` | Yes | Rich |
| `SequenceItemsElement` | 滑块控件 | `UI.SweepPanel.dll` | Yes | Rich |
| `SequenceItemElement` | 时间轴控件 | `UI.SweepPanel.dll` | Yes | Rich |
| `Square3DElement` | 正方体控件 | `UI.Common.dll` | No | Stub |
| `WeatherElement` | 天气控件 | `UI.Common.dll` | No | Rich |
| `XamlElement` | WPF XAML容器 | `UI.Common.dll` | No | Rich |
| `PagerElement` | 长图文滑块控件 | `UI.SweepPanel.dll` | Yes | Rich |
| `VideoBannerElement` | 视频滑块控件 | `UI.Common.dll` | Yes | Rich |
| `SlideScreenElement` | 推拉屏控件 | `UI.SweepPanel.dll` | Yes | Rich |
| `ToggleButton` | 支持两种状态的图片按钮控件 | `UI.Common.dll` | No | Rich |
| `RotateControlElement` | 图片旋转控件 | `UI.Common.dll` | No | Rich |
| `CameraElement` | 摄像头显示控件 | `UI.Camera.dll` | No | Stub |
| `MapElement` | 地图控件 | `UI.Common.dll` | No | Rich |
| `QrCodeElement` | 二维码控件 | `UI.Common.dll` | No | Rich |
| `NumberElement` | 数字控件 | `UI.Common.dll` | No | Rich |
| `LongPressButton` | 长按按钮控件 | `UI.Common.dll` | No | Rich |
| `KeyboardSearchElement` | 键盘搜索控件 | `UI.Common.dll` | No | Rich |
| `KeyBoardElement` | 键盘控件 | `UI.Common.dll` | No | Rich |
| `PaintElement` | 涂鸦控件 | `UI.Common.dll` | No | Rich |
| `FrameAnimationElement` | 帧动画控件 | `UI.Common.dll` | No | Rich |
| `DrawerPanelElement` | 抽屉面板控件 | `UI.SweepPanel.dll` | Yes | Rich |
| `CircularItemsElement` | 环形滑块控件 | `UI.SweepPanel.dll` | Yes | Rich |
| `SliderElement` | 滑块条控件 | `UI.Common.dll` | No | Rich |
| `VideoBgElement` | 视频背景控件 | `UI.Common.dll` | No | Rich |
| `HtmlRenderElement` | HTML渲染控件 | `UI.SensingWebBrowser.dll` | No | Rich |
| `EBookElement` | 增强电子书控件 | `UI.Common.dll` | No | Rich |
| `BokongElement` | 波动控件 | `UI.Common.dll` | No | Stub |
| `DanceingBubbleElement` | 跳动的图片控件 | `UI.Common.dll` | No | Stub |
| `InteractiveWall3DElement` | 3D互动墙控件 | `UI.Wall3D.dll` | Yes | Stub |
| `FloorsElement` | 楼层控件 | `UI.Common.dll` | No | Rich |
| `CopilotElement` | 智能助手控件 | `UI.Common.dll` | No | Rich |

## Control registration template

```xml
<!-- UI.Common.dll controls -->
<Element ViewType="ImageElement" AssemblyFile="UI.Common.dll"
  TypeName="UI.Common.SensingControl.ImageControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.Common.dll"
    TypeName="UI.Common.SensingView.ImageElementViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>

<!-- UI.FlipView.dll controls -->
<Element ViewType="FlipViewElement" AssemblyFile="UI.FlipView.dll"
  TypeName="UI.FlipView.FlipViewControl, UI.FlipView, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.FlipView.dll"
    TypeName="UI.FlipView.FlipViewViewModel, UI.FlipView, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>

<!-- UI.Wall3D.dll controls -->
<Element ViewType="Wall3DElement" AssemblyFile="UI.Wall3D.dll"
  TypeName="UI.Wall3D.Wall3DControl, UI.Wall3D, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.Wall3D.dll"
    TypeName="UI.Wall3D.Wall3DControlViewModel, UI.Wall3D, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>

<!-- UI.SweepPanel.dll controls -->
<Element ViewType="PopupShowElement" AssemblyFile="UI.SweepPanel.dll"
  TypeName="UI.SweepPanel.PopupControl.PopupShowControl, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.SweepPanel.dll"
    TypeName="UI.SweepPanel.PopupControl.PopupShowElementViewModel, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>

<!-- UI.SensingWebBrowser.dll controls -->
<Element ViewType="WebBrowserElement" AssemblyFile="UI.SensingWebBrowser.dll"
  TypeName="UI.SensingWebBrowser.SensingWebBrowser, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.SensingWebBrowser.dll"
    TypeName="UI.SensingWebBrowser.WebBrowserViewModel, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

Replace `ViewType`, `AssemblyFile`, and both `TypeName` values with the specific control's details.
