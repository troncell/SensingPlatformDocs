# 公用内容讲解（CommonElement）

Troncell 平台上的所有可交互元素都可以分解为 Troncell 的功能控件。所有控件要想在页面中生效，都需要在页面 XML 配置文件中按照规范进行声明。

本文档讲解所有控件共用的配置片段，包括 `UIDisplay`、`ImageSource` / `FileSource`、`DataProvider` 和 `Items`。

## 1.XML 通用规则

### 1.1大小写敏感

SensingPlatform 的 XML 配置是大小写敏感的。例如 `ViewType="ImageElement"` 有效，而 `viewtype="imageelement"` 会在运行时失败。

### 1.2特殊字符转义

事件 URL 和文本内容中若包含以下特殊字符，需要进行 XML 实体转义：

| 字符 | 转义写法 | 说明                      |
| ---- | -------- | ------------------------- |
| `&`  | `&amp;`  | 与号，事件 URL 参数分隔符 |
| `<`  | `&lt;`   | 小于号                    |
| `>`  | `&gt;`   | 大于号                    |
| `"`  | `&quot;` | 双引号                    |
| `'`  | `&apos;` | 单引号                    |

示例：

```xml
<!--正确-->
<ClickEvent>Navigate?Page=HomePage&Args=imageButton</ClickEvent>

<!--错误-->
<ClickEvent>Navigate?Page=HomePage&Args=imageButton</ClickEvent>
```

---

## 2.UIDisplay 片段讲解

`UIDisplay` 用于控件的定位、大小、层级和显示控制，是几乎每个控件都必须配置的节点。

### 2.1属性说明

| 属性               | 必填 | 说明                                                          | 示例    |
| ------------------ | ---- | ------------------------------------------------------------- | ------- |
| `Left`             | 否   | 控件左上角距离父容器左边框的距离，单位像素或百分比            | `0`     |
| `Top`              | 否   | 控件左上角距离父容器上边框的距离，单位像素或百分比            | `0`     |
| `Width`            | 否   | 控件宽度，单位像素或百分比                                    | `1920`  |
| `Height`           | 否   | 控件高度，单位像素或百分比                                    | `1080`  |
| `IsShow`           | 否   | 是否显示。`True` 显示，`False` 隐藏                           | `True`  |
| `ZIndex`           | 否   | 控件层级，数值越大越在上层                                    | `1`     |
| `UsePercent`       | 否   | 是否按比例布局。`True` 按父容器比例，`False` 按实际像素       | `False` |
| `Opacity`          | 否   | 透明度，`0` 完全透明，`1` 完全不透明                          | `1`     |
| `IsHitTestVisible` | 否   | 是否可穿透点击。`True` 点击可穿透到下层控件，`False` 不可穿透 | `True`  |
| `IsUseCache`       | 否   | 是否缓存控件 UI。`True` 缓存，`False` 不缓存                  | `False` |
| `ClipToBounds`     | 否   | 是否裁剪超出控件边界的内容。`True` 裁剪，`False` 不裁剪       | `False` |
| `Rotate`           | 否   | 图片旋转角度，单位度。所有图片角度一致时可设置                | `0`     |
| `RotateRandom`     | 否   | 图片角度是否随机显示                                          | `False` |
| `LowRotateRange`   | 否   | 随机旋转的最小角度                                            | `-10`   |
| `HighRotateRange`  | 否   | 随机旋转的最大角度                                            | `10`    |

### 2.2属性详细说明

- **Left / Top**：控件在父容器中的左上角坐标。当 `UsePercent="True"` 时，值为 `0` ~ `1` 之间的比例；当 `UsePercent="False"` 时，值为像素。
- **Width / Height**：控件的尺寸。当 `UsePercent="True"` 时，按父容器宽高比例计算；当 `UsePercent="False"` 时，按实际像素计算。
- **IsShow**：控制控件是否可见。隐藏时控件不渲染，但仍可能占用布局空间（取决于控件实现）。
- **ZIndex**：决定控件在页面上的叠放顺序。数值越大越靠上，容易被用户看到和点击。
- **UsePercent**：开启后，`Left`、`Top`、`Width`、`Height` 均按父容器尺寸的比例解析。
- **Opacity**：设置控件整体透明度。`0` 完全透明，`1` 完全不透明。
- **IsHitTestVisible**：`True` 时，点击事件会穿透该控件到达下层；`False` 时，该控件会拦截点击事件。
- **IsUseCache**：开启缓存可提升渲染性能，但会占用更多内存。内容频繁变化时建议关闭。
- **ClipToBounds**：开启后，子控件超出父容器边界部分会被裁剪；关闭则允许子控件超出边界显示。
- **Rotate**：统一设置所有内容的旋转角度。
- **RotateRandom / LowRotateRange / HighRotateRange**：开启随机旋转后，内容会在最小和最大角度范围内随机旋转。

### 2.3示例

```xml
<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="False" />
```

```xml
<UIDisplay Left="0" Top="0" Width="300" Height="600" IsShow="True" ZIndex="7" UsePercent="False" Opacity="1" IsUseCache="True" RotateRandom="False" LowRotateRange="-10" HighRotateRange="10" />
```

---

## 3.ImageSource、FileSource 片段讲解

`ImageSource` 和 `FileSource` 用于配置图片、文件、视频等资源的路径。两者配置含义相同，仅在部分控件中使用不同的节点名。

### 3.1UriKind 说明

| UriKind       | 路径基准                                           | 典型路径                               | 适用场景                              |
| ------------- | -------------------------------------------------- | -------------------------------------- | ------------------------------------- |
| `Relative`    | 当前 XML 文件所在目录                              | `resource\bg.png`、`test.jpg`          | 页面同级目录下的资源                  |
| `Application` | 应用程序启动目录（`TronSensingShow.exe` 所在目录） | `Shell\Pages\HomePage\resource\bg.png` | 项目 `Shell/` 或 `Resource/` 下的资源 |
| `Project`     | `Shell` 文件夹                                     | `Pages\HomePage\resource\bg.png`       | 省略 `Shell\` 前缀的路径              |
| `Absolute`    | 物理磁盘绝对路径                                   | `C:\Images\bg.png`                     | 外部磁盘、U盘、网络路径               |
| `Web`         | HTTP/HTTPS 地址                                    | `https://example.com/image.png`        | 在线资源                              |

### 3.2示例

#### Application 路径

相对于应用启动目录，路径以 `Shell\` 开头：

```xml
<ImageElement>
    <ImageSource UriKind="Application">Shell\Pages\CirclePage\test.jpg</ImageSource>
</ImageElement>
```

#### Relative 路径

相对于当前 XML 文件所在目录：

```xml
<ImageElement>
    <ImageSource UriKind="Relative">lianiankan.png</ImageSource>
</ImageElement>
```

#### Absolute 路径

使用真实物理路径：

```xml
<ImageElement>
    <ImageSource UriKind="Absolute">C:\Images\bg.png</ImageSource>
</ImageElement>
```

### 3.3常见错误

- `Application` 路径缺少 `Shell\` 前缀；
- `Project` 路径多写了 `Shell\` 前缀；
- `Relative` 路径指向了不存在的同级目录；
- 路径中包含多余空格，如 `Shell\ Pages\...`。

---

## 4.DataProvider 连接数据库配置片段讲解

描述：

`DataProvider` 用于将页面控件与后台数据源关联，实现动态数据绑定。具体如何进行连接数据库配置，请参照文档《Data 配置》。

### 4.1语法格式

```
DataSourceName?CSTable=TableName&Where=[条件]&Orderby=[排序]
```

### 4.2示例

```xml
<DataProvider>FishEyeData?CSTable=FishEye</DataProvider>
```

### 4.3参数说明

| 参数             | 说明                                                                         | 示例                      |
| ---------------- | ---------------------------------------------------------------------------- | ------------------------- |
| `DataSourceName` | 数据源名称，对应 `Data.xml` 中 `<ExcelData Name="FishEyeData">` 的 `Name` 值 | `FishEyeData`             |
| `CSTable`        | 固定参数，表示以表的形式查询                                                 | `CSTable=FishEye`         |
| `TableName`      | 数据表名称，对应 `Data.xml` 中 `<Table Name="FishEye">` 的 `Name` 值         | `FishEye`                 |
| `Where`          | 可选，筛选条件，使用方括号                                                   | `Where=[Name like %key%]` |
| `Orderby`        | 可选，排序条件，使用方括号                                                   | `Orderby=[DESC Name]`     |

### 4.4详细说明

- `DataSourceName` 和 `TableName` 必须与实际 `Data.xml` 中配置的名称完全一致；
- 多个参数之间使用 `&amp;` 分隔；
- 在 `Template` 内可以通过 `{$列名}` 绑定数据源的列。

示例：

```xml
<DataProvider>FishEyeData?CSTable=FishEye&Where=[Name like %test%]&Orderby=[DESC Name]</DataProvider>
```

---

## 5.Items 片段讲解

描述：

Items 是相当于一个容器，，用于包含子控件。不同控件根据业务需要，在 `Items` 下有四种常见配置方式。如 ImageElement、ImageButton、TextElement 等

一般在 Items 下会有如下四中配置方式 :

### 5.1方式一：放置多个 Item 节点

放置多个 Item 节点，适用于固定数量的子项目。通常在 Items 中列举出有多少个子项目就配置多少个 Item 节点，相当于一个子级别的容器，里面也可以含有一个或多个简单的控件，如
ImageElement、ImageButton、TextElement 等

```xml
<!--放置Item-->
<Items>
<Item>
<!--放置简单的控件ImageButton，如何配置控件请参考基本控件配置中ImageButton控件的
配置方法-->

<ImageButton>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">Shell \FishEyes\KPIRedA.png</ImageSource>
<ClickEvent>Navigate?Page=HomePage&Args=imageButton</ClickEvent>
</ImageButton>
</Item>
</Items>
```

### 5.2方式二：放置 Template 节点

适用于动态数据绑定场景。`Template` 作为模板，配合 `DataProvider` 使用，根据数据行数动态生成子项。
放置多个 Template，用于使用进行动态的配置，显示出不同的效果，相当于一个子级别的容器，若用户指定节点个数而不是从数据库中动态查询节点个数,则不需要配置此项，里面也可以含有一个或多个简单的控件，如 ImageElement、ImageButton、TextElement 等

```xml
<!--放置Template-->
<Items>
<Template>
<!--放置简单的控件ImageElement，如何配置控件请参考基本控件配置中ImageElement控件
的配置方法-->

<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">{$IconPath}</ImageSource>
<ClickEvent>{$EventAction}?Page={$NavigatePage}&Args=imageButton</ClickEvent>
</ImageElement>
</Template>
</Items>
```

### 5.3方式三：直接放置简单控件

适用于不需要分组的简单场景，直接在 `Items` 下放置 `ImageElement`、`ImageButton`、`TextElement` 等控件。

```xml
<!--放置简单的控件ImageElement，如何配置控件请参考基本控件配置中ImageElement控件
的配置方法-->
<Items>
<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">Shell\ FishEyeData\ KPIRedA.png</ImageSource>
</ImageElement>
</Items>
```

### 5.4方式四：混合配置

也可以在一个 `Items` 内同时混合使用 `Template`、`Item` 和直接控件。

```xml
<Items>
<Template>
<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">{$IconPath}</ImageSource>
<ClickEvent>{$EventAction}?Page={$NavigatePage}&Args=imageButton</ClickEvent>
</ImageElement>
</Template>
<ImageElement>
<UIDisplay Left="100" Top="100" Width="392" Height="390" IsShow="True" ZIndex="1"
UsePercent="False"/>
<ImageSource UriKind="Application">Shell\Data\ KPIRedA.png</ImageSource>
</ImageElement>
</Items>
```

### 5.5使用建议

| 方式       | 适用场景                 |
| ---------- | ------------------------ |
| `Item`     | 固定数量的子项目         |
| `Template` | 数据源动态生成的子项目   |
| 直接控件   | 简单固定内容             |
| 混合       | 既有固定内容又有动态内容 |

---

## 6.全局事件键

在 `ClickEvent` 等事件 URL 中，以下键名具有全局含义，不要与具体事件的参数重名：

| 键名                                  | 说明                        | 示例                         |
| ------------------------------------- | --------------------------- | ---------------------------- |
| `EDelay`                              | 延迟触发时间，单位毫秒      | `EDelay=1000`                |
| `TargetControl` / `TargetControlName` | 指定接收事件的目标控件      | `TargetControlName=PopItems` |
| `UriKind`                             | 路径解析模式                | `UriKind=Application`        |
| `Loop`                                | 循环次数，`-1` 表示无限循环 | `Loop=-1`                    |
| `StopLoop`                            | 停止循环                    | `StopLoop=True`              |
| `Async`                               | 是否异步执行                | `Async=true`                 |

---

## 7.常见问题

### 控件不显示

- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查 `Left`、`Top`、`Width`、`Height` 是否合理；
- 检查 `ZIndex` 是否被其他控件遮挡。

### 图片/文件找不到

- 检查 `UriKind` 是否选择正确；
- 检查路径是否包含多余空格；
- 使用 `Application` 时确认路径以 `Shell\` 或 `Resource\` 开头；
- 使用 `Project` 时确认没有加 `Shell\` 前缀。

### 数据绑定不生效

- 检查 `DataProvider` 中的数据源名称和表名是否正确；
- 检查 `Template` 中使用的 `{$列名}` 是否与数据源列名一致；
- 确认数据源中确实有数据。

### 事件 URL 解析报错

- 检查事件 URL 中的 `&` 是否已转义为 `&amp;`；
- 检查是否使用了全局保留键名作为自定义参数。

### 子控件超出父容器被裁剪

- 检查父控件的 `ClipToBounds` 是否为 `True`，若是且不需要裁剪，可设为 `False`；
- 检查子控件的 `Left`、`Top`、`Width`、`Height` 是否超出了父容器范围。
