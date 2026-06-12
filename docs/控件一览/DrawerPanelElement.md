# 抽屉控件（DrawerPanelElement）

## 1.控件作用

抽屉控件以抽屉效果显示内容，支持拉出和推进两种交互状态。通常用于在有限空间内展示更多信息，用户可以通过点击或交互展开/收起抽屉内容。

## 2.适用场景

- 需要隐藏部分信息，点击后展开查看详情
- 页面空间有限，需要折叠展示内容
- 底部、侧边抽屉式信息面板
- 产品详情、介绍信息的折叠展示

## 3.前置依赖

使用抽屉控件前，必须满足以下条件：

1. 项目目录中存在抽屉控件 DLL（常见为 `UI.DrawerPanel.dll` 或 `UI.SweepPanel.dll`，以实际项目为准）；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `DrawerPanelElement`；
3. 准备好抽屉展开和收起时要显示的图片、文字等子控件资源。

## 4.控件 UI 效果

![Placeholder](../images/DrawerPanelElement.gif)

## 5.配置文件样例

```xml
<DrawerPanelElement>
    <UIDisplay Left="2" Top="575" Width="681" Height="380" IsShow="True" ZIndex="2" UsePercent="False" />
        <Controls>
            <XYContainerElement>
                <UIDisplay Left="0" Top="0" Width="681" Height="380" IsShow="True" ZIndex="1" UsePercent="False" />
                <Controls>
                    <ImageElement>
                     <UIDisplay Left="0" Top="0" Width="681" Height="380" IsShow="True"
                          ZIndex="1" UsePercent="False" />
                    <ImageSource UriKind="Application">
                          Shell\Pages\choutiPage\resource\drawerbg2.png</ImageSource>
                    </ImageElement>
                    <ImageElement name="introduce">
                    <UIDisplay Left="0" Top="0" Width="684" Height="148" IsShow="True"
                          ZIndex="1" UsePercent="False" />
                    <ImageSource UriKind="Application">
                          Shell\Pages\choutiPage\resource\introduce1.png</ImageSource>
                    </ImageElement>
                </Controls>
            </XYContainerElement>
        </Controls>
    <CustomerConfig>
        <DrawerPanel CollapseHeight="140" IsCollapse="True"></DrawerPanel>
    </CustomerConfig>
</DrawerPanelElement>

```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对抽屉控件：

- `Width` / `Height`：定义抽屉控件的完整展开尺寸；
- `ZIndex`：注意抽屉与其他控件的层级关系，展开时需要覆盖下层内容；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`。
-

## 7.Controls 子控件

`DrawerPanelElement` 的 `Controls` 节点用于放置抽屉的内容。常见做法：

- 使用 `XYContainerElement` 作为内容的根容器，便于整体布局；
- 在 `XYContainerElement` 内放置 `ImageElement`、`ImageButton`、`TextElement` 等控件；
- 子控件的 `Top`、`Left` 通常相对于 `DrawerPanelElement` 或内部容器定位。

> 注意：`DrawerPanelElement` 的 `Controls` 内不要出现重复的 `Name`，否则可能导致控件查找异常。

### CustomerConfig参数说明

#### DrawerPanel 节点

| 属性             | 必填 | 说明                                                        | 示例   |
| ---------------- | ---- | ----------------------------------------------------------- | ------ |
| `CollapseHeight` | 否   | 抽屉折叠（未拉出）状态时显示的高度                          | `140`  |
| `IsCollapse`     | 否   | 初始状态。`True` 初始折叠，可拉出；`False` 初始展开，可推进 | `True` |

#### 属性说明

- **CollapseHeight**：抽屉在折叠状态下显示的高度。例如总高度为 380，折叠高度为 140，则初始只显示顶部 140 像素的内容。
- **IsCollapse**：定义抽屉的初始状态和交互方向。
  - `True`：初始为折叠状态，点击或交互后展开到完整高度；
  - `False`：初始为展开状态，点击或交互后折叠到 `CollapseHeight`。

### 抽屉展开/收起行为

抽屉控件通常通过点击触发展开或收起：

- 当 `IsCollapse="True"` 时，抽屉初始处于折叠状态，显示 `CollapseHeight` 高度的内容；
- 用户点击抽屉区域后，抽屉展开到 `UIDisplay` 中定义的完整高度；
- 再次点击后，抽屉收回到 `CollapseHeight` 高度。

# 8.UIControlDict.xml 添加抽屉控件

如果使用抽屉控件，需要在 `UIControlDict.xml` 中注册。不同版本可能使用不同的 DLL，请根据实际项目选择：

### 注册方式一（UI.DrawerPanel.dll）

```
  <!--UI.DrawerPanel控件包-->
<Element ViewType="DrawerPanelElement" AssemblyFile="UI.DrawerPanel.dll" TypeName="UI.DrawerPanel.DrawerPanelControl, UI.DrawerPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.DrawerPanel.dll" TypeName="UI.DrawerPanel.DrawerPanelControlViewModel, UI.DrawerPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
<!--UI.DrawerPanel End-->
```

### 注册方式二（UI.SweepPanel.dll）

```xml
<!--UI.SweepPanel 控件包-->
<Element ViewType="DrawerPanelElement" AssemblyFile="UI.SweepPanel.dll" TypeName="UI.SweepPanel.DrawerPanel.DrawerPanelControl, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.SweepPanel.dll" TypeName="UI.SweepPanel.DrawerPanel.DrawerPanelControlViewModel, UI.SweepPanel, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
<!--UI.SweepPanel End-->
```

> 注：`TypeName` 中的具体类名以实际 DLL 中的类型为准。不同项目可能使用不同 DLL。

## 9.部署说明

1. 确认项目目录中存在抽屉控件 DLL；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 在页面 XML 中使用 `DrawerPanelElement`，配置 `UIDisplay`、`Controls` 和 `CustomerConfig`；
4. 确保抽屉内容的 `Name` 不重复，避免控件查找冲突。

## 10.常见问题

### 抽屉内容不显示

- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查子控件的 `ImageSource` 路径和 `UriKind` 是否正确；
- 检查 `ZIndex` 是否被其他控件遮挡；
- 检查 `Controls` 内子控件是否超出了 `DrawerPanelElement` 的边界。

### 抽屉无法展开/收起

- 检查 `IsCollapse` 是否配置正确；
- 检查 `CollapseHeight` 是否大于 0 且小于完整高度；
- 检查抽屉区域是否被上层控件遮挡导致点击事件无法响应。

### 折叠状态下内容显示不全

- 调整 `CollapseHeight` 的值，使其能够显示需要展示的内容；
- 检查子控件的位置，确保关键内容位于 `CollapseHeight` 范围内。

### 多个 DrawerPanelElement 同时存在时异常

- 检查不同 `DrawerPanelElement` 内部的子控件 `Name` 是否重复；
- 检查 `ZIndex` 设置，避免抽屉展开时互相遮挡。

### 抽屉展开时被父容器裁剪

- 检查父容器（如 `XYContainerElement`、`SequenceItemsElement`）是否启用了 `ClipToBounds`；
- 如果父容器裁剪了超出边界的内容，需要增大父容器高度或关闭裁剪。

## 11.版本说明

- 抽屉控件可能在不同项目中使用 `UI.DrawerPanel.dll` 或 `UI.SweepPanel.dll`；
- 配置时请确保 `UIControlDict.xml` 中的 `AssemblyFile` 和 `TypeName` 与实际 DLL 一致；
- XML 属性名大小写敏感，请使用 `Name` 而不是 `name`。
