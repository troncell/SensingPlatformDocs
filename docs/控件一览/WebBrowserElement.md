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

```
 <!--UI.SensingWebBrowser 控件包-->
  <Element ViewType="WebBrowserElement" AssemblyFile="UI.SensingWebBrowser.dll" TypeName="UI.SensingWebBrowser.SensingWebBrowser, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.SensingWebBrowser.dll" TypeName="UI.SensingWebBrowser.WebBrowserViewModel, UI.SensingWebBrowser, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.SensingWebBrowser End-->
```
