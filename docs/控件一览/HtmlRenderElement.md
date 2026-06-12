# 网页渲染控件（HtmlRenderElement）

## 1.控件作用

网页渲染控件用于加载和渲染静态 HTML 网页内容，并自动下载网页中引用的图片资源显示到屏幕上。该控件通常配合后台配置、AppPod 数据下载和 `SensingData` 模块使用，适用于需要动态展示富文本、图文混排内容的场景。

## 2.适用场景

- 需要展示包含图文混排的动态内容
- 后台编辑 HTML 内容，前端自动渲染
- 产品介绍、新闻资讯、活动详情等富文本展示
- 需要离线缓存网页图片的展示场景

## 3.前置依赖

使用网页渲染控件前，必须满足以下条件：

1. 项目目录中存在 `UI.HtmlRenderControl.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `HtmlRenderElement`；
3. 在 `TronSensingShow.dll.config` 中启用 `SensingData` 模块（如需要）；
4. 通过 AppPod 配置软件下载相关数据；
5. 后台配置中已准备好 HTML 内容和图片资源地址。

## 4.控件 UI 效果

![Placeholder](../images/BookElement.png)

## 5.配置文件样例

```xml

<HtmlRenderElement>
	<UIDisplay Left="910" Top="623" Width="720" Height="324" IsShow="True" ZIndex="6" UsePercent="False"/>

	<CustomerConfig>
		<HtmlRender UriKind="Project">{$Description}</HtmlRender>
	</CustomerConfig>

</HtmlRenderElement>

```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对网页渲染控件：

- `Width` / `Height`：定义网页内容的渲染区域大小；
- `ZIndex`：注意网页内容与其他控件的层级关系；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`。

## 7.CustomerConfig 参数说明

### 7.1HtmlRender 节点

| 属性      | 必填 | 说明                    | 示例      |
| --------- | ---- | ----------------------- | --------- |
| `UriKind` | 是   | HTML 内容的路径解析方式 | `Project` |

### 7.2节点值

`HtmlRender` 节点的值为静态 HTML 代码或 HTML 文件路径。常见用法：

1. **数据绑定模式**：使用 `{$Description}` 绑定数据源中的 HTML 内容字段；
2. **直接嵌入模式**：直接在节点内写入 HTML 代码；
3. **文件路径模式**：指向本地 HTML 文件路径。

### 7.3UriKind 说明

| 取值          | 路径基准              | 示例                                  |
| ------------- | --------------------- | ------------------------------------- |
| `Application` | 应用根目录            | `Shell\Pages\DetailPage\content.html` |
| `Project`     | `Shell` 文件夹        | `Pages\DetailPage\content.html`       |
| `Relative`    | 当前 XML 文件所在目录 | `content.html`                        |
| `Absolute`    | 绝对路径              | `C:\Content\content.html`             |

### 7.4数据绑定示例

```xml
<DataProvider>NewsData?CSTable=News</DataProvider>

<CustomerConfig>
    <HtmlRender UriKind="Project">{$Description}</HtmlRender>
</CustomerConfig>
```

- `{$Description}` 对应数据源中的 HTML 内容字段；
- 字段内容应为完整的 HTML 代码片段或 HTML 文件路径。

### 7.5图片资源说明

网页中的图片地址需要指向可访问的资源：

- 在线图片：使用完整的 HTTP/HTTPS URL；
- 本地图片：使用相对于 HTML 内容的路径，或配置为可被控件下载的地址；
- 通过 AppPod 配置下载的图片资源，通常会自动缓存到本地指定目录。

## 8.后台配置与数据流程

1. **后台配置**：在管理后台编辑 HTML 内容，并设置图片资源地址；
2. **AppPod 下载**：通过 AppPod 配置软件将后台数据下载到本地；
3. **SensingData 加载**：运行时通过 `SensingData` 模块读取本地数据；
4. **HtmlRenderElement 渲染**：控件根据配置渲染 HTML 内容和图片。

## 9.UIControlDict.xml 添加网页渲染控件

如果使用网页渲染控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<!--HtmlRender 控件包-->
<Element ViewType="HtmlRenderElement" AssemblyFile="UI.HtmlRenderControl.dll" TypeName="UI.HtmlRenderControl.HtmlRenderControl, UI.HtmlRenderControl, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.HtmlRenderControl.dll" TypeName="UI.HtmlRenderControl.HtmlRenderViewModel, UI.HtmlRenderControl, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 10.部署说明

1. 将 `UI.HtmlRenderControl.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 在 `TronSensingShow.dll.config` 中启用 `SensingData` 模块；
4. 通过 AppPod 下载后台配置的 HTML 内容和图片资源；
5. 在页面 XML 中使用 `HtmlRenderElement`，配置 `UIDisplay` 和 `CustomerConfig`。

## 11.常见问题

### 网页内容不显示

- 检查 `HtmlRender` 节点值是否为空或路径错误；
- 检查 `UriKind` 是否选择正确；
- 检查 `DataProvider` 中的数据源名称和字段名是否正确。

### 图片不显示

- 检查 HTML 中图片地址是否可访问；
- 检查图片是否已通过 AppPod 正确下载到本地；
- 检查图片路径是否使用了正确的 `UriKind`。

### 渲染样式异常

- 检查 HTML 代码是否包含不被支持的 CSS 或 JavaScript；
- 检查控件是否支持复杂的 HTML 布局；
- 尝试简化 HTML 代码进行测试。

### 数据没有更新

- 检查是否已通过 AppPod 重新下载最新数据；
- 检查 `SensingData` 模块是否正常工作；
- 检查数据源中的字段值是否已更新。

### 控件加载失败

- 检查 `UI.HtmlRenderControl.dll` 是否存在于应用根目录；
- 检查 `UIControlDict.xml` 中的 `AssemblyFile` 和 `TypeName` 是否正确；
- 检查 `SensingData` 模块是否已启用。

## 12.注意事项

- 网页渲染控件主要用于静态 HTML 内容，复杂的 JavaScript 交互可能不支持；
- 建议控制 HTML 内容的大小和复杂度，避免影响渲染性能；
- 图片资源建议提前通过 AppPod 下载到本地，避免运行时网络加载延迟；
- HTML 中引用的资源路径建议使用相对路径或本地缓存路径。
