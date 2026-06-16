# 图片旋转控件（RotateControlElement）

## 1.控件作用

图片旋转控件用于在页面中显示一组图片，并支持用户通过点击拖动来旋转浏览这些图片。图片按文件名顺序排列，旋转时会依次显示不同的图片，适用于 360 度产品展示、全景浏览、图片序列查看等场景。

## 2.适用场景

- 360 度产品展示（如汽车、家具、商品）
- 全景图片浏览
- 需要手动旋转查看的序列帧图片
- 展厅互动旋转展示

## 3.前置依赖

使用图片旋转控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `RotateControlElement`；
3. 准备一组按顺序命名的图片文件，并放置在同一文件夹中。

## 4.控件 UI 效果

![Placeholder](../images/RotateControlElement.gif)

## 5.配置文件样例

```xml
<RotateControlElement>
  <UIDisplay Left="600" Top="450" Width="973" Height="913" IsShow="True" ZIndex="1" UsePercent="False" />
  <CustomerConfig>
  <!--图片的存放位置-->
        <!--方向 X或Y -->
        <!--摩擦系数 默认是1 ，其值越大，移动越慢 -->
    <RotateConfig Path="Images" Orientation="Y" Sensitivity="0.05" />
     <!--配置自动旋转,Value设置是否可以自动旋播放，其值为ture或false；Orientation设置为移动到上一张还是下一张图片,设置为1为移动到下一张图片，其它值为移动到上一张图片，Duration为设置多长时间移动一圈，其值为时间型; StartTime表示多久无人操作则开始自动旋转，其值为整数，单位为秒-->
    <AutoRotate Value="True" Orientation="1" Duration="00:00:04" StartTime="2" />
  </CustomerConfig>
</RotateControlElement>



```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。

## 7.CustomerConfig 参数说明

### 7.1RotateConfig 节点

| 属性          | 必填 | 说明                                         | 示例     |
| ------------- | ---- | -------------------------------------------- | -------- |
| `Path`        | 是   | 图片文件夹路径                               | `Images` |
| `Orientation` | 否   | 旋转方向，`X` 表示水平旋转，`Y` 表示垂直旋转 | `Y`      |
| `Sensitivity` | 否   | 摩擦系数，默认 `1`，值越大移动越慢           | `0.05`   |

### 7.2AutoRotate 节点

| 属性          | 必填 | 说明                                                                                     | 示例       |
| ------------- | ---- | ---------------------------------------------------------------------------------------- | ---------- |
| `Value`       | 否   | 是否自动旋转播放，`True` 或 `False`                                                      | `True`     |
| `Orientation` | 否   | 自动旋转方向，设置为移动到上一张还是下一张图片。`1` 为移动到下一张，其它值为移动到上一张 | `1`        |
| `Duration`    | 否   | 自动旋转一圈的时间，时间格式 `HH:MM:SS`                                                  | `00:00:04` |
| `StartTime`   | 否   | 无人操作多久后开始自动旋转，单位秒                                                       | `2`        |

### 7.3属性说明

- **Path**：图片存放的文件夹路径。控件会读取该文件夹下的所有图片，并按文件名排序后依次显示。
- **Orientation**：用户拖动旋转的方向。
  - `X`：水平方向拖动旋转；
  - `Y`：垂直方向拖动旋转。
- **Sensitivity**：控制旋转的灵敏度。数值越大，相同拖动距离下旋转越慢；数值越小，旋转越快。
- **AutoRotate.Value**：是否启用自动旋转。
- **AutoRotate.Orientation**：自动旋转的方向，与手动拖动方向对应。
- **AutoRotate.Duration**：自动旋转完成一圈所需的时间。
- **AutoRotate.StartTime**：用户停止操作后，等待多少秒开始自动旋转。

## 8.图片命名规范

旋转控件读取文件夹中的图片时，按文件名字母顺序排序。建议按以下方式命名：

```
Images/
├── image01.png
├── image02.png
├── image03.png
├── ...
└── image36.png
```

- 使用连续的数字命名，确保顺序正确；
- 建议数字前补零（如 `01`、`02`），避免 `image10.png` 排在 `image2.png` 之前；
- 所有图片建议尺寸一致，避免旋转时出现跳动。

### 8.1路径说明

`Path` 属性指定图片文件夹路径，路径解析方式取决于实际实现：

| 路径类型 | 说明                            | 示例                                       |
| -------- | ------------------------------- | ------------------------------------------ |
| 相对路径 | 相对于应用根目录或当前 XML 文件 | `Images`、`Shell\Pages\ProductPage\Images` |
| 绝对路径 | 物理磁盘绝对路径                | `C:\Images\Product`                        |

建议将图片放在页面资源目录下，便于管理。

## 9.UIControlDict.xml 添加图片旋转控件

如果使用图片旋转控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<!--UI.Common 控件包-->
<Element ViewType="RotateControlElement" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.RotateControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.RotateControlViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 10.部署说明

1. 确认项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 准备一组按顺序命名的图片，放入同一文件夹；
4. 在页面 XML 中使用 `RotateControlElement`，配置 `UIDisplay` 和 `CustomerConfig`。

## 11.常见问题

### 图片不显示

- 检查 `Path` 路径是否正确；
- 检查文件夹中是否存在图片文件；
- 检查图片格式是否受支持；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`。

### 旋转不流畅

- 调整 `Sensitivity` 的值，过大或过小都可能影响体验；
- 检查图片尺寸是否过大，过大图片会影响性能；
- 减少图片数量或压缩图片。

### 图片顺序不对

- 检查图片命名是否按字母顺序排列；
- 建议使用补零数字命名，如 `image01.png`、`image02.png`；
- 避免使用特殊字符或不同长度的文件名。

### 自动旋转不生效

- 检查 `AutoRotate` 的 `Value` 是否为 `True`；
- 检查 `Duration` 是否设置合理；
- 检查 `StartTime` 是否设置过大；
- 检查用户交互后是否会暂停自动旋转。

### 旋转方向不对

- 检查 `RotateConfig` 的 `Orientation` 是否为期望的 `X` 或 `Y`；
- 检查 `AutoRotate` 的 `Orientation` 是否为期望的值。

### 图片旋转时跳动

- 检查所有图片尺寸是否一致；
- 检查图片是否按正确顺序排列；
- 调整 `UIDisplay` 的 `Width` 和 `Height` 与图片比例匹配。

## 12.注意事项

- 图片旋转控件依赖文件名字母顺序，命名时务必注意顺序；
- 建议所有图片使用相同尺寸，避免切换时视觉跳动；
- 图片数量较多或尺寸较大时，建议进行压缩以提升性能；
- `Sensitivity` 需要根据实际交互体验调整，建议在实际设备上测试；
- 自动旋转功能在无人操作时才启动，用户交互后通常会暂停。
