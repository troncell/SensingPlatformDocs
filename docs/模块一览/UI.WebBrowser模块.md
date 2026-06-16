## 1. UI.WebBrowser 模块

UI.WebBrowser 模块提供嵌入式浏览器能力，对应控件为 `WebBrowserElement`。支持两种浏览器后端：

- **Edge**：基于 Microsoft WebView2 运行时。
- **Chrome**：基于 CefSharp（Chromium）。

该模块需要在 `TronSensingShow.exe.config` 中显式注册，因为模块加载时需要初始化 CefSharp 环境（即使使用 Edge 模式，模块初始化逻辑也会执行）。

### 1.1 模块注册

在 `TronSensingShow.exe.config` 的 `modules` 节点中添加：

```xml
<module assemblyFile="UI.SensingWebBrowser.dll"
        moduleType="UI.SensingWebBrowser.SensingWebBrowserModule, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"
        moduleName="UI.SensingWebBrowser"
        startupLoaded="true" />
```

### 1.2 全局开关

在 `TronSensingShow.exe.config` 的 `appSettings` 节点中控制是否启用 WebView：

```xml
<appSettings>
  <!-- 是否使用 WebView（WebView2 / CefSharp）。设为 False 时浏览器控件不会初始化 -->
  <add key="IsUseWebView" value="True" />
</appSettings>
```

`IsUseWebView` 为 `True` 时，`UI.SensingWebBrowser` 模块才会进行浏览器环境初始化；为 `False` 时即使注册了模块，浏览器控件也不会生效。

### 1.3 平台要求

- 必须编译为 **x64**（WebView2 与 CefSharp 均要求 x64，不可改为 AnyCPU）。
- 使用 Edge 模式时，运行环境需安装 WebView2 运行时。
- 使用 Chrome 模式时，需确保 CefSharp 环境完整（`Installation.Instance.IsInstalledChromeEnv` 为 `True`）。

### 1.4 控件使用

模块启用后，在页面 XML 中使用 `WebBrowserElement` 控件：

```xml
<WebBrowserElement Name="WebBrowser">
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
  <CustomerConfig>
    <WebBrowser Type="Edge" Zoom="100">
      <DefaultAddress UriKind="Web">http://www.example.com</DefaultAddress>
    </WebBrowser>
  </CustomerConfig>
</WebBrowserElement>
```

控件详细参数、事件（切换地址、刷新、JS 交互）和常见问题请参考 [控件一览/WebBrowserElement.md](../控件一览/WebBrowserElement.md)。

### 1.5 控件注册

如果 `SysConfig/UIControlDict.xml` 中尚未注册 `WebBrowserElement`，需要添加：

```xml
<!--UI.SensingWebBrowser 控件包-->
<Element ViewType="WebBrowserElement" AssemblyFile="UI.SensingWebBrowser.dll" TypeName="UI.SensingWebBrowser.SensingWebBrowser, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.SensingWebBrowser.dll" TypeName="UI.SensingWebBrowser.WebBrowserViewModel, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
<!--UI.SensingWebBrowser End-->
```

### 1.6 注意事项

1. 浏览器控件层级较高，容易遮挡其他 WPF 控件，设计页面时注意 `ZIndex` 与布局。
2. `WebViewCallToJS` 事件中的 URL 参数 `&` 必须转义为 `&amp;`。
3. 控件卸载时会取消事件订阅并释放浏览器资源。
4. 详细的浏览器实现与 JS 桥接说明可参考 [Product/UI/UI.WebBrowser/CLAUDE.md](../../Product/UI/UI.WebBrowser/CLAUDE.md)。
