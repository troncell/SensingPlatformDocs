# **图片控件**（**ImageElement**）

## 1.控件作用

图片控件用于在页面或弹出框中直接显示图片。它是最常用的基础控件之一，支持通过 `ImageSource` 指定图片路径，并可配合 `UIDisplay` 控制显示位置、大小、层级、透明度等属性。

## 2.适用场景

- 页面背景图
- 产品图片展示
- 按钮图标、装饰图片
- 弹出框内容图片
- 需要动态切换图片的场景

## 3.前置依赖

使用图片控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `ImageElement`。

## 4.控件 UI 效果

![Placeholder](../images/imageelement_1.png)

## 5.配置文件样例

```xml
<ImageElement  Name="Background">
    <!--参考控件公用片段的讲解中UIDdisplay片段讲解-->
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1" IsHitTestVisible="True" IsUseCache="True"/>
    <!--参考控件公用片段的讲解中ImageSource片段讲解-->
    <ImageSource UriKind="Application">Shell\Pages\CirclePage\test.jpg</ImageSource>
</ImageElement>
```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对图片控件：

- `Width` / `Height`：定义图片的显示区域大小；
- `ZIndex`：注意图片与其他控件的层级关系；
- `Opacity`：设置图片透明度；
- `IsHitTestVisible`：是否允许点击穿透到下层控件；
- `IsUseCache`：是否缓存图片，频繁显示的图片建议开启；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`。

## 7.ImageSource 参数说明

| 属性      | 必填 | 说明             | 示例          |
| --------- | ---- | ---------------- | ------------- |
| `UriKind` | 是   | 图片路径解析方式 | `Application` |

### 7.1UriKind 说明

| 取值          | 路径基准              | 示例                              |
| ------------- | --------------------- | --------------------------------- |
| `Relative`    | 当前 XML 文件所在目录 | `test.jpg`、`resource\bg.png`     |
| `Application` | 应用根目录            | `Shell\Pages\CirclePage\test.jpg` |
| `Project`     | `Shell` 文件夹        | `Pages\CirclePage\test.jpg`       |
| `Absolute`    | 物理磁盘绝对路径      | `C:\Images\bg.png`                |
| `Web`         | HTTP/HTTPS 地址       | `https://example.com/image.png`   |

### 7.2示例

1.Application 路径

```xml
<ImageSource UriKind="Application">Shell\Pages\CirclePage\test.jpg</ImageSource>
```

2.Relative 路径

```xml
<ImageSource UriKind="Relative">lianliankan.png</ImageSource>
```

3.Absolute 路径

```xml
<ImageSource UriKind="Absolute">C:\Images\bg.png</ImageSource>
```

## 8.可接受的事件

### 8.1SourceChanged 事件

`SourceChanged` 事件用于动态变更图片控件显示的图片。

```xml
<ClickEvent>SourceChanged?TargetControlName=Background&ImageSource=Shell\Pages\HomePage\resource\newBg.jpg</ClickEvent>
```

| 参数                | 说明             | 示例                                      |
| ------------------- | ---------------- | ----------------------------------------- |
| `TargetControlName` | 目标图片控件名称 | `Background`                              |
| `ImageSource`       | 新的图片路径     | `Shell\Pages\HomePage\resource\newBg.jpg` |

## 9.UIControlDict.xml 添加图片控件

如果使用图片控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<Element ViewType="ImageElement" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.ImageControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.ImageElementViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 10.部署说明

1. 确认项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 准备图片资源；
4. 在页面 XML 中使用 `ImageElement`，配置 `UIDisplay` 和 `ImageSource`。

## 11.常见问题

### 图片不显示

- 检查 `ImageSource` 的 `UriKind` 和路径是否正确；
- 确认图片文件真实存在；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查 `ZIndex` 是否被其他控件遮挡。

### 图片路径错误

- `Application` 路径需要以 `Shell\` 或 `Resource\` 开头；
- `Project` 路径不需要加 `Shell\` 前缀；
- `Relative` 路径是相对于当前 XML 文件所在目录；
- 路径中不要有多余空格。

### 图片显示模糊或变形

- 检查 `UIDisplay` 的 `Width` / `Height` 是否与图片原始比例匹配；
- 检查是否使用了 `UsePercent="True"` 导致缩放；
- 图片本身分辨率过低也可能导致模糊。

### 动态切换图片不生效

- 检查 `SourceChanged` 事件中的 `TargetControlName` 是否与目标图片控件的 `Name` 一致；
- 检查新的图片路径是否正确；
- 检查目标图片控件是否配置了 `Name` 属性。

### 图片加载慢

- 检查图片文件大小是否过大；
- 将 `IsUseCache` 设为 `True` 以缓存图片；
- 对于大背景图，建议使用适当压缩的图片。

## 12.注意事项

- `ImageElement` 是最基础的显示控件，配置简单但使用频率最高；
- 建议为需要被事件引用的图片控件配置 `Name` 属性；
- 路径中的特殊字符和空格需要谨慎处理；
- 在线图片（Web）需要网络访问权限，且加载速度受网络影响。
