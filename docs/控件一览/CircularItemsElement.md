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
    <!-- 旋转控件：环形轨道 + 菜单项 -->
    <CircularItemsElement Name="CircularItems">
      <UIDisplay Left="222" Top="1135" Width="1370" Height="1489" IsShow="True" ZIndex="3" UsePercent="False" ClipToBounds="False" />
      <Items IsCacheUI="True">
        <ImageButton>
          <UIDisplay Left="1272" Top="17" Width="461" Height="460" IsShow="True" ZIndex="1" UsePercent="False" />
          <ImageSource UriKind="Application">Shell\Pages\CircularItems\resource\社会责任.png</ImageSource>
          <ClickEvent>Navigate?Page=qiyePage</ClickEvent>
        </ImageButton>

        <ImageButton>
          <UIDisplay Left="1180" Top="1255" Width="661" Height="661" IsShow="True" ZIndex="1" UsePercent="False" />
          <ImageSource UriKind="Application">Shell\Pages\CircularItems\resource\主要业绩介绍.png</ImageSource>
          <ClickEvent>Navigate?Page=SolutionPage</ClickEvent>
        </ImageButton>

        <ImageButton>
          <UIDisplay Left="450" Top="1480" Width="461" Height="461" IsShow="True" ZIndex="1" UsePercent="False" />
          <ImageSource UriKind="Application">Shell\Pages\CircularItems\resource\文化风貌.png</ImageSource>
          <ClickEvent>Navigate?Page=ztPage</ClickEvent>
        </ImageButton>

        <ImageButton>
          <UIDisplay Left="-133" Top="-414" Width="460" Height="460" IsShow="True" ZIndex="1" UsePercent="False" />
          <ImageSource UriKind="Application">Shell\Pages\CircularItems\resource\实体模型互动.png</ImageSource>
          <ClickEvent>Navigate?Page=RotatePage</ClickEvent>
        </ImageButton>
      </Items>

      <CustomerConfig>
        <!-- 背景图片(旋转的底图) -->
        <BackgroundImage UriKind="Application" Directory="Shell\Pages\CircularItems\resource\组 11.png" />
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
  - **重要**：`CustomerConfig/BackgroundImage` 会按此区域的 `Width/Height` 拉伸填充。若想让底图不变形，建议将 `Width/Height` 设为底图的原尺寸或等比例尺寸。
- `ZIndex`：若页面上有悬浮按钮或弹出层，注意层级关系；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`；
- `ClipToBounds`：是否裁剪超出控件边界的内容。当子项（如按钮）需要显示到 `CircularItemsElement` 边界之外时，必须设为 `False`，否则会被裁剪。

## 6.1 控件尺寸、旋转半径与底图变形

配置 `CircularItemsElement` 的尺寸时需要同时考虑三件事：

| 尺寸选择 | 底图效果 | 子项效果 | 适用场景 |
| --- | --- | --- | --- |
| 与底图尺寸一致 | 不变形，刚好填满 | 子项可能超出边界，需配合 `ClipToBounds="False"` | 底图是环形轨道，子项在轨道内外 |
| 比底图大很多 | 底图被拉伸放大 | 旋转半径大，子项不易被裁剪 | 底图可拉伸，或希望整体放大 |
| 比底图小 | 底图被压缩 | 旋转半径小，子项可能拥挤 | 一般不推荐 |

建议做法：先让 `UIDisplay` 的 `Width/Height` 等于底图原尺寸，再根据需要微调。子项超出边界时加 `ClipToBounds="False"`。

## 7.Items 说明

`Items` 是旋转控件的子元素集合，每个子元素会围绕中心点排列。支持以下控件：

- `XYContainerElement`：常用，用于包裹 `ImageButton`、`TextElement` 等子控件；
- `ImageButton`：可直接作为旋转项；
- `TextElement`：用于显示文字标签；
- 其他简单控件。

### 7.1 子项坐标说明

`Items` 内子控件的 `Left/Top` 是**相对于 `CircularItemsElement` 左上角的偏移量**，允许为负数。整个子项会以 `CircularConfig` 的 `CenterX/CenterY` 为圆心做整体旋转。

示例中的 `Left="-133" Top="-414"` 表示该按钮位于控件区域的左上方之外，配合 `ClipToBounds="False"` 才能完整显示。

### 7.2 Items 属性

| 属性        | 必填 | 说明                                                 | 示例   |
| ----------- | ---- | ---------------------------------------------------- | ------ |
| `IsCacheUI` | 否   | 是否缓存子元素 UI。`True` 提升性能，`False` 节省内存 | `True` |

## 8.CustomerConfig 参数说明

### 8.1BackgroundImage 节点

| 属性        | 必填 | 说明                 | 示例                               |
| ----------- | ---- | -------------------- | ---------------------------------- |
| `UriKind`   | 是   | 背景图片路径解析方式 | `Application`                      |
| `Directory` | 是   | 背景图片路径         | `Shell\Pages\CircularItems\resource\组 11.png` |

- `UriKind="Project"` 表示路径相对于 `Shell` 文件夹，不需要加 `Shell\` 前缀；`UriKind="Application"` 表示路径相对于应用启动目录，需要带 `Shell\` 前缀。
- **注意**：这里用的是 `Directory` 属性，不是平时常见的 `<ImageSource>` 节点。
- 背景图片会作为旋转底图显示在所有旋转项的下方，并且会按 `UIDisplay` 的 `Width/Height` 拉伸填充。若要保持原图比例不变形，请将 `UIDisplay` 的 `Width/Height` 设置为底图原尺寸。

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

计算实际圆心像素位置：

```
圆心X = Left + Width × CenterX
圆心Y = Top + Height × CenterY
```

当 `UIDisplay` 的 `Width/Height` 与底图尺寸一致，并设置 `CenterX="0.5" CenterY="0.5"` 时，圆心即为底图中心，旋转时不会晃动。

## 9.UIControlDict.xml 添加旋转控件

如果使用旋转控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<Element ViewType="CircularItemsElement" AssemblyFile="UI.CircularPanel.dll" TypeName="UI.CircularPanel.CircularItemsControl, UI.CircularPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.CircularPanel.dll" TypeName="UI.CircularPanel.CircularItemsElementViewModel, UI.CircularPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 10.整体旋转写法（固定子项相对位置）

如果需要让底图和多个子项保持固定的相对位置一起旋转，可以把它们全部放在一个 `<Item>` / `<XYContainerElement>` 内。这种写法下，子项的 `Left/Top` 是相对于 `XYContainerElement` 的绝对坐标，整个组合会围绕 `CircularConfig` 的 `CenterX/CenterY` 旋转。

```xml
<CircularItemsElement Name="CircularItems">
  <UIDisplay Left="0" Top="0" Width="2160" Height="3840" IsShow="True" ZIndex="3" UsePercent="False" />
  <Items IsCacheUI="True">
    <Item Left="0" Top="0" Width="2160" Height="3840" ZIndex="1" TemplateID="10001" CanRotate="True">
      <XYContainerElement>
        <UIDisplay Left="0" Top="0" Width="2160" Height="3840" />
        <Controls>
          <ImageElement Name="Background">
            <UIDisplay Left="222" Top="1135" Width="1370" Height="1489" IsShow="True" ZIndex="1" UsePercent="False" />
            <ImageSource UriKind="Application">Shell\Pages\CircularItems\resource\组 11.png</ImageSource>
          </ImageElement>
          <ImageButton>
            <UIDisplay Left="1494" Top="1152" Width="461" Height="460" IsShow="True" ZIndex="1" UsePercent="False" />
            <ImageSource UriKind="Application">Shell\Pages\CircularItems\resource\社会责任.png</ImageSource>
            <ClickEvent>Navigate?Page=qiyePage</ClickEvent>
          </ImageButton>
          <!-- 其他按钮... -->
        </Controls>
      </XYContainerElement>
    </Item>
  </Items>
  <CustomerConfig>
    <AutoRotate IsAutoPlay="True" MaxEllapsedTime="2000" RotationSpeed="10" />
    <CircularConfig Damping="0.1" Debug="True" CenterX="0.42" CenterY="0.49" />
  </CustomerConfig>
</CircularItemsElement>
```

注意：`CenterX/CenterY` 需要根据底图中心计算。例如底图 `Left="222" Width="1370"`，则圆心 X 为 `222 + 1370/2 = 907`，相对全屏 `2160` 即为 `0.42`。

## 11.部署说明

1. 将 `UI.CircularPanel.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 在页面 XML 中使用 `CircularItemsElement`，配置 `UIDisplay`、`Items` 和 `CustomerConfig`。

## 12.常见问题

### 旋转项不显示

- 检查 `Items` 内子控件的 `UIDisplay` 和 `ImageSource` 是否正确；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查 `Items` 的 `IsCacheUI` 是否配置正确。

### 旋转项被裁剪

- 如果子项显示到 `CircularItemsElement` 边界之外，需要在 `UIDisplay` 上设置 `ClipToBounds="False"`。

### 背景图片太大/太小或变形

- 检查 `UIDisplay` 的 `Width/Height` 是否和底图原尺寸一致；
- `BackgroundImage` 会按 `UIDisplay` 的 `Width/Height` 拉伸填充，尺寸不一致会导致变形或缩放异常。

### 旋转时整体晃动/中心点偏移

- 调整 `CircularConfig` 的 `CenterX` 和 `CenterY`，使其与底图中心重合；
- 计算公式：`CenterX = (底图Left + 底图Width/2) / 控件Width`，`CenterY = (底图Top + 底图Height/2) / 控件Height`；
- 开启 `Debug="True"` 可查看中心位置辅助调试。

### 不自动旋转

- 检查 `AutoRotate` 的 `IsAutoPlay` 是否为 `True`；
- 检查 `MaxEllapsedTime` 是否设置合理；
- 检查 `RotationSpeed` 是否大于 `0`。

### 手动旋转后停不下来

- 调整 `CircularConfig` 的 `Damping` 数值，增大阻尼可让旋转更快停止。

### 背景图片不显示

- 检查 `BackgroundImage` 的 `UriKind` 是否正确，`Project` 路径不需要加 `Shell\` 前缀；
- 注意 `BackgroundImage` 用的是 `Directory` 属性，不是 `ImageSource` 节点；
- 检查图片文件是否存在；
- 检查 `ZIndex` 是否被旋转项遮挡。
