# 浏览器控件（WebBrowserElement）

## 控件作用

WebBrowser 控件用于嵌入浏览器以提供一些网络信息。目前支持微软居于Edge的Webview2，以及居于Google的Chrome的CEF两种解决方案。

## 控件 UI 效果

![Placeholder](../images/WebBrowserElement.png)

## 配置文件样例

```
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

## 可接受的事件

1. WebViewSourceChanged 接受视频切换事件      --------此事件应该升级为SourceChanged事件，以提高通用性
2. WebViewDoRefresh 接受webview刷新事件       --------此事件应该升级为Control事件，以提高通用性
3. WebViewCallToJS 接受向WebView种的js传递事件，从而改变UI的显示

## 配置说明

### 节点 WebBrowser

    该节点主要用于设置浏览器的种类，目前只支持Chorme。

    属性说明

     Type:浏览器种类；

     Zoom（只针对wpf）:放大倍数，若zoom=200，就是显示的网页是原网页的2倍。

### 节点 DefaultAddress

    该节点主要设置的是网站的网址，不同浏览器显示的格式不完全相同，具体参照上方配置文件样例中的样例1和样例2。此外，此节点中除了嵌入网页的具体网址外，还可以嵌入某个html文件，具体方式参照上方配置文件样例中的样例3。

# UIControlDict.xml 添加浏览器控件

如果使用浏览器控件则需要在 UIControlDict.xml 中添加浏览器控件

```xml
 <!--UI.SensingWebBrowser 控件包-->
  <Element ViewType="WebBrowserElement" AssemblyFile="UI.SensingWebBrowser.dll" TypeName="UI.SensingWebBrowser.SensingWebBrowser, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.SensingWebBrowser.dll" TypeName="UI.SensingWebBrowser.WebBrowserViewModel, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.SensingWebBrowser End-->
```

## WebView与原生Wpf的交付,目前支持Edge和chrome双模式

WebView里面的html通过Javascript可与WPF原生进行交付，SensingPlatform里面的支持的事件都可以发送至Wpf端

```javascript
// WPF WebView2/CEF 收发的js, 可以新建一个javascript文件，命名为: troncell-Quorra-win.js

(function () {
    'use strict';
    function detectBrowser() {
        if (
            window.chrome &&
            window.chrome.webview &&
            window.chrome.webview.hostObjects
        ) {
            return 'edge';
        }
        if (window.android) {
            return 'chrome';
        }
        return 'unknown';
    }

    function getNative() {
        if (typeof window === 'undefined') return null;
        var browser = detectBrowser();
        if (browser === 'chrome' && window.android) return window.android;
        if (
            browser === 'edge' &&
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
                'Sensing bridge not available. Call ' +
                    methodName +
                    ' after bridge is ready.',
            );
        }
        return native;
    }

    function wrap(result) {
        if (result && typeof result.then === 'function') {
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
            return wrap(ensureNative('callNative').callNativeFromJs(msg));
        },

        getDeviceSubKey: function () {
            return wrap(ensureNative('getDeviceSubKey').getDeviceSubKey());
        },

        getDeviceId: function () {
            return wrap(ensureNative('getDeviceId').getDeviceId());
        },

        getStoreType: function () {
            return wrap(ensureNative('getStoreType').getStoreType());
        },

        getDeviceInfo: function () {
            return wrap(ensureNative('getDeviceInfo').getDeviceInfo());
        },

        getTenantId: function () {
            return wrap(ensureNative('getTenantId').getTenantId());
        },

        setValueByKey: function (key, value) {
            return wrap(
                ensureNative('setValueByKey').setValueByKey(key, value),
            );
        },

        getValueByKey: function (key) {
            return wrap(ensureNative('getValueByKey').getValueByKey(key));
        },

        downloadFileUrlsToLocal: function (links) {
            return wrap(
                ensureNative('downloadFileUrlsToLocal').downloadFileUrlsToLocal(
                    JSON.stringify(links),
                ),
            );
        },

        getLocalFileUrl: function (url) {
            return wrap(ensureNative('getLocalFileUrl').getLocalFileUrl(url));
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
            var native = ensureNative('addBehaviorRecord');
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
            return wrap(ensureNative('log').log(content));
        },

        publishEvents: function (events) {
            return wrap(ensureNative('publishEvents').publishEvents(JSON.stringify(events)));
        },
    };
})();


```

具体使用的例子如下:

```javascript

<script src="troncell-Quorra-win.js"></script>

// 收
// Entry point for WPF -> JS callbacks
function jsCallbackByNative(action, jsonData) {
    console.log('Received from native:', action, jsonData);
    addCallback(action, jsonData);
}

// 发事件到Wpf Native
SensingBridge.publishEvents(['Navigate?Page=StarPWallPageA&TrackingData=知识产权'])
```
