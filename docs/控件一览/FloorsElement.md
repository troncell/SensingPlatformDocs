# 楼层Floors控件（FloorsElement）

## 1.控件作用

楼层控件用于展示和切换多个楼层选项，通常与地图控件（如 `MapElement`）配合使用。控件会根据数据源动态生成楼层按钮，点击某个楼层按钮后会触发楼层切换事件，更新对应页面或控件中显示的楼层内容。

## 2.适用场景

- 楼宇导览系统中的楼层切换
- 地图控件配套楼层选择器
- 展厅、商场、园区等多楼层场景导航
- 需要单选互斥的选项列表

## 3.前置依赖

使用楼层控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `FloorsElement`；
3. 如需动态加载内容，需在 `Shell/Data/Data.xml` 中配置数据源并在页面中使用 `DataProvider`；
4. 若使用 `ToggleButton`，需确认 `ToggleButton` 已在 `UIControlDict.xml` 中注册。

## 4.控件UI效果

![Placeholder](../images/FloorsElement.png)

## 5.配置文件样例

```xml
<FloorsElement Name="floors">
      <UIDisplay Left="570" Top="1005" Width="1203" Height="85" IsShow="True" ZIndex="2"
        UsePercent="False" />
      <DataProvider>wyfData?CSTable=Floors</DataProvider>
      <Items>
        <Template Left="0" Top="20" Width="146" Height="58" TemplateID="11001">
          <ToggleButton>
            <UIDisplay Left="0" Top="0" Width="146" Height="58" IsShow="True" ZIndex="1"
              UsePercent="False" />
            <CustomerConfig>
              <ImageSource UriKind="Application">Shell\Data\wyfData\CacheData\{$Extends}</ImageSource>
              <ImageSourceChecked UriKind="Application">
                Shell\Data\wyfData\CacheData\{$ThumbnailImageUrl}</ImageSourceChecked>
              <CheckedEvent>
                <Event>
                  FloorIndexChangedEvent?TargetPageName=HomePage&TargetControlName=map&FloorId={$Id}</Event>
                <Event>ResetEvent?TargetPageName=HomePage&TargetControlName=ScaleBar</Event>
              </CheckedEvent>
              <GroupName>AAA</GroupName>
              <IsChecked>False</IsChecked>
            </CustomerConfig>
          </ToggleButton>
        </Template>
      </Items>
      <CustomerConfig>
        <Floors Orientation="horizontal" />
      </CustomerConfig>
    </FloorsElement>
```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对楼层控件：

- `Width` / `Height`：定义楼层按钮区域的大小；
- `ZIndex`：注意楼层按钮与地图等控件的层级关系；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`。

## 7.DataProvider 与 Items

### 动态数据源模式

通过 `DataProvider` 绑定数据源，数据源中的每一行会生成一个楼层按钮。

```xml
<DataProvider>wyfData?CSTable=Floors</DataProvider>
```

- `wyfData`：数据源实例名称，需在 `Shell/Data/Data.xml` 中定义；
- `CSTable=Floors`：数据表/集合名称；
- `Template` 中的 `{$Extends}`、`{$ThumbnailImageUrl}`、`{$Id}` 等变量需与数据源中的列名一致。

### 8.Template 属性

| 属性         | 必填 | 说明                         | 示例    |
| ------------ | ---- | ---------------------------- | ------- |
| `Left`       | 否   | 模板左上角位置               | `0`     |
| `Top`        | 否   | 模板左上角位置               | `20`    |
| `Width`      | 否   | 模板宽度                     | `146`   |
| `Height`     | 否   | 模板高度                     | `58`    |
| `TemplateID` | 否   | 模板标识，可用于条件模板匹配 | `11001` |

## 9.ToggleButton 配置

楼层控件通常使用 `ToggleButton` 作为楼层项。`ToggleButton` 支持两种状态：未选中（Unchecked）和已选中（Checked），同组内通常只有一个按钮处于选中状态。

### CustomerConfig 参数说明

| 属性/节点            | 必填 | 说明                                      | 示例                                                |
| -------------------- | ---- | ----------------------------------------- | --------------------------------------------------- |
| `ImageSource`        | 否   | 未选中状态下显示的图片                    | `Shell\Data\wyfData\CacheData\{$Extends}`           |
| `ImageSourceChecked` | 否   | 选中状态下显示的图片                      | `Shell\Data\wyfData\CacheData\{$ThumbnailImageUrl}` |
| `CheckedEvent`       | 否   | 选中时触发的事件集合                      | -                                                   |
| `GroupName`          | 否   | 分组名称，同组按钮互斥                    | `AAA`                                               |
| `IsChecked`          | 否   | 初始是否选中。`True` 选中，`False` 未选中 | `False`                                             |

### CheckedEvent

`CheckedEvent` 内可以配置一个或多个 `Event` 节点，当楼层按钮被选中时依次触发。

### 常用事件

| 事件                     | 说明                                       | 示例                                                                                         |
| ------------------------ | ------------------------------------------ | -------------------------------------------------------------------------------------------- |
| `FloorIndexChangedEvent` | 楼层切换事件，通常用于通知地图控件切换楼层 | `FloorIndexChangedEvent?TargetPageName=HomePage&amp;TargetControlName=map&amp;FloorId={$Id}` |
| `ResetEvent`             | 重置事件，通常用于重置缩放条、地图视角等   | `ResetEvent?TargetPageName=HomePage&amp;TargetControlName=ScaleBar`                          |

## 10.CustomerConfig 参数说明

### Floors 节点

| 属性          | 必填 | 说明                                                 | 示例         |
| ------------- | ---- | ---------------------------------------------------- | ------------ |
| `Orientation` | 否   | 楼层按钮排列方向。`horizontal` 横向，`vertical` 纵向 | `horizontal` |

## 11.UIControlDict.xml 添加楼层控件

如果使用楼层控件，需要在 `UIControlDict.xml` 中注册 `FloorsElement` 和 `ToggleButton`：

```xml
<!--UI.Common 控件包-->
<Element ViewType="FloorsElement" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.FloorsControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.FloorsViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>

<Element ViewType="ToggleButton" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.ToggleButtonControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.ToggleButtonViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

> 注：`TypeName` 中的具体类名以实际 DLL 中的类型为准。

## 12.部署说明

1. 确认项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `FloorsElement` 和 `ToggleButton`；
3. 如需动态数据，在 `Shell/Data/Data.xml` 中配置数据源，并在页面中使用 `DataProvider`；
4. 在页面 XML 中使用 `FloorsElement`，配置 `UIDisplay`、`DataProvider`、`Items`、`ToggleButton` 和 `CustomerConfig`；
5. 在目标页面或地图控件中处理 `FloorIndexChangedEvent` 事件。

## 13.常见问题

### 楼层按钮不显示

- 检查 `DataProvider` 中的数据源名称和表名是否正确；
- 检查 `ImageSource` 和 `ImageSourceChecked` 的 `UriKind` 和路径是否正确；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`。

### 楼层按钮无法选中

- 检查 `ToggleButton` 是否在 `UIControlDict.xml` 中注册；
- 检查 `GroupName` 是否配置正确；
- 检查是否有上层控件拦截了点击事件。

### 点击楼层后地图没有切换

- 检查 `FloorIndexChangedEvent` 中的 `TargetPageName` 和 `TargetControlName` 是否正确；
- 检查 `FloorId` 参数是否正确；
- 检查目标地图控件是否处理了 `FloorIndexChangedEvent`。

### 多个楼层按钮同时选中

- 检查 `GroupName` 是否相同，同组按钮应互斥；
- 检查 `IsChecked` 初始状态是否配置正确。

### 数据源内容没有生成多个楼层按钮

- 确认 `DataProvider` 中的数据源名称和表名正确；
- 确认数据源中有多条数据；
- 确认 `Template` 中使用了正确的 `{$变量名}` 绑定。
