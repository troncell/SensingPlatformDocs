# 3D互动墙控件（InteractiveWall3DElement）

## 1.控件作用

3D 互动墙控件以三维墙的形式展示一系列卡片内容，用户可以通过点击卡片查看放大的详情。常用于展示企业发展历程、时间轴事件、产品演进阶段等内容。

**重要提示**：`InteractiveWall3DElement` 与 `Wall3DElement` 对应的是同一个实现（`UI.Wall3D.dll` 中的 [`Wall3DControl`](../../Product/UI/UI.3DWall/Wall3DControl.cs)）。当前代码只会解析 [`Wall3DControlViewModel`](../../Product/UI/UI.3DWall/Wall3DControlViewModel.cs) 中读取的 `Scenario3D`、`Animation`、`AutoMove` 等节点。旧文档中 `<InteractiveWall3D>`、`<Layout>`、`<Zoom>`、`<CardInfoLayout>`、`<AnimationTime>` 等节点在当前实现中**不会被解析**，配置后也不会生效。请使用下方与 `Wall3DElement` 一致的 `CustomerConfig` 结构，详细参数说明也请参考 [Wall3DElement.md](Wall3DElement.md)。

## 2.适用场景

- 企业发展历程展示
- 时间轴事件展示
- 产品版本演进展示
- 展厅互动 3D 墙

## 3.前置依赖

使用 3D 互动墙控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Wall3D.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `InteractiveWall3DElement`；
3. 如需动态加载内容，需在 `Shell/Data/Data.xml` 中配置数据源并在页面中使用 `DataProvider`。

## 4.控件UI效果

![Placeholder](../images/InteractiveWall3DElement.png)

## 5.配置文件样例

```xml
<InteractiveWall3DElement>
	<UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="false" IsUseCache="false" />
	<DataProvider>
		IntroductionData?CSTable=AboutUs
	</DataProvider>
	<CustomerConfig>
		<InteractiveWall3D>
			<Layout Per3DHeight="750" ItemSpan="150" />
			<Zoom ZoomValue="1.5" ZoomStatusAngle="-45" />
			<AnimationTime>
				1000
			</AnimationTime>
			<CardInfoLayout Width="500" Height="400" Left="1158" />
		</InteractiveWall3D>
	</CustomerConfig>
</InteractiveWall3DElement>

```

## UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对 3D 互动墙控件：

- `Width` / `Height`：定义 3D 互动墙的显示区域大小；
- `ZIndex`：注意 3D 墙与其他控件的层级关系；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`；
- `IsUseCache`：根据内存和性能需求设置是否缓存 UI。

## DataProvider 说明

通过 `DataProvider` 绑定数据源，数据源中的每一行会生成 3D 墙上的一张卡片。

```xml
<DataProvider>IntroductionData?CSTable=AboutUs</DataProvider>
```

- `IntroductionData`：数据源实例名称，需在 `Shell/Data/Data.xml` 中定义；
- `CSTable=AboutUs`：数据表/集合名称；
- 卡片内容通常通过数据源中的列绑定到 3D 墙的展示模板中。

## CustomerConfig 参数说明

### InteractiveWall3D 节点

`InteractiveWall3D` 是 3D 互动墙配置的根节点。

### Layout 节点

| 属性          | 必填 | 说明                                  | 示例  |
| ------------- | ---- | ------------------------------------- | ----- |
| `Per3DHeight` | 否   | 2D 画面的多少像素对应 3D 中的一个单位 | `750` |
| `ItemSpan`    | 否   | 卡片之间的间距或倾斜相关参数          | `150` |

### Zoom 节点

| 属性              | 必填 | 说明                         | 示例  |
| ----------------- | ---- | ---------------------------- | ----- |
| `ZoomValue`       | 否   | 点击某个卡片后放大的 3D 距离 | `1.5` |
| `ZoomStatusAngle` | 否   | 放大后 3D 墙的倾斜角度       | `-45` |

### AnimationTime 节点

| 属性   | 必填 | 说明                   | 示例   |
| ------ | ---- | ---------------------- | ------ |
| 节点值 | 否   | 动画过渡时间，单位毫秒 | `1000` |

### CardInfoLayout 节点

| 属性     | 必填 | 说明               | 示例   |
| -------- | ---- | ------------------ | ------ |
| `Width`  | 否   | 点开后面板的宽度   | `500`  |
| `Height` | 否   | 点开后面板的高度   | `400`  |
| `Left`   | 否   | 点开后面板的左边距 | `1158` |

### 属性说明

- **Per3DHeight**：控制 2D 像素与 3D 单位之间的映射比例。数值越大，3D 场景中的元素相对越小。
- **ItemSpan**：控制卡片之间的间距或排列方式，具体效果受 3D 墙实现影响。
- **ZoomValue**：点击卡片后，相机向卡片靠近的距离倍数。数值越大，放大效果越明显。
- **ZoomStatusAngle**：放大后 3D 墙的倾斜角度，负值通常表示向左倾斜。
- **AnimationTime**：卡片切换、放大、缩小等动画的过渡时间。
- **CardInfoLayout**：点击卡片后显示详细信息面板的位置和大小。

## UIControlDict.xml 添加 3D 互动墙控件

如果使用 3D 互动墙控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
  <Element ViewType="InteractiveWall3DElement" AssemblyFile="UI.Wall3D.dll" TypeName="UI.Wall3D.Wall3DControl, UI.Wall3D, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Wall3D.dll" TypeName="UI.Wall3D.Wall3DControlViewModel, UI.Wall3D, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```

> 注：`TypeName` 中的具体类名以实际 DLL 中的类型为准。

## 部署说明

1. 将 `UI.Wall3D.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 如需动态数据，在 `Shell/Data/Data.xml` 中配置数据源，并在页面中使用 `DataProvider`；
4. 在页面 XML 中使用 `InteractiveWall3DElement`，配置 `UIDisplay`、`DataProvider` 和 `CustomerConfig`。

## 常见问题

### 3D 墙不显示

- 检查 `UI.Wall3D.dll` 是否存在于应用根目录；
- 检查 `UIControlDict.xml` 中的注册信息是否正确；
- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`。

### 卡片不显示

- 检查 `DataProvider` 中的数据源名称和表名是否正确；
- 检查数据源中是否有数据；
- 检查卡片模板配置是否正确。

### 点击卡片后没有放大效果

- 检查 `Zoom` 节点的 `ZoomValue` 是否大于 0；
- 检查 `AnimationTime` 是否设置合理；
- 检查是否有上层控件拦截了点击事件。

### 详情面板位置不对

- 调整 `CardInfoLayout` 的 `Width`、`Height`、`Left`；
- 检查 `Layout` 的 `Per3DHeight` 和 `ItemSpan` 是否影响了整体布局。

### 动画卡顿

- 减少数据源中的卡片数量；
- 降低图片分辨率；
- 将 `IsUseCache` 设为 `True` 或 `False` 测试性能差异。

## 注意事项

- 3D 互动墙控件依赖 `UI.Wall3D.dll`，对显卡和内存有一定要求；
- 大数据量或高分辨率图片可能导致性能下降；
- 具体参数效果可能需要根据实际运行时效果进行微调；
- 该控件为 `GroupView` 控件，内部可能支持 `Items` 或 `Controls` 子节点，具体以实际版本为准。
