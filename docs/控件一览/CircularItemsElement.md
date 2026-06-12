# 旋转控件（CircularItemsElement）

## 1.控件作用

旋转控件用于将配置的多个子控件围绕某个中心点排列，并支持自动或手动旋转。常用于制作环形菜单、旋转导航、产品展示轮盘等交互效果。

## 2.适用场景

- 环形导航菜单
- 旋转展示产品或功能入口
- 展厅互动转盘
- 围绕中心图标的放射状布局

## 3.前置依赖

使用旋转控件前，必须满足以下条件：

1. 项目目录中存在 `UI.CircularPanel.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `CircularItemsElement`；
3. `Items` 内放置需要旋转展示的子控件。

## 4.控件 UI 效果

控件将子元素围绕中心点均匀分布，可以自动缓慢旋转，也可以由用户拖拽旋转。

<img style="width:200px;height:350px" src="image/CircularItemsElement/1762413423947.png" alt="输入图片说明" />

## 5.配置文件样例

```xml
<CircularItemsElement >
	<UIDisplay Left="200" Top="700" Width="1600" Height="1600" IsShow="True" ZIndex="4" UsePercent="false" />
	<Items IsCacheUI="True">
      <!-- Items下支持现有的XYContainerElement、ImageButton、TextElement等控件 -->
			<XYContainerElement>
				<UIDisplay Left="0" Top="0" Width="461" Height="460" />
				<Controls>
					<ImageButton>
						<UIDisplay Left="0" Top="0" Width="461" Height="460" IsShow="True" ZIndex="1" UsePercent="False"/>
						<ImageSource UriKind="Application">Shell\Pages\AllPage\resource\社会责任.png</ImageSource>
						<ClickEvent>
							<Event>Navigate?Page=FirstPage</Event>
						</ClickEvent>
					</ImageButton>
				</Controls>
			</XYContainerElement>

			<XYContainerElement>
				<UIDisplay Left="0" Top="0" Width="461" Height="460" />
				<Controls>
					<ImageButton>
						<UIDisplay Left="0" Top="0" Width="461" Height="461" IsShow="True" ZIndex="2" UsePercent="False"/>

						<ImageSource UriKind="Application">Shell\Pages\AllPage\resource\文化风貌.png</ImageSource>

						<ClickEvent>
							<Event>Navigate?Page=SecondPage</Event>
						</ClickEvent>
					</ImageButton>
				</Controls>
			</XYContainerElement>

			<XYContainerElement>
				<UIDisplay Left="500" Top="0" Width="461" Height="460" />
				<Controls>
					<ImageButton>
						<UIDisplay Left="0" Top="0" Width="661" Height="661" IsShow="True" ZIndex="1" UsePercent="False"/>

						<ImageSource UriKind="Application">Shell\Pages\AllPage\resource\主要业绩介绍.png</ImageSource>

						<ClickEvent>
							<Event>Navigate?Page=ThirdPage</Event>
						</ClickEvent>
					</ImageButton>
				</Controls>
			</XYContainerElement>
			<XYContainerElement>
				<UIDisplay Left="600" Top="600" Width="461" Height="460"/>
				<Controls>
					<ImageButton>
						<UIDisplay Left="0" Top="0" Width="460" Height="460" IsShow="True" ZIndex="1" UsePercent="False"/>

						<ImageSource UriKind="Application">Shell\Pages\AllPage\resource\实体模型互动.png</ImageSource>

						<ClickEvent>
							<Event>Navigate?Page=FourPage</Event>
						</ClickEvent>
					</ImageButton>
				</Controls>
			</XYContainerElement>
	</Items>
	<CustomerConfig>
    <!-- 背景图片(旋转的底图) -->
		<BackgroundImage UriKind="Project" Directory="Pages\AllPage\resource\组 11.png"></BackgroundImage>
    <!-- 自动旋转相关 -->
		<AutoRotate IsAutoPlay="True" MaxEllapsedTime="2000" RotationSpeed="10" />
    <!-- 配置旋转元素的中心点及阻尼 -->
		<CircularConfig Damping="0.1" Debug="True" CenterX="0.5" CenterY="0.5" />
	</CustomerConfig>

</CircularItemsElement>

```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对旋转控件：

- `Width` / `Height`：定义旋转控件的显示区域，通常建议设置为正方形或足够大的区域；
- `ZIndex`：若页面上有悬浮按钮或弹出层，注意层级关系；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`。

## 7.Items 说明

`Items` 是旋转控件的子元素集合，每个子元素会围绕中心点排列。支持以下控件：

- `XYContainerElement`：常用，用于包裹 `ImageButton`、`TextElement` 等子控件；
- `ImageButton`：可直接作为旋转项；
- `TextElement`：用于显示文字标签；
- 其他简单控件。

### 7.1Items 属性

| 属性        | 必填 | 说明                                                 | 示例   |
| ----------- | ---- | ---------------------------------------------------- | ------ |
| `IsCacheUI` | 否   | 是否缓存子元素 UI。`True` 提升性能，`False` 节省内存 | `True` |

## 8.CustomerConfig 参数说明

### 8.1BackgroundImage 节点

| 属性        | 必填 | 说明                 | 示例                               |
| ----------- | ---- | -------------------- | ---------------------------------- |
| `UriKind`   | 是   | 背景图片路径解析方式 | `Project`                          |
| `Directory` | 是   | 背景图片路径         | `Pages\AllPage\resource\组 11.png` |

- `UriKind="Project"` 表示路径相对于 `Shell` 文件夹，不需要加 `Shell\` 前缀。
- 背景图片会作为旋转底图显示在所有旋转项的下方。

### 8.2AutoRotate 节点

| 属性              | 必填 | 说明                                                     | 示例   |
| ----------------- | ---- | -------------------------------------------------------- | ------ |
| `IsAutoPlay`      | 否   | 是否自动旋转                                             | `True` |
| `MaxEllapsedTime` | 否   | 加载完成或手动旋转停止后，等待多久开始自动旋转，单位毫秒 | `2000` |
| `RotationSpeed`   | 否   | 自动旋转速度                                             | `10`   |

### 8.3CircularConfig 节点

| 属性      | 必填 | 说明                                                             | 示例   |
| --------- | ---- | ---------------------------------------------------------------- | ------ |
| `Damping` | 否   | 阻尼系数，取值范围 `0 ~ 1`。系数越大，手动旋转松手后转动距离越短 | `0.1`  |
| `Debug`   | 否   | 是否显示中心位置调试信息                                         | `True` |
| `CenterX` | 否   | 圆心横坐标，相对控件区域的比例。`0.5` 表示中心                   | `0.5`  |
| `CenterY` | 否   | 圆心纵坐标，相对控件区域的比例。`0.5` 表示中心                   | `0.5`  |

## 9.UIControlDict.xml 添加旋转控件

如果使用旋转控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<Element ViewType="CircularItemsElement" AssemblyFile="UI.CircularPanel.dll" TypeName="UI.CircularPanel.CircularItemsControl, UI.CircularPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.CircularPanel.dll" TypeName="UI.CircularPanel.CircularItemsElementViewModel, UI.CircularPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 10.部署说明

1. 将 `UI.CircularPanel.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 在页面 XML 中使用 `CircularItemsElement`，配置 `UIDisplay`、`Items` 和 `CustomerConfig`。

## 11.常见问题

### 旋转项不显示

- 检查 `Items` 内子控件的 `UIDisplay` 和 `ImageSource` 是否正确；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查 `Items` 的 `IsCacheUI` 是否配置正确。

### 不自动旋转

- 检查 `AutoRotate` 的 `IsAutoPlay` 是否为 `True`；
- 检查 `MaxEllapsedTime` 是否设置合理；
- 检查 `RotationSpeed` 是否大于 `0`。

### 手动旋转后停不下来

- 调整 `CircularConfig` 的 `Damping` 数值，增大阻尼可让旋转更快停止。

### 旋转中心位置不对

- 调整 `CircularConfig` 的 `CenterX` 和 `CenterY`，`0.5` 表示控件区域的中心；
- 开启 `Debug="True"` 可查看中心位置辅助调试。

### 背景图片不显示

- 检查 `BackgroundImage` 的 `UriKind` 是否正确，`Project` 路径不需要加 `Shell\` 前缀；
- 检查图片文件是否存在；
- 检查 `ZIndex` 是否被旋转项遮挡。
