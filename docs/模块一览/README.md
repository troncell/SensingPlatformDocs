# 模块一览

SensingPlatform 采用 Prism 模块化架构，运行时由 Shell 从 `Build/Bin` 目录加载所需的模块 DLL。模块主要分为三类：

- **设备/协议模块**：负责与摄像头、串口、UDP/TCP、SignalR 等外设或第三方系统通讯。
- **数据模块**：提供 `IDataProvider` 实现，为 UI 控件供给数据。
- **UI 模块**：提供具体的 WPF 控件和对应 ViewModel，供页面配置使用。

## 已文档化的模块

| 模块 | 说明 | 文档 |
| --- | --- | --- |
| Module.Camera | 摄像头（RealSense / Kinect / USB / Web）及视觉算法集成 | [Camera模块.md](Camera模块.md) |
| Module.InputManager | 外设输入协议：UDP、TCP、串口、SignalR、扫描枪 | [InputManager包中模块.md](InputManager包中模块.md) |
| SyncManager | 多机事件同步（服务端/客户端 TCP 同步） | [SyncManager模块.md](SyncManager模块.md) |
| UI.WebBrowser | 浏览器控件（Edge WebView2 / CefSharp） | [UI.WebBrowser模块.md](UI.WebBrowser模块.md) |

## 待补充文档的模块

> 以下模块在代码中存在，但尚未整理成独立的使用文档。需要时可参考对应项目源码或控件一览中的说明。

### 设备/协议模块

| 模块 | 说明 |
| --- | --- |
| Module.SyncManager | 基于 dll.config 的同步模块（与 Foundation 内置 SyncManager 二选一使用） |
| Module.InputManagerTests | 串口协议单元测试项目 |
| SerialPortModules | 步进电机串口控制模块 |
| EightControlModule | 8 屏开合机械控制模块 |

### 数据模块

| 模块 | 说明 |
| --- | --- |
| Data.Camera | 摄像头数据源 |
| Data.Chart | 图表数据源 |
| Data.CitySkype | 城市 Skype 相关数据 |
| Data.Common | 通用数据源 |
| Data.DeepZoom |  DeepZoom 数据源 |
| Data.Navigation | 导航/楼层数据 |
| Data.Sensing | Sensing 云端数据接口 |
| Data.SoftwareClientWebApi | SoftwareClient WebApi 数据 |
| Data.WebAPI | 通用 WebAPI 数据源 |
| SensingDownloader | 资源下载器 |

### UI 模块

UI 模块较多，大多数在 [控件一览](../控件一览/) 中有详细说明。常见模块包括：

- UI.Common、UI.Album、UI.Book、UI.EBook
- UI.Bubble、UI.FishEye、UI.FlipView、UI.PerspectiveWall
- UI.VideoBanner、UI.VideoBg
- UI.WebBrowser、UI.QrCode、UI.DrawerPanel
- UI.Search、UI.Keyboard、UI.Map（NavigationControl）
- UI.Paint、UI.HtmlRender、UI.SensingChart
- UI.Copilot、UI.Background、UI.Camera 等

## 如何选择需要加载的模块

普通项目通常只需要加载：

1. 外设/协议模块：根据硬件选择 `Module.InputManager`、`Module.Camera` 等。
2. UI 模块：大多数 UI 模块无需在 `TronSensingShow.exe.config` 中显式注册，只要 DLL 在 `Build/Bin` 中即可通过命名约定自动发现。
3. 特殊模块：如 `UI.WebBrowser` 需要 CefSharp 初始化，浏览器模块需要在 `modules` 节点显式配置；`SyncManager` 需要在 `System.xml` 中配置同步参数。

具体配置方式请查看各模块的详细文档。
