# 浏览器控件（WebBrowserElement）

## 1.控件作用

浏览器控件用于在页面或弹出框中嵌入浏览器，显示网页内容或与 Web 应用交互。当前支持两种浏览器后端：

- **Edge（WebView2）**：基于 Microsoft Edge 的 WebView2 运行时；
- **Chrome（CefSharp）**：基于 Google Chromium 的 CefSharp 浏览器。

控件支持通过事件切换地址、刷新页面，并支持与网页 JavaScript 进行双向通信。

## 2.适用场景

- 页面内嵌网页展示
- 地图、数据可视化大屏
- 需要与 Web 前端交互的触摸屏应用
- 网页游戏或 H5 活动页面

## 3.前置依赖

使用浏览器控件前，必须满足以下条件：

1. 项目目录中存在 `UI.SensingWebBrowser.dll`；
2. 平台目标必须为 `x64`（WebView2 与 CefSharp 均要求 x64，不可使用 AnyCPU）；
3. 在 `SysConfig/UIControlDict.xml` 中注册 `WebBrowserElement`；
4. 使用 Edge 模式时，运行环境需安装 WebView2 运行时；
5. 使用 Chrome 模式时，需确保已安装 CefSharp 运行环境（`Installation.Instance.IsInstalledChromeEnv` 为 `True`）。

## 4.控件 UI 效果

![Placeholder](../images/WebBrowserElement.png)

## 5.配置文件样例

### 5.1Edge 浏览器

```xml
<WebBrowserElement Name="WebBrowser">
    <UIDisplay Left="100" Top="100" Width="1720" Height="880" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1"/>
    <CustomerConfig>
        <!--放置WebBrowser片段
        Type：为所使用的浏览器类型，可选用Edge浏览器和Chrom浏览器中的一种
        Zoom: 浏览器默认的放大比例
        DefaultAddress：为默认大概的页面地址，UriKind是通用的，和ImageSource片段类似
         -->
        <WebBrowser Type="Edge" Zoom="100">
            <DefaultAddress UriKind="Web">http://www.microsoft.com/en-us/default.aspx</DefaultAddress>
        </WebBrowser>
    </CustomerConfig>
</WebBrowserElement>
```

### 5.2Chrome 浏览器

```xml
<WebBrowserElement Name="WebBrowser">
    <UIDisplay Left="100" Top="100" Width="1720" Height="880" IsShow="True" ZIndex="1" UsePercent="False" Opacity="1" />
    <CustomerConfig>
        <WebBrowser Type="Chrome" Zoom="100">
            <DefaultAddress UriKind="Web">http://www.microsoft.com/en-us/default.aspx</DefaultAddress>
        </WebBrowser>
    </CustomerConfig>
</WebBrowserElement>
```

### 5.3本地 HTML 文件

```xml
<WebBrowserElement Name="WebBrowser">
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
    <CustomerConfig>
        <WebBrowser Type="Edge" Zoom="100">
            <DefaultAddress UriKind="Application">Shell\Pages\HomePage\index.html</DefaultAddress>
        </WebBrowser>
    </CustomerConfig>
</WebBrowserElement>
```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。

## 7.CustomerConfig 参数说明

### 7.1WebBrowser 节点

| 属性     | 必填 | 类型                  | 默认值                    | 说明                                                      |
| -------- | ---- | --------------------- | ------------------------- | --------------------------------------------------------- |
| `Type` | 否   | `Edge` / `Chrome` | `IE`（实际回退为 Edge） | 浏览器类型，大小写不敏感。                                |
| `Zoom` | 否   | `double`            | `100`                   | 页面缩放比例，`100` 表示原尺寸，`200` 表示放大 2 倍。 |

### 7.2节点 DefaultAddress

    该节点主要设置的是网站的网址，不同浏览器显示的格式不完全相同，具体参照上方配置文件样例中的样例1和样例2。此外，此节点中除了嵌入网页的具体网址外，还可以嵌入某个html文件，具体方式参照上方配置文件样例中的样例3。

| 属性        | 必填 | 类型                                                                  | 默认值 | 说明                                     |
| ----------- | ---- | --------------------------------------------------------------------- | ------ | ---------------------------------------- |
| `UriKind` | 否   | `Web` / `Application` / `Project` / `Absolute` / `Relative` | —     | 地址解析方式。                           |
| 节点值      | 是   | `string`                                                            | —     | 默认加载的网页地址或本地 HTML 文件路径。 |

### 7.3UriKind 说明

| 取值            | 路径基准              | 示例                                |
| --------------- | --------------------- | ----------------------------------- |
| `Web`         | HTTP/HTTPS 网络地址   | `http://www.microsoft.com`        |
| `Application` | 应用根目录            | `Shell\Pages\HomePage\index.html` |
| `Project`     | `Shell` 文件夹      | `Pages\HomePage\index.html`       |
| `Absolute`    | 物理磁盘绝对路径      | `C:\Web\index.html`               |
| `Relative`    | 当前 XML 文件所在目录 | `index.html`                      |

## 8.可接受的事件

### 8.1WebViewSourceChanged 事件

WebViewSourceChanged 接受视频切换事件 --------此事件应该升级为SourceChanged事件，以提高通用性
用于动态切换浏览器加载的地址。

```xml
<ClickEvent>WebViewSourceChanged?TargetPageName=HomePage&TargetControlName=WebBrowser&SourcePath=http://example.com</ClickEvent>
```

| 参数                  | 说明                       | 示例                   |
| --------------------- | -------------------------- | ---------------------- |
| `TargetPageName`    | 目标页面名称               | `HomePage`           |
| `TargetControlName` | 目标浏览器控件名称         | `WebBrowser`         |
| `SourcePath`        | 新的网页地址或本地文件路径 | `http://example.com` |

### 8.2WebViewDoRefresh 事件

WebViewDoRefresh 接受webview刷新事件 --------此事件应该升级为Control事件，以提高通用性

用于刷新浏览器当前页面。

```xml
<ClickEvent>WebViewDoRefresh?TargetPageName=HomePage&TargetControlName=WebBrowser</ClickEvent>
```

### 8.3WebViewCallToJS 事件

WebViewCallToJS 接受向WebView种的js传递事件，从而改变UI的显示

用于向浏览器中的 JavaScript 发送消息。

```xml
<ClickEvent>WebViewCallToJS?TargetPageName=HomePage&TargetControlName=WebBrowser&DoAction=showAlert&JsonData=hello</ClickEvent>
```

| 参数         | 说明             | 示例                |
| ------------ | ---------------- | ------------------- |
| `DoAction` | JS 回调动作名称  | `showAlert`       |
| `JsonData` | 传递给 JS 的数据 | `{"key":"value"}` |

## 9.WebView 与原生 WPF 的交互

浏览器控件支持 WebView 中的 JavaScript 与 WPF 原生代码双向通信。网页端可通过 `window.android`（CefSharp）或 `window.chrome.webview.hostObjects.android`（WebView2）调用原生方法，也可通过 `jsCallbackByNative(action, jsonData)` 接收来自 WPF 的消息。

### 9.1JS SDK 示例

将以下代码保存为 `troncell-Quorra-win.js` 并在网页中引用：

```javascript
// WPF WebView2/CEF 收发的js, 可以新建一个javascript文件，命名为: troncell-Quorra-win.js
(function () {
  "use strict";

  function detectBrowser() {
    if (
      window.chrome &&
      window.chrome.webview &&
      window.chrome.webview.hostObjects
    ) {
      return "edge";
    }
    if (window.android) {
      return "chrome";
    }
    return "unknown";
  }

  function getNative() {
    if (typeof window === "undefined") return null;
    var browser = detectBrowser();
    if (browser === "chrome" && window.android) return window.android;
    if (
      browser === "edge" &&
      window.chrome &&
      window.chrome.webview &&
      window.chrome.webview.hostObjects &&
      window.chrome.webview.hostObjects.android
    ) {
      return window.chrome.webview.hostObjects.android;
    }
    return null;
  }

  window.SensingBridge = {
    browserType: detectBrowser(),
    isAvailable: function () {
      return !!getNative();
    },
    callNative: function (msg) {
      var native = getNative();
      return native
        ? native.callNativeFromJs(msg)
        : Promise.reject("bridge not ready");
    },
    getDeviceId: function () {
      var native = getNative();
      return native ? native.getDeviceId() : Promise.reject("bridge not ready");
    },
    getDeviceInfo: function () {
      var native = getNative();
      return native
        ? native.getDeviceInfo()
        : Promise.reject("bridge not ready");
    },
    setValueByKey: function (key, value) {
      var native = getNative();
      return native
        ? native.setValueByKey(key, value)
        : Promise.reject("bridge not ready");
    },
    getValueByKey: function (key) {
      var native = getNative();
      return native
        ? native.getValueByKey(key)
        : Promise.reject("bridge not ready");
    },
    publishEvents: function (events) {
      var native = getNative();
      return native
        ? native.publishEvents(JSON.stringify(events))
        : Promise.reject("bridge not ready");
    },
    log: function (content) {
      var native = getNative();
      return native ? native.log(content) : Promise.reject("bridge not ready");
    },
  };
})();
```

### 9.2接收 WPF 消息

```html
<script src="troncell-Quorra-win.js"></script>
<script>
  function jsCallbackByNative(action, jsonData) {
    console.log("Received from native:", action, jsonData);
  }
</script>
```

### 9.3发送事件到 WPF

```javascript
SensingBridge.publishEvents([
  "Navigate?Page=StarPWallPageA&TrackingData=知识产权",
]);
```

> **Edge 模式额外说明**：除了 HostObject 方式，WebView2 还支持通过 `window.chrome.webview.postMessage` 发送 JSON 消息，WPF 端通过 `CoreWebView2.WebMessageReceived` 接收。

# 10.UIControlDict.xml 添加浏览器控件

如果使用浏览器控件则需要在 UIControlDict.xml 中添加浏览器控件

```xml
 <!--UI.SensingWebBrowser 控件包-->
  <Element ViewType="WebBrowserElement" AssemblyFile="UI.SensingWebBrowser.dll" TypeName="UI.SensingWebBrowser.SensingWebBrowser, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.SensingWebBrowser.dll" TypeName="UI.SensingWebBrowser.WebBrowserViewModel, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.SensingWebBrowser End-->
```

## 11.WebView与原生Wpf的交付,目前支持Edge和chrome双模式（以前老的）

WebView里面的html通过Javascript可与WPF原生进行交付，SensingPlatform里面的支持的事件都可以发送至Wpf端

```javascript
// WPF WebView2/CEF 收发的js, 可以新建一个javascript文件，命名为: troncell-Quorra-win.js

(function () {
  "use strict";
  function detectBrowser() {
    if (
      window.chrome &&
      window.chrome.webview &&
      window.chrome.webview.hostObjects
    ) {
      return "edge";
    }
    if (window.android) {
      return "chrome";
    }
    return "unknown";
  }

  function getNative() {
    if (typeof window === "undefined") return null;
    var browser = detectBrowser();
    if (browser === "chrome" && window.android) return window.android;
    if (
      browser === "edge" &&
      window.chrome &&
      window.chrome.webview &&
      window.chrome.webview.hostObjects &&
      window.chrome.webview.hostObjects.android
    ) {
      return window.chrome.webview.hostObjects.android;
    }
    return null;
  }

  function ensureNative(methodName) {
    var native = getNative();
    if (!native) {
      throw new Error(
        "Sensing bridge not available. Call " +
          methodName +
          " after bridge is ready.",
      );
    }
    return native;
  }

  function wrap(result) {
    if (result && typeof result.then === "function") {
      return result;
    }
    return Promise.resolve(result);
  }

  window.SensingBridge = {
    browserType: detectBrowser(),

    isAvailable: function () {
      return !!getNative();
    },

    callNative: function (msg) {
      return wrap(ensureNative("callNative").callNativeFromJs(msg));
    },

    getDeviceSubKey: function () {
      return wrap(ensureNative("getDeviceSubKey").getDeviceSubKey());
    },

    getDeviceId: function () {
      return wrap(ensureNative("getDeviceId").getDeviceId());
    },

    getStoreType: function () {
      return wrap(ensureNative("getStoreType").getStoreType());
    },

    getDeviceInfo: function () {
      return wrap(ensureNative("getDeviceInfo").getDeviceInfo());
    },

    getTenantId: function () {
      return wrap(ensureNative("getTenantId").getTenantId());
    },

    setValueByKey: function (key, value) {
      return wrap(ensureNative("setValueByKey").setValueByKey(key, value));
    },

    getValueByKey: function (key) {
      return wrap(ensureNative("getValueByKey").getValueByKey(key));
    },

    downloadFileUrlsToLocal: function (links) {
      return wrap(
        ensureNative("downloadFileUrlsToLocal").downloadFileUrlsToLocal(
          JSON.stringify(links),
        ),
      );
    },

    getLocalFileUrl: function (url) {
      return wrap(ensureNative("getLocalFileUrl").getLocalFileUrl(url));
    },

    addBehaviorRecord: function (
      jsonRecordOrThingId,
      thingCategory,
      thingName,
      action,
      increment,
      collectionTime,
      collectEndTime,
      softwareName,
      pageName,
      pageArea,
      previousPageName,
      previousPageArea,
      position,
      pSource,
      comments,
    ) {
      var native = ensureNative("addBehaviorRecord");
      if (arguments.length === 1) {
        return wrap(native.addBehaviorRecord(jsonRecordOrThingId));
      }
      return wrap(
        native.addBehaviorRecord(
          jsonRecordOrThingId,
          thingCategory,
          thingName,
          action,
          increment,
          collectionTime,
          collectEndTime,
          softwareName,
          pageName,
          pageArea,
          previousPageName,
          previousPageArea,
          position,
          pSource,
          comments,
        ),
      );
    },

    log: function (content) {
      return wrap(ensureNative("log").log(content));
    },

    publishEvents: function (events) {
      return wrap(
        ensureNative("publishEvents").publishEvents(JSON.stringify(events)),
      );
    },
  };
})();
```

具体使用的例子如下:

```javascript
<script src="troncell-Quorra-win.js"></script>;

// 收
// Entry point for WPF -> JS callbacks
function jsCallbackByNative(action, jsonData) {
  console.log("Received from native:", action, jsonData);
  addCallback(action, jsonData);
}

// 发事件到Wpf Native
SensingBridge.publishEvents([
  "Navigate?Page=StarPWallPageA&TrackingData=知识产权",
]);
```

## 12.部署说明

1. 确认项目目录中存在 `UI.SensingWebBrowser.dll`；
2. 确认平台目标为 `x64`；
3. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
4. 根据需求选择 Edge 或 Chrome 模式；
5. 准备网页地址或本地 HTML 文件；
6. 在页面 XML 中使用 `WebBrowserElement`，配置 `UIDisplay` 与 `CustomerConfig`。

## 13.常见问题

### 浏览器不显示

- 检查 `UI.SensingWebBrowser.dll` 是否存在于应用根目录；
- 检查 `UIControlDict.xml` 中是否已注册 `WebBrowserElement`；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查平台目标是否为 `x64`。

### Edge 模式黑屏或无法加载

- 检查运行环境是否已安装 WebView2 运行时；
- 检查 `DefaultAddress` 的 `UriKind` 和地址是否正确；
- 检查网络连接是否正常（Web 地址）。

### Chrome 模式无法启动

- 检查 CefSharp 环境是否完整；
- 检查 `Installation.Instance.IsInstalledChromeEnv` 是否为 `True`；
- 检查平台目标是否为 `x64`。

### JS 交互不生效

- 检查网页中是否正确引入 `troncell-Quorra-win.js`；
- 检查是否定义了 `jsCallbackByNative(action, jsonData)` 函数；
- 检查 `WebViewCallToJS` 事件中的 `TargetPageName` 与 `TargetControlName` 是否正确；
- Edge 模式下确认 `androidBridgeReady` 事件已触发后再调用原生方法。

### 页面缩放不符合预期

- 调整 `WebBrowser` 节点的 `Zoom` 属性；
- Edge 模式下 `Zoom=-1` 会根据控件实际宽度自动缩放（以 800px 为参考宽度）。

## 14.注意事项

- 该模块必须编译为 `x64`，不可改为 `AnyCPU`；
- 当前默认浏览器类型代码中为 `IE`，但实际未识别时会回退为 `Edge`；
- Chrome 模式依赖 `Installation.Instance.IsInstalledChromeEnv`，若环境不满足会返回 `null`，控件不会显示；
- 控件卸载时会取消事件订阅并释放浏览器资源；
- 事件 URL 中的 `&` 必须转义为 `&amp;`；
- 详细的浏览器实现与 JS 桥接说明可参考 [Product/UI/UI.WebBrowser/CLAUDE.md](Product/UI/UI.WebBrowser/CLAUDE.md)。
