# 二维码控件（QrCodeElement）

## 1.控件作用

二维码控件用于在页面中动态生成并显示二维码。通过配置 `Text` 属性指定二维码内容（如 URL、文本、字符串等），控件会自动渲染对应的二维码图片。

## 2.适用场景

- 展示网站或应用下载链接
- 展示产品信息、活动详情
- 展示联系方式、WiFi 密码
- 需要用户使用手机扫码获取信息的场景

## 3.前置依赖

使用二维码控件前，必须满足以下条件：

1. 项目目录中存在 `UI.QrCode.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `QrCodeElement`；
3. 准备好需要生成二维码的内容（URL 或文本）。

## 4.控件 UI 效果

![Placeholder](../images/QrCodeElement.png)

## 5.配置文件样例

### 5.1静态二维码

```xml
<QrCodeElement>
    <UIDisplay Left="500" Top="500" Width="300" Height="300" IsShow="True" ZIndex="1" UsePercent="False" Opacity="1" />

    <CustomerConfig>
        <QrCode LightBrush="#FFFFFFFF" DarkBrush="#FF000000" IsGrayImage="True" Text="https://troncell.com" />
    </CustomerConfig>
</QrCodeElement>
```

### 5.2动态数据绑定二维码

```xml
<QrCodeElement>
    <UIDisplay Left="500" Top="500" Width="300" Height="300" IsShow="True" ZIndex="1" UsePercent="False" />

    <DataProvider>ProductData?CSTable=Products</DataProvider>

    <CustomerConfig>
        <QrCode LightBrush="#FFFFFFFF" DarkBrush="#FF000000" IsGrayImage="False" Text="{$QrCodeUrl}" />
    </CustomerConfig>
</QrCodeElement>
```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)

## 7.CustomerConfig 参数说明

### 7.1QrCode节点

| 属性          | 必填 | 说明                                                        | 示例                   |
| ------------- | ---- | ----------------------------------------------------------- | ---------------------- |
| `Text`        | 是   | 生成二维码的文本内容，可以是 URL 或任意字符串               | `https://troncell.com` |
| `LightBrush`  | 否   | 二维码浅色部分（背景）颜色                                  | `#FFFFFFFF`            |
| `DarkBrush`   | 否   | 二维码深色部分（码点）颜色                                  | `#FF000000`            |
| `IsGrayImage` | 否   | 是否为灰度图片。`True` 时只能调整亮度，`False` 时可调整颜色 | `True`                 |

### 7.2属性说明

- **Text**：二维码的实际内容。可以是网址、文本、联系方式等。支持通过 `{$变量名}` 绑定数据源中的列。
- **LightBrush**：二维码背景色，通常为白色。
- **DarkBrush**：二维码前景色（码点颜色），通常为黑色。
- **IsGrayImage**：控制二维码是否以灰度方式渲染。
  - `True`：二维码以灰度图方式显示，此时 `LightBrush` 和 `DarkBrush` 主要影响亮度；
  - `False`：二维码以彩色方式显示，可以完全自定义二维码颜色。

### 7.3颜色格式

颜色值支持以下格式：

- 十六进制 ARGB：`#FFFFFFFF`、`#FF000000`
- 颜色名称：`White`、`Black`、`Red` 等

### 7.4其他可能支持的参数

不同版本的二维码控件可能还支持以下参数：

| 参数                   | 说明                               | 示例 |
| ---------------------- | ---------------------------------- | ---- |
| `ErrorCorrectionLevel` | 二维码容错级别：`L`、`M`、`Q`、`H` | `M`  |
| `ModuleSize`           | 二维码模块大小                     | `4`  |
| `QuietZone`            | 二维码边距                         | `4`  |

> 以上参数以实际版本为准。

## 8.数据绑定

二维码控件可以通过 `DataProvider` 动态生成二维码。例如：

```xml
<DataProvider>ProductData?CSTable=Products</DataProvider>

<CustomerConfig>
    <QrCode Text="{$QrCodeUrl}" />
</CustomerConfig>
```

- `{$QrCodeUrl}` 对应数据源中存储二维码内容的列；
- 当数据变化时，二维码会自动重新生成。

## 9.SourceChanged 事件

二维码控件支持 `SourceChanged` 事件，用于动态变更二维码内容。

```xml
<ClickEvent>SourceChanged?TargetControlName=MyQrCode&Text=https://new-url.com</ClickEvent>
```

| 参数                | 说明               | 示例                  |
| ------------------- | ------------------ | --------------------- |
| `TargetControlName` | 目标二维码控件名称 | `MyQrCode`            |
| `Text`              | 新的二维码内容     | `https://new-url.com` |

## 10.UIControlDict.xml 添加二维码控件

如果使用二维码控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<!--UI.QrCode 控件包-->
<Element ViewType="QrCodeElement" AssemblyFile="UI.QrCode.dll" TypeName="UI.QrCode.QrCodeControl, UI.QrCode, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.QrCode.dll" TypeName="UI.QrCode.QrCodeControlViewModel, UI.QrCode, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
<!--UI.QrCode END-->
```

## 11.部署说明

1. 将 `UI.QrCode.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 准备需要生成二维码的内容；
4. 在页面 XML 中使用 `QrCodeElement`，配置 `UIDisplay` 和 `CustomerConfig`。

## 12.常见问题

### 二维码不显示

- 检查 `UI.QrCode.dll` 是否存在于应用根目录；
- 检查 `UIControlDict.xml` 中的注册信息是否正确；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查 `Text` 是否为空或包含非法字符。

### 二维码无法识别

- 确保 `Text` 内容符合二维码编码规范；
- 检查二维码尺寸是否过小；
- 检查 `LightBrush` 和 `DarkBrush` 对比度是否足够；
- 避免使用过于复杂的 URL 或长文本。

### 二维码颜色异常

- 检查 `IsGrayImage` 是否为 `False`（如果需要自定义颜色）；
- 检查 `LightBrush` 和 `DarkBrush` 颜色值是否正确；
- 确保深色和浅色有足够的对比度。

### 动态数据绑定的二维码不更新

- 检查 `DataProvider` 中的数据源名称和表名是否正确；
- 检查 `{$QrCodeUrl}` 等变量名是否与数据源列名一致；
- 检查数据源中对应列的值是否为空。

### 二维码内容被截断

- 增大 `UIDisplay` 的 `Width` 和 `Height`；
- 减少 `Text` 内容长度；
- 检查是否使用了过低的分辨率。

## 13.注意事项

- 二维码内容过长时，建议增大显示尺寸以提高识别率；
- 二维码前景色和背景色应有明显对比，避免使用相近颜色；
- 二维码控件生成的图片为位图，放大时可能会出现锯齿；
- 动态数据绑定时，确保数据源中的内容为有效的二维码内容（如 URL 编码后的字符串）。
