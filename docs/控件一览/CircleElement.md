# 环形卡片控件（CircleElement）

## 1.控件作用

环形卡片控件以 360 度环绕滑块的方式展示图片列表。每个列表项以卡片形式分布在环形轨道上，支持用户拖拽或点击切换，常用于图片墙、产品展示、荣誉展示等场景。

## 2.适用场景

- 产品 360 度环绕展示
- 照片墙、荣誉墙
- 需要突出中心焦点的图片轮播
- 展厅互动展示墙

## 3.前置依赖

使用环形卡片控件前，必须满足以下条件：

1. 项目目录中存在 `UI.SweepPanel.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `CircleElement`；
3. 如需动态加载内容，需在 `Shell/Data/Data.xml` 中配置数据源并在页面中使用 `DataProvider`。

## 4.UI效果

<!-- <img alt="CircleElement Preview Image" src="../images/CircleElement.png" width="900"> -->

![Placeholder](../images/CircleElement.png)

## 5.配置文件样例

```xml
<!--Name 为控件在页面中的名字，为可选项-->
<CircleElement Name="CircleElement">
<!--参考控件公用片段CommonElement.md讲解中UIDisplay片段讲解-->
	<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="3" UsePercent="False" />
	<!--参考控件公用片段CommonElement.md讲解中DataProvide片段讲解-->
	<DataProvider>CirclePanelData?CSTable=Circle</DataProvider>
	<Items>
		<Template>
			<ImageButton Name="TestPageNav">
				<UIDisplay Left="100" Top="100" Width="150" Height="113" IsShow="True" ZIndex="1" UsePercent="False" />
				<ImageSource UriKind="Absolute">{$ImagePath}</ImageSource>
				<ClickEvent>Navigate?Page=TestPage&Args=imageButton</ClickEvent>
			</ImageButton>
		</Template>
	</Items>
	<!-- 放置CustomerConfig片段 -->
	<CustomerConfig>
		<!-- 放置CirClePanel片段 -->
		<CirClePanel>
			<!--一圈最多显示多少个卡片-->
			<MaxItemCount>17</MaxItemCount>
			<!-- 环形圈半径 -->
			<Radius>500</Radius>
			<!-- 倾斜角度 -->
			<CameraAngle>45</CameraAngle>
			<!-- 梯形角度 -->
			<ZoomAngle>0</ZoomAngle>
			<!-- 中心点位置 -->
			<Center X="800" Y="500">
			</Center>
			<!-- 配置滑块倒影是否显示 -->
			<ShowShadow>true</ShowShadow>
			 <!--用户没有交互时，自动滚动时间间隔；若不需要自动滚动，去掉该节点即可-->
			<AutoScrollTime>00:00:14</AutoScrollTime>
			<!-- 滑动模式 横向：Horizontal，纵向：Vertical -->
			<ArrangeMode>Horizontal</ArrangeMode>
			<!-- 放置ClickSensity片段，配置点击灵明度 -->
			<ClickSensity>
				<!-- 最大响应时间，单位为毫秒 -->
				<MaxTime>800</MaxTime>
				<!-- 最小相应时间，单位为毫秒 -->
				<MinTime>2</MinTime>
			</ClickSensity>
		</CirClePanel>
	</CustomerConfig>
</CircleElement>

```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对环形卡片控件：

- `Width` / `Height`：定义控件在页面上的显示区域，建议覆盖整个页面或足够大的区域；
- `ZIndex`：若页面上有悬浮按钮或弹出层，注意层级关系；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`。

## 7.DataProvider 与 Items

### 7.1动态数据源模式

通过 `DataProvider` 绑定数据源，数据源中的每一行会生成一个环形卡片。

```xml
<DataProvider>CirclePanelData?CSTable=Circle</DataProvider>
```

- `CirclePanelData`：数据源实例名称，需在 `Shell/Data/Data.xml` 中定义；
- `CSTable=Circle`：数据表/集合名称；
- `Template` 中的 `{$ImagePath}` 等变量需与数据源中的列名一致。

### 7.2Template

`Items` 内使用 `Template` 作为卡片模板。`Template` 内部通常放置 `ImageButton`，用于显示图片并响应点击事件。

## 8.CustomerConfig 参数说明

### 8.1CirClePanel 节点

`CirClePanel` 用于设置整个环形 360 度展示的形态和动画效果。

| 参数             | 必填 | 说明                                                                    | 示例              |
| ---------------- | ---- | ----------------------------------------------------------------------- | ----------------- |
| `MaxItemCount`   | 否   | 环形一圈最多显示多少个卡片                                              | `17`              |
| `Radius`         | 否   | 环形圈的半径，单位像素                                                  | `500`             |
| `CameraAngle`    | 否   | 整个环形圈的倾斜角度                                                    | `45`              |
| `ZoomAngle`      | 否   | 环形圈的梯形角度，影响卡片远近透视效果                                  | `0`               |
| `Center`         | 否   | 环形圈的中心点位置                                                      | `X="800" Y="500"` |
| `ShowShadow`     | 否   | 卡片倒影是否显示。`true` 显示，`false` 不显示                           | `true`            |
| `AutoScrollTime` | 否   | 用户无交互时自动滚动的时间间隔，TimeSpan 格式；去掉该节点则停止自动滚动 | `00:00:14`        |
| `ArrangeMode`    | 否   | 滑动模式。`Horizontal` 横向，`Vertical` 纵向                            | `Horizontal`      |

### 8.2ClickSensity 节点

`ClickSensity` 用于设置环形圈的点击灵敏度。

| 参数      | 必填 | 说明                                                   | 示例  |
| --------- | ---- | ------------------------------------------------------ | ----- |
| `MaxTime` | 否   | 点击最大响应时间，单位毫秒。超过该时间视为拖拽而非点击 | `800` |
| `MinTime` | 否   | 点击最小响应时间，单位毫秒。低于该时间可能忽略点击     | `2`   |

### 8.3参数说明

- **MaxItemCount**：决定环形轨道上同时显示的卡片数量。如果数据项多于该值，多余项会在滚动时逐个替换显示。
- **Radius**：环形轨道的半径，单位像素。半径越大，卡片分布越稀疏。
- **CameraAngle**：环形的倾斜角度，模拟 3D 视角。`0` 表示正对平面，数值越大倾斜越明显。
- **ZoomAngle**：梯形角度，影响卡片的远近大小透视效果。
- **Center**：环形在控件显示区域内的中心点坐标。
- **ShowShadow**：是否显示卡片下方的倒影效果。
- **AutoScrollTime**：用户无操作时的自动滚动间隔。格式为 `HH:MM:SS`，例如 `00:00:14` 表示 14 秒。
- **ArrangeMode**：环形滑动方向，`Horizontal` 为水平方向，`Vertical` 为垂直方向。
- **MaxTime / MinTime**：用于区分点击和拖拽。手指或鼠标按下到抬起的时间在 MinTime 和 MaxTime 之间视为点击，否则视为拖拽滚动。

## 9.UIControlDict.xml 添加环形卡片控件

如果使用环形卡片控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<!--UI.SweepPanel 控件包-->
<Element ViewType="CircleElement" AssemblyFile="UI.SweepPanel.dll" TypeName="UI.SweepPanel.Ellipse.CirclePanelControl, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.SweepPanel.dll" TypeName="UI.SweepPanel.Ellipse.CirclePanelViewModel, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 10.部署说明

1. 将 `UI.SweepPanel.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 如需动态数据，在 `Shell/Data/Data.xml` 中配置数据源，并在页面中使用 `DataProvider`；
4. 在页面 XML 中使用 `CircleElement`，配置 `UIDisplay`、`DataProvider`、`Items` 和 `CustomerConfig`。

## 11.常见问题

### 卡片不显示

- 检查 `DataProvider` 中的数据源名称和表名是否正确；
- 检查 `ImageSource` 的 `UriKind` 和路径是否正确；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`。

### 点击卡片没反应

- 检查 `ClickEvent` 中的 `&` 是否已转义为 `&amp;`；
- 检查 `ClickSensity` 的 `MaxTime` 是否过小，导致拖拽和点击无法区分；
- 检查卡片是否被其他控件遮挡。

### 环形位置偏移

- 调整 `Center` 的 `X`、`Y` 坐标，使其位于控件显示区域的合适位置；
- 调整 `Radius` 大小，避免卡片超出显示区域。

### 自动滚动不生效

- 检查 `AutoScrollTime` 是否配置正确，格式为 `HH:MM:SS`；
- 若不需要自动滚动，应完全移除 `AutoScrollTime` 节点。

### 卡片显示过多或过少

- 调整 `MaxItemCount` 数值；
- 调整 `Radius` 和 `CameraAngle` 以获得更好的视觉效果。
