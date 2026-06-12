# 飞图控件（AlbumElement）

## 1.控件作用

飞图控件以自动浮动的交互方式展示一系列图片或视频，它的特点是更换资料非常方便，只要更换文件夹里面的图片即可。适用于照片墙、作品展示、荣誉墙等场景。

## 2.适用场景

- 需要自动漂浮、缓慢移动的图片展示墙
- 不希望手动配置每张图片，而是通过文件夹批量加载
- 支持背景图和底部分类栏切换的展示页

## 3.控件 UI 效果

![Placeholder](../images/album_1.png)

## 4.前置依赖

使用飞图控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Album.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `AlbumElement`；
3. （可选）在应用根目录放置 `UI.Album.dll.config` 作为全局默认配置。

## 5.UIControlDict.xml 注册

如果使用飞图控件则需要在 UIControlDict.xml 中添加飞图控件

```
 <!--UI.AlbumLibrary 控件包-->
  <Element ViewType="AlbumElement" AssemblyFile="UI.Album.dll" TypeName="UI.Album.AlbumControl, UI.Album, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Album.dll" TypeName="UI.Album.AlbumControlViewModel, UI.Album, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.AlbumLibrary  END-->
```

## 6.配置文件样例

```xml
<AlbumElement>
<!--参考控件公用片段CommonElement.md讲解中UIDisplay片段讲解-->
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="false" IsUseCache="false" />
    <CustomerConfig>
        <BgType Type="1" UriKind="Application">Shell\Pages\PhotoPage\resource\bg\bg.png</BgType>
        <Fold UriKind="Application">Shell\Pages\PhotoPage\resource</Fold>
        <IsFoldBarVisible>False</IsFoldBarVisible>
    </CustomerConfig>
</AlbumElement>
```

## 7.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对飞图控件，需要特别注意：

- `Width` / `Height`：决定飞图控件的显示区域大小，图片会在该区域内漂浮；
- `ZIndex`：如果页面有其他悬浮按钮或弹出层，建议飞图控件放在较低的层级；
- `IsUseCache`：建议设为 `false`，飞图控件通常从磁盘实时加载文件夹内容，开启缓存可能导致更换资源后无法立即生效。

## 8.CustomerConfig 参数说明

| 参数               | 必填 | 说明                                                                                      | 示例                                                                |
| ------------------ | ---- | ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `BgType`           | 否   | 背景配置。`Type="0"` 不显示背景；`Type="1"` 显示图片背景；后续版本可能支持视频或 Web 背景 | `<BgType Type="1" UriKind="Application">Shell\...\bg.png</BgType>`  |
| `Fold`             | 是   | 资源文件夹路径，控件会从该文件夹加载图片或视频                                            | `<Fold UriKind="Application">Shell\Pages\PhotoPage\resource</Fold>` |
| `IsFoldBarVisible` | 否   | 底部分类文件夹栏是否显示。`False` 不显示，`True` 显示                                     | `<IsFoldBarVisible>False</IsFoldBarVisible>`                        |

## 9.BgType 的两种配置方式

页面级配置优先级高于 `UI.Album.dll.config` 全局配置：

- 如果页面 `CustomerConfig` 中声明了 `BgType`，则使用页面配置；
- 如果页面未声明，则读取 `UI.Album.dll.config` 中的 `BgType` 键值。

## 10.资源文件夹规范

`Fold` 节点指向的文件夹为飞图控件的资源根目录，建议按以下结构组织：

```

Shell\Pages\PhotoPage\resource\

├── bg.png              # 背景图片，当 BgType=1 时使用

├── 1.jpg

├── 2.png

├── 3.jpg

└── ...

```

- 支持直接放置图片文件；
- 文件会按一定规则（如文件名排序或随机顺序）在显示区域内漂浮；
- 若需要分类展示，通常配合子文件夹实现，具体分类逻辑以运行时效果为准。

## 11.UI.Album.dll.config 详细说明

在应用根目录放置 `UI.Album.dll.config`，可作为全局默认配置。各配置项说明如下：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <appSettings>
    <add key="Fold" value="Resources"/>
    <!--1左移2右移-->
    <add key="Direction" value="2"/>
    <!--摆动幅度-->
    <add key="SwingAngle" value="0"/>
    <!--摆动角度最大速度(0.1~1)-->
    <add key="SwingAngleMaxSpeed" value="0.0"/>
    <!--滑动速度-->
    <add key="SweepSpeed" value="1"/>
    <!--滑动频率毫秒-->
    <add key="SweepInterval" value="1"/>
    <!--是否随机显示-->
    <add key="RandomShow" value="true"/>
    <!--自动关闭弹出窗口时间，整数s-->
    <add key="AutoClostInterval" value="3"/>
    <!--本地web资源文件夹-->
    <add key="LocalWebPath" value="WebResources\LocalWebs"/>
    <!--ie图标文件夹-->
    <add key="IEImages" value="WebResources\IEImages"/>
    <!--签名对应名称-->
    <add key="SignMark" value="Sign"/>
    <!--背景类型（1：picture,2:video,3:web）#后面加bg文件夹下的资源,web例子：3#XXX.htm-->
    <add key="BgType" value="1#bg.png"/>
    <!--选择保存路径，0：temp文件夹；1：领导文件夹-->
    <add key="SavePath" value="0"/>
    <add key="KeepAngle" value="True"/>
    <!-- 随机摆动范围 -->
    <add key="ROTATESCROPE" value="0"/>
  </appSettings>
</configuration>
```

| 配置键               | 默认值                   | 说明                                                                               |
| -------------------- | ------------------------ | ---------------------------------------------------------------------------------- |
| `Fold`               | `Resources`              | 默认资源文件夹路径                                                                 |
| `Direction`          | `2`                      | 漂浮移动方向：`1` 左移，`2` 右移                                                   |
| `SwingAngle`         | `0`                      | 摆动幅度，单位度。`0` 表示不摆动                                                   |
| `SwingAngleMaxSpeed` | `0.0`                    | 摆动角度最大速度，取值范围 `0.1 ~ 1`                                               |
| `SweepSpeed`         | `1`                      | 图片整体滑动速度                                                                   |
| `SweepInterval`      | `1`                      | 滑动频率，单位毫秒                                                                 |
| `RandomShow`         | `true`                   | 是否随机显示图片位置                                                               |
| `AutoClostInterval`  | `3`                      | 点击图片弹出的详情窗口自动关闭时间，单位秒                                         |
| `LocalWebPath`       | `WebResources\LocalWebs` | 本地 Web 资源文件夹                                                                |
| `IEImages`           | `WebResources\IEImages`  | IE 图标文件夹                                                                      |
| `SignMark`           | `Sign`                   | 签名对应名称                                                                       |
| `BgType`             | `1#bg.png`               | 全局背景类型。格式为 `类型#资源`，`1` 图片、`2` 视频、`3` Web。示例：`3#index.htm` |
| `SavePath`           | `0`                      | 选择保存路径：`0` temp 文件夹，`1` 领导文件夹                                      |
| `KeepAngle`          | `True`                   | 是否保持图片当前的旋转角度                                                         |
| `ROTATESCROPE`       | `0`                      | 随机摆动范围                                                                       |

## 12.交互行为

- 图片会自动在 `UIDisplay` 定义的区域内漂浮移动；
- 点击某张图片通常会弹出详情查看窗口；
- 弹出窗口会在 `AutoClostInterval` 设定的时间后自动关闭；
- 若开启 `IsFoldBarVisible`，底部会显示分类栏，可切换不同分类。

## 13.支持的媒体格式

| 类型 | 常见格式                                | 说明                               |
| ---- | --------------------------------------- | ---------------------------------- |
| 图片 | `.png`、`.jpg`、`.jpeg`、`.bmp`、`.gif` | 推荐使用 `.png` 或 `.jpg`          |
| 视频 | 视运行时解码能力而定                    | 如有视频需求，建议先用实际文件测试 |
| Web  | `.htm` / `.html`                        | 当 `BgType=3` 时作为背景加载       |

## 14.部署说明

1. 将 `UI.Album.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 将 `UI.Album.dll.config` 复制到同一目录（如使用全局配置）；
3. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
4. 在页面 XML 中使用 `<AlbumElement>` 并配置 `CustomerConfig`。

## 15.常见问题

### 图片不显示

- 检查 `Fold` 路径是否正确；
- 确认 `UriKind` 选择正确，`Application` 对应应用根目录，`Relative` 对应页面 XML 所在目录；
- 确认文件夹内存在支持的图片格式文件。

### 背景不显示

- 检查 `BgType` 是否为 `1`；
- 检查背景图片路径是否正确；
- 如果页面未配置 `BgType`，检查 `UI.Album.dll.config` 中的 `BgType` 键值。

### 分类栏没有显示

- 确认 `IsFoldBarVisible` 为 `True`；
- 确认资源文件夹结构符合分类展示要求。

### 弹出窗口不自动关闭

- 检查 `UI.Album.dll.config` 中 `AutoClostInterval` 是否大于 0；
- 注意该值为整数秒。
