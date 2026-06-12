# 摄像头数据流控件（CameraElement）

## 10控件作用

摄像头数据流控件用于在页面上实时显示摄像头采集的画面，支持彩色图像（Color）和深度图像（Depth）两种显示模式。常用于需要展示摄像头画面或接入体感、深度识别等硬件能力的场景。

## 2.适用场景

- 展示摄像头实时画面
- 体感交互项目中显示彩色或深度图像
- 需要预览摄像头采集效果的调试页面
- 结合 `Module.Camera` 实现深度识别、骨骼追踪等高级功能

## 3.前置依赖

使用摄像头数据流控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Camera.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `CameraElement`；
3. 摄像头硬件已正确连接并可被系统识别；
4. 如需使用深度图像或高级功能，需确保 `Module.Camera` 模块已正确加载和配置。

## 4.控件 UI 效果

摄像头数据流控件在页面上显示一个矩形区域，实时渲染摄像头采集的图像内容。显示内容根据 `Display` 属性决定：

- `Color`：显示彩色摄像头画面；
- `Depth`：显示深度摄像头画面（灰度或伪彩色，取决于硬件和模块配置）。

## 5.配置文件样例

```xml
<CameraElement>
  <UIDisplay Left="220" Top="165" Width="300" Height="300" IsShow="True" ZIndex="20" UsePercent="False" />
  <CustomerConfig>
 <!--Display 只能选一个：Color 或 Depth。Color 表示彩色图像，Depth 表示深度图像-->
    <Stream CameraId="001" Display="Color/Depth"></Stream> <!-- 只能选一个Color或者Depth，Color是彩色图像 -->
     <!--具体摄像头功能设置请参考 Module.Camera 模块配置-->
  </CustomerConfig>
</CameraElement>

```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对摄像头控件：

- `Width` / `Height`：摄像头画面在页面上的显示尺寸；
- `ZIndex`：摄像头画面通常需要显示在较高层级，避免被背景或其他控件遮挡；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`；
- `IsShow`：控制控件是否显示。

## 7.CustomerConfig 参数说明

### Stream 节点

| 属性       | 必填 | 说明                                                         | 示例    |
| ---------- | ---- | ------------------------------------------------------------ | ------- |
| `CameraId` | 是   | 摄像头注册 ID，对应 `Module.Camera` 或系统识别到的摄像头标识 | `001`   |
| `Display`  | 是   | 显示模式。`Color` 显示彩色图像，`Depth` 显示深度图像         | `Color` |

### 属性说明

- **CameraId**：摄像头的唯一标识。该 ID 需要在 `Module.Camera` 模块配置或系统摄像头注册表中正确配置，控件才能找到对应的摄像头设备。
- **Display**：选择要显示的图像类型。
  - `Color`：彩色图像，普通 RGB 摄像头画面。
  - `Depth`：深度图像，通常由深度摄像头（如 Kinect、RealSense 等）提供，显示距离信息。

## 8.Module.Camera 模块配置

摄像头控件的高级功能（如设备注册、深度参数、分辨率设置等）通常由 `Module.Camera` 模块管理。具体配置方式请参考 `Module.Camera` 相关文档。

在 `TronSensingShow.dll.config` 中通常需要添加：

```xml
<modules>
  <!-- 其他模块 -->
  <module name="Camera" assembly="Module.Camera.dll" />
</modules>
```

> 模块的 exact 名称和 DLL 名称以实际项目或产品文档为准。

## 9.UIControlDict.xml 添加摄像头数据流控件

如果使用摄像头数据流控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<!--UI.Camera 控件包-->
<Element ViewType="CameraElement" AssemblyFile="UI.Camera.dll" TypeName="UI.Camera.CameraControl, UI.Camera, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.Camera.dll" TypeName="UI.Camera.CameraControlViewModel, UI.Camera, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
<!--UI.Camera End-->
```

## 10.部署说明

1. 将 `UI.Camera.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 将摄像头设备连接到电脑并安装正确的驱动程序；
3. 在 `TronSensingShow.dll.config` 中启用 `Module.Camera` 模块（如使用高级功能）；
4. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
5. 在页面 XML 中使用 `CameraElement`，配置正确的 `CameraId` 和 `Display`。

## 11.常见问题

### 摄像头画面不显示

- 检查摄像头硬件是否已正确连接并被系统识别；
- 检查 `CameraId` 是否与 `Module.Camera` 模块中注册的 ID 一致；
- 检查 `Display` 是否选择了摄像头支持的图像类型；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`，以及 `ZIndex` 是否被其他控件遮挡。

### 只能显示黑白/深度图像

- 如果希望显示彩色图像，将 `Display` 设为 `Color`；
- 如果设备只有深度摄像头，可能无法显示彩色图像。

### 画面卡顿或延迟

- 检查摄像头分辨率和帧率设置，过高的分辨率可能导致性能问题；
- 检查 `Module.Camera` 模块中的性能相关配置。

### 多个摄像头如何区分

- 每个摄像头应配置不同的 `CameraId`，在页面中使用对应的 ID 引用。

## 12.版本与硬件说明

- 彩色图像需要摄像头支持 RGB 采集；
- 深度图像需要摄像头支持深度采集（如 Kinect、Intel RealSense 等）；
- 具体支持的摄像头型号和分辨率取决于 `Module.Camera` 模块和运行时版本。
