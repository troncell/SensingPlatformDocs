# 相对布局控件（XYContainerElement）

## 1.控件作用

相对布局控件用于将多个基本控件组合成一个整体容器。容器内部使用 `Canvas` 进行绝对定位，子控件通过 `Left`、`Top`、`Width`、`Height` 属性确定位置和大小。当单个配置位置需要同时承载多个控件，或需要将一组相关控件作为一个整体进行管理时，可使用 `XYContainerElement`。

## 2.适用场景

- 将多个控件组合为一个整体页面区域
- 需要按百分比或像素精确布局的容器
- 作为弹窗、滚动内容、轮播项的内容容器
- 需要统一控制显示/隐藏的一组控件

## 3.前置依赖

`XYContainerElement` 是框架内置控件，由 `SensingPlatform.Foundation` 提供，无需额外程序集，但需确保：

1. `SensingPlatform.Foundation.dll` 存在于项目目录；
2. 内部使用的子控件已在 `SysConfig/UIControlDict.xml` 中注册。

## 4.配置文件样例

```xml
<XYContainerElement>
    <UIDisplay Left="0" Top="0" Width="0.5" Height="1" IsShow="True"  ZIndex="1" UsePercent="True"/>
    <Controls>
        <ImageButton>
            <UIDisplay Left="0" Top="0" Width="180" Height="180" IsShow="True"  ZIndex="1" UsePercent="false"/>
            <ImageSource UriKind="Relative">NavIcons\bubble.png</ImageSource>
            <ClickEvent>PopupEvent?TargetPageName=HomePage&TargetControlName=VideoElement&X=100&Y=100&Height=100&Width=200&EventID=PC03.wmv&EventPath=</ClickEvent>
        </ImageButton>
    </Controls>
</XYContainerElement>

```

## 5.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。

## 6.Controls 节点

`Controls` 是 `XYContainerElement` 的直接子节点，内部可包含一个或多个已注册的子控件。每个子控件独立配置自己的 `UIDisplay` 和事件。

```xml
<Controls>
    <ImageButton>... </ImageButton>
    <TextElement>... </TextElement>
    <ImageElement>... </ImageElement>
</Controls>
```

### 6.1子控件定位

容器内部使用 `Canvas` 布局，子控件的 `Left` 和 `Top` 是相对于容器左上角的坐标：

- 当容器 `UsePercent="True"` 而子控件 `UsePercent="False"` 时，容器大小会随父容器缩放，子控件保持固定像素大小；
- 当容器和子控件都 `UsePercent="True"` 时，子控件的位置和大小均按容器尺寸百分比计算；
- 子控件的 `ZIndex` 仅在容器内部参与层级排序。

## 7.嵌套使用

`XYContainerElement` 可以嵌套使用，即一个 `XYContainerElement` 内部可以包含另一个 `XYContainerElement`，用于实现更复杂的分层布局。

```xml
<XYContainerElement Name="Outer">
    <UIDisplay Left="0" Top="0" Width="1" Height="1" UsePercent="True" />
    <Controls>
        <XYContainerElement Name="Inner">
            <UIDisplay Left="0.1" Top="0.1" Width="0.8" Height="0.8" UsePercent="True" />
            <Controls>
                <ImageElement>... </ImageElement>
            </Controls>
        </XYContainerElement>
    </Controls>
</XYContainerElement>
```

## 8.UIControlDict.xml 说明

`XYContainerElement` 由框架在 `UIElementManager.RegisterInnerElement()` 中自动注册，通常不需要手动在 `UIControlDict.xml` 中添加。如需自定义注册，可参考：

```xml
<Element ViewType="XYContainerElement" AssemblyFile="SensingPlatform.Foundation.dll" TypeName="SensingPlatform.Foundation.Page.XYContainer, SensingPlatform.Foundation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="SensingPlatform.Foundation.dll" TypeName="SensingPlatform.Foundation.Page.SensingContainerViewModel, SensingPlatform.Foundation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 9.部署说明

1. 确认 `SensingPlatform.Foundation.dll` 存在于项目目录；
2. 确保需要在容器内使用的子控件已在 `SysConfig/UIControlDict.xml` 中注册；
3. 在页面 XML 中使用 `XYContainerElement`，配置 `UIDisplay` 和 `Controls`；
4. 在 `Controls` 内按需求添加子控件。

## 10.常见问题

### 容器不显示

- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查 `Width` / `Height` 是否大于 0；
- 检查 `ZIndex` 是否被其他控件遮挡。

### 子控件不显示

- 检查子控件的 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查子控件的 `Left`、`Top` 是否在容器可见范围内；
- 检查子控件的资源路径是否正确；
- 检查子控件是否已在 `UIControlDict.xml` 中注册。

### 百分比布局异常

- 检查容器和子控件的 `UsePercent` 配置是否匹配预期；
- 当容器 `UsePercent="True"` 时，子控件若使用像素值，可能会出现不同分辨率下布局不一致的问题；
- 需要自适应时，建议容器和子控件统一使用 `UsePercent="True"`。

### 页面切换后子控件状态丢失

- 检查 `UIDisplay` 的 `IsUseCache` 是否为 `True`；
- 缓存开启时，子控件不会被重新创建，可保留状态，但会占用更多内存。

## 11.注意事项

- `XYContainerElement` 内部使用 `Canvas` 绝对定位，子控件超出容器边界时默认不会被裁剪；
- 子控件的 `Left`/`Top` 是相对于容器左上角的坐标；
- 建议为容器和需要被事件引用的子控件配置 `Name` 属性；
- 事件 URL 中的 `&` 必须转义为 `&amp;`；
- 控件卸载时会自动释放非缓存状态的子控件资源。
