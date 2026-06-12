# 长图文滑块控件（PagerElement）

## 1.控件作用

长图文滑块控件用于展示多张长图文内容。每张长图文可以上下滑动浏览，同时支持左右滑动切换上一张/下一张长图文。常用于漫画、长图文章、详情页等需要纵向滚动和横向切换结合的场景。

## 2.适用场景

- 漫画、绘本阅读
- 长图文详情展示
- 产品介绍长图
- 宣传海报、图文混排内容

## 3.前置依赖

使用长图文滑块控件前，必须满足以下条件：

1. 项目目录中存在 `UI.FlipView.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `PagerElement`；
3. 如需动态加载内容，需在 `Shell/Data/Data.xml` 中配置数据源并在页面中使用 `DataProvider`；
4. 若使用 `ScrollViewerElement`，需确认该控件已注册。

## 4.控件 UI 效果

![Placeholder](../images/PagerElement.png)
![Placeholder](../images/PagerElement.gif)

## 5.配置文件样例

```
<PagerElement Name="resource">
    <UIDisplay Left="125" Top="258" Width="829" Height="1372" IsShow="True" ZIndex="3" UsePercent="False" />
    <DataProvider>CartoonData?CSTable=深交所</DataProvider>
    <Items IsCacheUI="True">
        <Template Left="0" Top="0" Width="829" Height="1381" TemplateID="10001">
            <XYContainerElement>
                <UIDisplay Left="0" Top="0" Width="829" Height="1381" IsShow="True"  ZIndex="3" UsePercent="False"/>
                <Controls>
                    <ScrollViewerElement>
                        <UIDisplay Left="0" Top="0" Width="829" Height="1381" IsShow="True" ZIndex="4" UsePercent="False" />
                        <Items>
                            <Item>
                                <ImageElement Name="resource">
                                    <UIDisplay Left="0" Top="0" Width="829" Height="8000" IsShow="True" ZIndex="3" UsePercent="False" Opacity="1" IsUseCache="True" />
                                    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\证券基础知识\衍生品\漫画\{$Pic}</ImageSource>
                                    <CustomerConfig>
                                        <Image AutoHeight="True"/>
                                    </CustomerConfig>
                                </ImageElement>
                            </Item>
                        </Items>
                        <CustomerConfig>
                            <ScrollView />
                            <!-- <ThumbImage UriKind="Application" Width="33" Height="38">Shell\Pages\HomePage\resource\thumb.png</ThumbImage> -->
                        </CustomerConfig>
                    </ScrollViewerElement>
                </Controls>
            </XYContainerElement>
        </Template>
    </Items>
    <CustomerConfig>
        <PagerIndex VerticalAlignment="Top" Offset="-33" PageIndexColor="#" PageIndexSelectedColor="RED"  />
    </CustomerConfig>
</PagerElement>
```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)

## 7.DataProvider 与 Items

### 7.1动态数据源模式

通过 `DataProvider` 绑定数据源，数据源中的每一行会生成一页长图文。

```xml
<DataProvider>CartoonData?CSTable=深交所</DataProvider>
```

- `CartoonData`：数据源实例名称，需在 `Shell/Data/Data.xml` 中定义；
- `CSTable=深交所`：数据表/集合名称；
- `Template` 中的 `{$Pic}` 等变量需与数据源中的列名一致。

### 7.2Items 属性

| 属性        | 必填 | 说明                                                     | 示例   |
| ----------- | ---- | -------------------------------------------------------- | ------ |
| `IsCacheUI` | 否   | 是否缓存页面 UI。`True` 提升切换流畅度，`False` 节省内存 | `True` |

### 7.3Template 属性

| 属性         | 必填 | 说明           | 示例    |
| ------------ | ---- | -------------- | ------- |
| `Left`       | 否   | 模板左上角位置 | `0`     |
| `Top`        | 否   | 模板左上角位置 | `0`     |
| `Width`      | 否   | 模板宽度       | `829`   |
| `Height`     | 否   | 模板高度       | `1381`  |
| `TemplateID` | 否   | 模板标识       | `10001` |

## 8.长图文内容配置

每页长图文通常使用 `ScrollViewerElement` 包裹 `ImageElement`，实现上下滚动浏览长图。

```xml
<ScrollViewerElement>
    <Items>
        <Item>
            <ImageElement>
                <ImageSource UriKind="Application">...\{$Pic}</ImageSource>
                <CustomerConfig>
                    <Image AutoHeight="True" />
                </CustomerConfig>
            </ImageElement>
        </Item>
    </Items>
</ScrollViewerElement>
```

- `Image` 的 `AutoHeight="True"` 用于让图片根据原始比例自动调整高度；
- 图片高度通常远大于显示区域高度，因此需要 `ScrollViewerElement` 支持滚动。

## 9.CustomerConfig 参数说明

### 9.1PagerIndex 节点

| 属性                     | 必填 | 说明                                                                         | 示例            |
| ------------------------ | ---- | ---------------------------------------------------------------------------- | --------------- |
| `VerticalAlignment`      | 否   | 页面指示器的垂直对齐方式                                                     | `Top`、`Bottom` |
| `Offset`                 | 否   | 指示器的位置偏移，配置左右滑动圆点的位置                                     | `-33`           |
| `PageIndexColor`         | 否   | 未选中指示器的颜色，配置长图文滑块中，左右滑动到该长图文时，其它图标的颜色； | `#FFFFFF`       |
| `PageIndexSelectedColor` | 否   | 当前选中指示器的颜色，配置长图文滑块中，左右滑动到该长图文时，该图标的颜色。 | `RED`           |

### 9.2属性说明

- **VerticalAlignment**：页面指示器在垂直方向上的对齐方式，常见取值为 `Top` 或 `Bottom`。
- **Offset**：指示器相对于对齐位置的偏移量，负值向上偏移，正值向下偏移。
- **PageIndexColor**：未选中页面指示器的颜色。
- **PageIndexSelectedColor**：当前选中页面指示器的颜色。

## 10.UIControlDict.xml 添加长图文滑块控件

如果使用长图文滑块控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<Element ViewType="PagerElement" AssemblyFile="UI.FlipView.dll" TypeName="UI.FlipView.PagerView, UI.FlipView, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.FlipView.dll" TypeName="UI.FlipView.PagerViewModel, UI.FlipView, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 11.部署说明

1. 将 `UI.FlipView.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 如需动态数据，在 `Shell/Data/Data.xml` 中配置数据源，并在页面中使用 `DataProvider`；
4. 在页面 XML 中使用 `PagerElement`，配置 `UIDisplay`、`DataProvider`、`Items` 和 `CustomerConfig`。

## 12.常见问题

### 长图文不显示

- 检查 `DataProvider` 中的数据源名称和表名是否正确；
- 检查 `ImageSource` 的 `UriKind` 和路径是否正确；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`。

### 无法上下滑动

- 检查 `ScrollViewerElement` 是否正确配置；
- 检查 `ImageElement` 的高度是否大于 `ScrollViewerElement` 的高度；
- 检查 `Image` 的 `AutoHeight` 是否设为 `True`。

### 无法左右切换

- 检查 `PagerElement` 的 `UIDisplay` 宽度是否与 `Template` 宽度匹配；
- 检查是否有上层控件拦截了横向滑动事件。

### 页面指示器不显示

- 检查 `PagerIndex` 节点是否配置；
- 检查 `PageIndexColor` 和 `PageIndexSelectedColor` 是否配置正确；
- 检查 `VerticalAlignment` 和 `Offset` 是否导致指示器超出可见区域。

### 数据源内容没有生成多页

- 确认 `DataProvider` 中的数据源名称和表名正确；
- 确认数据源中有多条数据；
- 确认 `Template` 中使用了正确的 `{$变量名}` 绑定。

## 13.注意事项

- 长图文图片高度通常较大，注意图片压缩和加载性能；
- `IsCacheUI="True"` 可提升页面切换流畅度，但会占用更多内存；
- 横向滑动和纵向滚动可能产生事件冲突，建议测试实际交互效果；
- 页面指示器颜色应保证在背景图上清晰可见。
