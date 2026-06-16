# 电子书控件（BookElement）

## 1.控件作用

电子书控件以翻书的交互方式展示一系列图片或页面内容。用户可以通过点击页面边缘实现翻页效果，常用于电子画册、产品手册、宣传册、图书展示等场景。

## 2.适用场景

- 产品画册、企业宣传册翻页展示
- 电子图书、杂志阅读
- 相册集、荣誉证书翻页浏览
- 需要左右翻页交互的图文展示页面

## 3.前置依赖

使用电子书控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Book.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `BookElement`；
3. 如需动态加载内容，需在 `Shell/Data/Data.xml` 中配置数据源并在页面中使用 `<DataProvider>`。

## 4.控件 UI 效果

![Placeholder](../images/BookElement.png)

## 5.配置文件样例

```xml
<BookElement>
<!--参考控件公用片段CommonElement.md讲解中UIDisplay片段讲解-->
	<UIDisplay Left="165" Top="280" Width="1396" Height="588" IsShow="True" ZIndex="3" UsePercent="False" />
	<!--参考控件公用片段CommonElement.md讲解中DataProvide片段讲解-->
	<DataProvider>EBookData?CSTable=TEduBook5</DataProvider>
 <Items>
        <Template Left="0" Top="0" Width="671" Height="1080" TemplateID="Image">
            <XYContainerElement TrackingData="{$FileName}">
                <UIDisplay Left="0" Top="0" Width="671" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
                <Controls>
                    <ImageElement>
                        <UIDisplay Left="0" Top="0" Width="671" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
                        <ImageSource UriKind="Absolute">{$FullName}</ImageSource>
                    </ImageElement>
                </Controls>
            </XYContainerElement>
        </Template>
    </Items>

	<!--放置CustomerConfig片段-->
	<CustomerConfig>
	<!--放置Book片段 IsCacheUI 是否预加载；IsLoop 是否循环；ShadowLevel 阴影宽度；Width/Height 为书本大小-->
		<Book IsCacheUI="True" IsLoop="true" ShadowLevel="0.6" Width="865" Height="665">
			<TouchSurface>
				<TouchRect Left="0.0" Top="0.0" Height="0.5" Width="0.2" BookState="LT2RT">
				</TouchRect>
				<TouchRect Left="0.0" Top="0.5" Height="0.5" Width="0.2" BookState="LB2RB">
				</TouchRect>
				<TouchRect Left="0.8" Top="0.0" Height="0.5" Width="0.2" BookState="RT2LT">
				</TouchRect>
				<TouchRect Left="0.8" Top="0.5" Height="0.5" Width="0.2" BookState="RB2LB">
				</TouchRect>
			</TouchSurface>
		</Book>
	</CustomerConfig>
</BookElement>

```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对电子书控件：

- `Width` / `Height`：控件在页面上的整体显示区域，书本会按 `Book` 节点中的 `Width` / `Height` 渲染，并在此区域内居中或按实际位置摆放；
- `ZIndex`：如果页面上有按钮、弹窗等覆盖层，注意层级关系；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`。

## 7.DataProvider 与 Items

### 推荐：动态数据源模式（Template + DataProvider）

通过 `DataProvider` 绑定数据源，`Items` 中使用 `Template` 作为页面模板，数据源中的每一行会生成一个书页。

```xml
<DataProvider>EBookData?CSTable=TEduBook5</DataProvider>
<Items>
    <Template Left="0" Top="0" Width="671" Height="1080" TemplateID="Image">
        <!-- 页面模板，可通过 {$列名} 绑定数据 -->
    </Template>
</Items>
```

- `EBookData`：数据源实例名称，需在 `Shell/Data/Data.xml` 中定义；
- `CSTable=TEduBook5`：数据表/集合名称；
- `Template` 中的控件可以通过 `{$变量名}` 绑定数据源中的列。

### 固定页面模式（Item）

如果不配置 `DataProvider`，可以在 `Items` 中直接放置多个 `Item` 节点，每个 `Item` 对应一个固定页面：

```xml
<Items>
    <Item>
        <ImageElement>
            <UIDisplay Left="0" Top="0" Width="671" Height="1080" />
            <ImageSource UriKind="Absolute">Images/Page1.png</ImageSource>
        </ImageElement>
    </Item>
    <Item>
        <ImageElement>
            <UIDisplay Left="0" Top="0" Width="671" Height="1080" />
            <ImageSource UriKind="Absolute">Images/Page2.png</ImageSource>
        </ImageElement>
    </Item>
</Items>
```

`Item` 内部放置一个根控件（如 `ImageElement`、`XYContainerElement`、`ImageButton` 等）。

## 8.CustomerConfig 参数说明

### 8.1Book 节点

| 属性          | 必填 | 说明                                                                            | 示例   |
| ------------- | ---- | ------------------------------------------------------------------------------- | ------ |
| `IsCacheUI`   | 否   | 是否在页面加载时预加载所有页面。`True` 翻页流畅但占用更多内存；`False` 按需加载 | `True` |
| `IsLoop`      | 否   | 是否循环翻页。`true` 翻到最后一页后回到第一页，`false` 翻到边界停止             | `true` |
| `ShadowLevel` | 否   | 翻页时阴影效果的强度或宽度，取值范围通常为 `0` ~ `1`                            | `0.6`  |
| `Width`       | 否   | 书本的宽度                                                                      | `865`  |
| `Height`      | 否   | 书本的高度                                                                      | `665`  |

### 8.2属性说明

- **IsCacheUI**：设为 `True` 时，进入页面后会预先把所有页面加载到内存，翻页动画更流畅；页面内容较多时建议评估内存占用。设为 `False` 时延迟加载，可节省内存。
- **IsLoop**：控制翻页边界行为。`true` 表示最后一页之后继续翻回到第一页，形成循环；`false` 表示翻到有边界时停止，无法继续同方向翻页。
- **ShadowLevel**：翻页过程中书页下方阴影的深浅或宽度。数值越大阴影越明显，`0` 表示无阴影。
- **Width / Height**：定义电子书显示区域的书本大小，建议与背景图、页面内容尺寸匹配。

## 9.TouchSurface 与 TouchRect

`TouchSurface` 用于定义书本四周的点击热区，用户点击这些区域时触发翻页。

### 9.1TouchRect 属性

| 属性        | 必填 | 说明                                      | 示例    |
| ----------- | ---- | ----------------------------------------- | ------- |
| `Left`      | 是   | 热区左边距，取值为 `0.0` ~ `1.0` 的相对值 | `0.0`   |
| `Top`       | 是   | 热区上边距，取值为 `0.0` ~ `1.0` 的相对值 | `0.0`   |
| `Width`     | 是   | 热区宽度，取值为 `0.0` ~ `1.0` 的相对值   | `0.2`   |
| `Height`    | 是   | 热区高度，取值为 `0.0` ~ `1.0` 的相对值   | `0.5`   |
| `BookState` | 是   | 翻页方向状态                              | `LT2RT` |

### 9.2BookState 取值说明

| 取值    | 含义                     | 典型位置     |
| ------- | ------------------------ | ------------ |
| `LT2RT` | 从左上区域触发，向右翻页 | 左侧上半部分 |
| `LB2RB` | 从左下区域触发，向右翻页 | 左侧下半部分 |
| `RT2LT` | 从右上区域触发，向左翻页 | 右侧上半部分 |
| `RB2LB` | 从右下区域触发，向左翻页 | 右侧下半部分 |

> 热区坐标是相对书本区域（`0,0` 到 `1,1`）的百分比。例如 `Left="0.8" Width="0.2"` 表示右侧 20% 的宽度范围。

## 10.UIControlDict.xml 添加电子书控件

如果使用电子书控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<!--UI.Book 控件包-->
<Element ViewType="BookElement" AssemblyFile="UI.Book.dll" TypeName="UI.Book.BookControl, UI.Book, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.Book.dll" TypeName="UI.Book.BookElementViewModel, UI.Book, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
<!--UI.Book End-->
```

## 11.部署说明

1. 将 `UI.Book.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 如需动态数据，在 `Shell/Data/Data.xml` 中配置数据源，并在页面中使用 `<DataProvider>`；
4. 在页面 XML 中使用 `<BookElement>`，配置 `UIDisplay`、`DataProvider`、`Items` 和 `CustomerConfig`。

## 12.常见问题

### 翻页没反应

- 检查 `TouchSurface` 中 `TouchRect` 的 `BookState` 是否配置正确；
- 确认热区范围没有重叠或被上层控件遮挡；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`。

### 图片不显示

- 检查 `ImageSource` 的 `UriKind` 和路径是否正确；
- 图片路径中的 `&` 在 XML 中应写成 `&amp;`；
- 确认图片文件真实存在。

### 翻页到最后一页后无法继续

- 检查 `IsLoop` 是否为 `true`，`false` 时翻到边界会停止。

### 阴影效果不明显

- 调整 `ShadowLevel` 数值，通常 `0.5` 以上效果较明显；
- 若设为 `0`，则完全无阴影。

### 数据源内容没有生成多页

- 确认 `DataProvider` 中的数据源名称和表名正确；
- 确认数据源中有多条数据；
- 确认 `Item` 模板中使用了正确的 `{$变量名}` 绑定。

## 13.版本说明

- `IsLoop` 为较新版本新增属性，用于控制翻页循环行为。
- 若使用旧版本运行时，`IsLoop` 可能不被识别，建议升级到支持该属性的版本。

## 14.BookElement 与 EBookElement 的区别

两者都是以翻书交互方式展示内容的控件，主要区别如下：

| 对比项        | BookElement           | EBookElement               |
| ------------- | --------------------- | -------------------------- |
| 控件类型      | `BookElement`         | `EBookElement`             |
| 所属 DLL      | `UI.Book.dll`         | `UI.EBook.dll`             |
| 渲染方式      | 基于 WPF 3D 翻页效果  | 基于自定义 Canvas 翻页效果 |
| 注册 ViewType | `BookElement`         | `EBookElement`             |
| 注册 TypeName | `UI.Book.BookControl` | `UI.EBook.EBookControl`    |

### 选择建议

- **BookElement**：适合需要逼真 3D 翻页效果的场景。
- **EBookElement**：适合需要更灵活页面容器（如 `XYContainerElement`）或自定义触摸热区的场景。

两者都支持 `Template + DataProvider`（数据驱动）和 `Item`（固定页面）。**推荐优先使用 `Template + DataProvider`**，固定页面再使用 `Item`。

### 配置示例

**BookElement（使用 Template + DataProvider）：**

```xml
<BookElement>
    <DataProvider>EBookData?CSTable=TEduBook5</DataProvider>
    <Items>
        <Template Left="0" Top="0" Width="671" Height="1080" TemplateID="Image">
            <XYContainerElement TrackingData="{$FileName}">
                <UIDisplay Left="0" Top="0" Width="671" Height="1080" />
                <Controls>
                    <ImageElement>
                        <UIDisplay Left="0" Top="0" Width="671" Height="1080" />
                        <ImageSource UriKind="Absolute">{$FullName}</ImageSource>
                    </ImageElement>
                </Controls>
            </XYContainerElement>
        </Template>
    </Items>
    <CustomerConfig>
        <Book IsCacheUI="True" IsLoop="true" ShadowLevel="0.6" Width="865" Height="665" />
    </CustomerConfig>
</BookElement>
```

**EBookElement（使用 Template + DataProvider）：**

```xml
<EBookElement>
    <DataProvider>EBookData?CSTable=TEduBook5</DataProvider>
    <Items>
        <Template Left="0" Top="0" Width="671" Height="1080" TemplateID="Image">
            <XYContainerElement TrackingData="{$FileName}">
                <UIDisplay Left="0" Top="0" Width="671" Height="1080" />
                <Controls>
                    <ImageElement>
                        <UIDisplay Left="0" Top="0" Width="671" Height="1080" />
                        <ImageSource UriKind="Absolute">{$FullName}</ImageSource>
                    </ImageElement>
                </Controls>
            </XYContainerElement>
        </Template>
    </Items>
    <CustomerConfig>
        <Book IsCacheUI="True" IsLoop="true" ShadowLevel="0.6" Width="865" Height="665" />
    </CustomerConfig>
</EBookElement>
```

> 注：两者 `CustomerConfig` 中的 `Book` 节点属性基本一致，如 `IsCacheUI`、`ShadowLevel`、`Width`、`Height` 等。新版本两者均可能支持 `IsLoop` 属性，具体以运行时版本为准。
