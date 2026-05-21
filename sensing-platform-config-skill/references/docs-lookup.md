# Documentation Lookup

The detailed configuration docs for SensingPlatform live in the **SensingPlatformDocs** repo (`https://github.com/troncell/SensingPlatformDocs`). The skill's reference files summarize common patterns, but **when you need granular per-control parameters, always read the original doc file first.**

## How to resolve the docs path

The docs repo may be cloned anywhere. Before reading doc files, determine its location:

1. Ask the user: "Where is your SensingPlatformDocs repo cloned?" (or check common locations).
2. If the user has not cloned it, suggest they clone it: `git clone https://github.com/troncell/SensingPlatformDocs.git`
3. Common locations to check:
   - `D:\gits\SensingPlatformDocs\` (Windows)
   - `~/gits/SensingPlatformDocs/` or `~/SensingPlatformDocs/` (macOS/Linux)
   - `C:\Users\<user>\SensingPlatformDocs\` (Windows)

Use the resolved path as `<DOCS_ROOT>` in the table below.

## How to use

When the user asks for a specific control, event, data source, or module, `Read` the corresponding file below (under `<DOCS_ROOT>/docs/`) before generating XML. Do not rely on memory — the doc files are the authoritative source for `CustomerConfig` parameters, event arguments, and data source options.

## Controls (`<DOCS_ROOT>/docs/控件一览/`)

| ViewType | Doc file | Notes |
|---|---|---|
| `AlbumElement` | `<DOCS_ROOT>/docs/控件一览/AlbumElement.md` | |
| `BokongElement` | `<DOCS_ROOT>/docs/控件一览/BokongElement.md` | Stub |
| `BookElement` | `<DOCS_ROOT>/docs/控件一览/BookElement.md` | |
| `BubbleElement` | `<DOCS_ROOT>/docs/控件一览/BubbleElement.md` | |
| `CameraElement` | `<DOCS_ROOT>/docs/控件一览/CameraElement.md` | Stub |
| `CircleElement` | `<DOCS_ROOT>/docs/控件一览/CircleElement.md` | |
| `CircularItemsElement` | `<DOCS_ROOT>/docs/控件一览/CircularItemsElement.md` | |
| `CommonElement` | `<DOCS_ROOT>/docs/控件一览/CommonElement.md` | **Shared primer** — read this first for UIDisplay, ImageSource, DataProvider, Items syntax |
| `CopilotElement` | `<DOCS_ROOT>/docs/控件一览/CopilotElement.md` | |
| `CustomerElement` | `<DOCS_ROOT>/docs/控件一览/CustomerElement.md` | Host custom .NET 10 WPF controls — build in VS/Blend, drop DLL into app folder, reference via `<Activator>` |
| `DanceingBubbleElement` | `<DOCS_ROOT>/docs/控件一览/DanceingBubbleElement.md` | Stub |
| `DataTimesElement` | `<DOCS_ROOT>/docs/控件一览/DataTimesElement.md` | |
| `DrawerPanelElement` | `<DOCS_ROOT>/docs/控件一览/DrawerPanelElement.md` | |
| `EBookElement` | `<DOCS_ROOT>/docs/控件一览/EBookElement.md` | |
| `FishEyeElement` | `<DOCS_ROOT>/docs/控件一览/FishEyeElement.md` | |
| `FlipViewElement` | `<DOCS_ROOT>/docs/控件一览/FlipViewElement.md` | Rich data-binding example |
| `FloorsElement` | `<DOCS_ROOT>/docs/控件一览/FloorsElement.md` | |
| `FrameAnimationElement` | `<DOCS_ROOT>/docs/控件一览/FrameAnimationElement.md` | |
| `HtmlRenderElement` | `<DOCS_ROOT>/docs/控件一览/HtmlRenderElement.md` | |
| `ImageButton` | `<DOCS_ROOT>/docs/控件一览/ImageButton.md` | ClickEvent, AutoClick, ElapsedTime |
| `ImageElement` | `<DOCS_ROOT>/docs/控件一览/ImageElement.md` | ImageSource, UriKind |
| `InteractiveWall3DElement` | `<DOCS_ROOT>/docs/控件一览/InteractiveWall3DElement.md` | Stub |
| `KeyBoardElement` | `<DOCS_ROOT>/docs/控件一览/KeyBoardElement.md` | |
| `KeyboardSearchElement` | `<DOCS_ROOT>/docs/控件一览/KeyboardSearchElement.md` | |
| `LongPressButton` | `<DOCS_ROOT>/docs/控件一览/LongPressButton.md` | |
| `MapElement` | `<DOCS_ROOT>/docs/控件一览/MapElement.md` | |
| `NumberElement` | `<DOCS_ROOT>/docs/控件一览/NumberElement.md` | |
| `PagerElement` | `<DOCS_ROOT>/docs/控件一览/PagerElement.md` | |
| `PaintElement` | `<DOCS_ROOT>/docs/控件一览/PaintElement.md` | |
| `PerspectiveWallElement` | `<DOCS_ROOT>/docs/控件一览/PerspectiveWallElement.md` | |
| `PopupShowElement` | `<DOCS_ROOT>/docs/控件一览/PopupShowElement.md` | IncludeTemplate, LayoutManager |
| `QrCodeElement` | `<DOCS_ROOT>/docs/控件一览/QrCodeElement.md` | |
| `RotateControlElement` | `<DOCS_ROOT>/docs/控件一览/RotateControlElement.md` | |
| `ScrollViewElement` | `<DOCS_ROOT>/docs/控件一览/ScrollViewElement.md` | PointManger, scroll points |
| `SequenceItemElement` | `<DOCS_ROOT>/docs/控件一览/SequenceItemElement.md` | |
| `SequenceItemsElement` | `<DOCS_ROOT>/docs/控件一览/SequenceItemsElement.md` | |
| `SlideScreenElement` | `<DOCS_ROOT>/docs/控件一览/SlideScreenElement.md` | |
| `SliderElement` | `<DOCS_ROOT>/docs/控件一览/SliderElement.md` | |
| `Square3DElement` | `<DOCS_ROOT>/docs/控件一览/Square3DElement.md` | Stub |
| `TextElement` | `<DOCS_ROOT>/docs/控件一览/TextElement.md` | TextSource, AutoMove |
| `ToggleButton` | `<DOCS_ROOT>/docs/控件一览/ToggleButton.md` | |
| `VideoBannerElement` | `<DOCS_ROOT>/docs/控件一览/VideoBannerElement.md` | |
| `VideoBgElement` | `<DOCS_ROOT>/docs/控件一览/VideoBgElement.md` | |
| `VideoPlayerElement` | `<DOCS_ROOT>/docs/控件一览/VideoPlayerElement.md` | Player, Controller, FinishEvent |
| `Wall3DElement` | `<DOCS_ROOT>/docs/控件一览/Wall3DElement.md` | Scenario3D, Camera, Model3D |
| `WeatherElement` | `<DOCS_ROOT>/docs/控件一览/WeatherElement.md` | |
| `WebBrowserElement` | `<DOCS_ROOT>/docs/控件一览/WebBrowserElement.md` | Edge WebView2 / Chrome CEF; JS↔WPF bridge via `window.chrome.webview` |
| `XamlElement` | `<DOCS_ROOT>/docs/控件一览/XamlElement.md` | General WPF XAML host — TextBox, TextBlock, Border, gradients, etc. Paste XAML from Blend/VS directly |
| `XYContainerElement` | `<DOCS_ROOT>/docs/控件一览/XYContainerElement.md` | Groups multiple controls inside `<Controls>`; acts as a single unit for layout and events |

**Always read `<DOCS_ROOT>/docs/控件一览/CommonElement.md` first** when working with any control — it explains the universal `UIDisplay`, `ImageSource`, `FileSource`, `DataProvider`, and `Items` syntax.

**Always read `<DOCS_ROOT>/docs/控件一览/readme.md`** for the shared `Transitions`, `CustomerConfig`, and animation syntax.

## Events (`<DOCS_ROOT>/docs/事件一览/`)

| Topic | Doc file |
|---|---|
| All event actions | `<DOCS_ROOT>/docs/事件一览/README.md` |

## Data sources (`<DOCS_ROOT>/docs/数据一览/`)

| Data source | Doc file |
|---|---|
| All data source types | `<DOCS_ROOT>/docs/数据一览/README.md` |
| CameraData | `<DOCS_ROOT>/docs/数据一览/CameraData.md` |
| DbData | `<DOCS_ROOT>/docs/数据一览/DbData.md` |
| ExcelData | `<DOCS_ROOT>/docs/数据一览/ExcelData.md` |
| ExcelTimeLineData | `<DOCS_ROOT>/docs/数据一览/ExcelTimeLineData.md` |
| FolderData | `<DOCS_ROOT>/docs/数据一览/FolderData.md` |
| SensingData | `<DOCS_ROOT>/docs/数据一览/SensingData.md` |
| TimeLineData | `<DOCS_ROOT>/docs/数据一览/TimeLineData.md` |
| XmlData | `<DOCS_ROOT>/docs/数据一览/XmlData.md` |

## Modules (`<DOCS_ROOT>/docs/模块一览/`)

| Module | Doc file |
|---|---|
| Camera module | `<DOCS_ROOT>/docs/模块一览/Camera模块.md` |
| InputManager (UDP/TCP/Serial/SignalR) | `<DOCS_ROOT>/docs/模块一览/InputManager包中模块.md` |

## Product intro / system config (`<DOCS_ROOT>/docs/产品介绍/`)

| Topic | Doc file |
|---|---|
| Deployment | `<DOCS_ROOT>/docs/产品介绍/产品部署文档.md` |
| Basic usage | `<DOCS_ROOT>/docs/产品介绍/产品基础使用说明.md` |
| Project config structure | `<DOCS_ROOT>/docs/产品介绍/项目配置结构的介绍.md` |
| System.xml config | `<DOCS_ROOT>/docs/产品介绍/System配置说明.md` |
| Third-party module integration | `<DOCS_ROOT>/docs/产品介绍/第三方模块集成.md` |
