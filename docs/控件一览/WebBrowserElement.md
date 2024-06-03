# 浏览器控件（WebBrowserElement）

## 控件作用

WebBrowser 控件用于嵌入浏览器以提供一些网络信息。

## 控件 UI 效果

![Placeholder](../images/WebBrowserElement.png)

## 配置文件样例

```
<WebBrowserElement Name="WebBrowser">
    <UIDisplay Left="100" Top="100" Width="1720" Height="880" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1"/>
    <CustomerConfig>
        <!--放置WebBrowser片段 Type为所使用的浏览器类型，可选用IE浏览器和Chrom浏览器中的一种，DefaultAddress中放置的是目标地址-->
        <WebBrowser Type="IE">
            <DefaultAddress>http://www.microsoft.com/en-us/default.aspx</DefaultAddress>
        </WebBrowser>
    </CustomerConfig>
</WebBrowserElement>
```

```
<WebBrowserElement Name="WebBrowser">
    <UIDisplay Left="110" Top="45" Width="1640" Height="1000" IsShow="True" ZIndex="1" UsePercent="False" Opacity="1" />
    <CustomerConfig>
        <WebBrowser Type="wpf" Zoom="100">
            <!--Type为所使用的浏览器类型，由于浏览器需缩放，所以只能选用wpf浏览器；Zoom的值即为可缩放的倍数，若Zoom=200，则显示出的Web页为真正的Web页的2倍；DefaultAddress中放置的是目标地址，如果直接嵌入网页一般UriKind="Absolute"-->
            <DefaultAddress UriKind="Absolute">http://www.wxjgyey.com/</DefaultAddress>
        </WebBrowser>
    </CustomerConfig>
</WebBrowserElement >
```

```
<WebBrowserElement Name="WebBrowser">
    <UIDisplay Left="100" Top="40" Width="1600" Height="1000" IsShow="True" ZIndex="1" UsePercent="False" Opacity="1" />
    <CustomerConfig>
        <WebBrowser Type="wpf" Zoom="100">
            <DefaultAddress UriKind="Application">Shell\Pages\PanoramaPage\PopupItems\001\Flash1\1.html</DefaultAddress>
        </WebBrowser>
    </CustomerConfig>
</WebBrowserElement>

```

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
