# 数字控件（NumberElement）

## 1.控件作用

数字控件用于显示数字滚动动画，效果类似于抽奖机、计时器或游戏分数滚动出最终数字。常用于数据展示、统计数字、倒计时、抽奖结果等场景，能够吸引用户注意力并增强视觉效果。

## 2.适用场景

- 数据统计展示（如用户数、销售额、访问量）
- 倒计时或计时器
- 抽奖结果展示
- 游戏分数或排名
- 需要数字动态变化的页面

## 3.前置依赖

使用数字控件前，必须满足以下条件：

1. 项目目录中存在 `UI.ShuZi.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `NumberElement`；
3. 在 `TronSensingShow.dll.config` 中启用 `SensingData` 模块（如需要动态数据）；
4. 通过 AppPod 配置软件完成相关数据配置（如需要）。

## 4.控件 UI 效果

![Placeholder](../images/shuzi.mp4)

## 5.配置文件样例

```xml
<NumberElement>
	<UIDisplay Left="0" Top="0" Width="300" Height="300" IsShow="True"  ZIndex="1" UsePercent="False" Opacity="1"/>
	<CustomerConfig>
		<Shu Number="1234567" Speed="100" Delay="5000"/>
	</CustomerConfig>
</NumberElement>

```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。

## 7.CustomerConfig 参数说明

### 7.1Shu 节点

| 属性     | 必填 | 说明                                                     | 示例      |
| -------- | ---- | -------------------------------------------------------- | --------- |
| `Number` | 是   | 最终要显示的数字                                         | `1234567` |
| `Speed`  | 否   | 数字滚动速度，数值越小滚动越快，数值越大滚动越慢         | `100`     |
| `Delay`  | 否   | 动画开始前的延迟时间，即多长时间后开始加载动画，单位毫秒 | `5000`    |

### 7.2属性说明

- **Number**：控件最终显示的数字。可以是整数，也可以是带有小数位的数字（具体以控件实现为准）。
- **Speed**：控制数字滚动的快慢。数值越小，每一位数字切换越快，整体动画完成时间越短；数值越大，滚动越慢，动画时间越长。
- **Delay**：页面加载后等待多长时间再开始播放数字滚动动画。

## 8.数字格式说明

| 格式   | 说明           | 示例         |
| ------ | -------------- | ------------ |
| 整数   | 直接显示整数   | `1234567`    |
| 千分位 | 每三位添加逗号 | `1,234,567`  |
| 小数   | 保留指定小数位 | `1234567.89` |

具体支持的格式取决于控件实现。

## 9.UIControlDict.xml 添加数字控件

如果使用数字控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<!--数字控件-->
<Element ViewType="NumberElement" AssemblyFile="UI.ShuZi.dll" TypeName="UI.ShuZi.ShuZiControl, UI.ShuZi, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.ShuZi.dll" TypeName="UI.ShuZi.ShuZiControlViewModel, UI.ShuZi, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 10.SensingData 模块与 AppPod 配置

如果数字控件需要从后台获取动态数据，通常需要：

1. 在 `TronSensingShow.dll.config` 中启用 `SensingData` 模块；
2. 通过 AppPod 配置软件下载后台数据；
3. 在页面中使用 `DataProvider` 绑定数据源，并将数据列绑定到 `Shu` 节点的 `Number` 属性。

动态数据绑定示例：

```xml
<DataProvider>NumberData?CSTable=Statistics</DataProvider>

<CustomerConfig>
    <Shu Number="{$TotalCount}" Speed="100" Delay="1000" />
</CustomerConfig>
```

## 11.部署说明

1. 将 `UI.ShuZi.dll` 复制到应用根目录（与 `TronSensingShow.exe` 同级）；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 如需动态数据，在 `TronSensingShow.dll.config` 中启用 `SensingData` 模块，并通过 AppPod 下载数据；
4. 在页面 XML 中使用 `NumberElement`，配置 `UIDisplay` 和 `CustomerConfig`。

## 12.常见问题

### 数字不显示

- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查 `Shu` 节点的 `Number` 是否配置正确；
- 检查 `UI.ShuZi.dll` 是否存在于应用根目录。

### 数字没有滚动动画

- 检查 `Speed` 是否设置合理，数值过大可能导致动画极慢；
- 检查 `Delay` 是否设置过大，导致动画延迟很久才开始；
- 检查 `UIControlDict.xml` 中的注册信息是否正确。

### 数字显示格式不对

- 检查 `Number` 值是否为有效数字；
- 如果支持 `Format` 参数，检查格式字符串是否正确。

### 动态数据不生效

- 检查 `DataProvider` 中的数据源名称和表名是否正确；
- 检查 `{$TotalCount}` 等变量名是否与数据源列名一致；
- 检查 `SensingData` 模块是否已启用。

### 数字被裁剪

- 增大 `UIDisplay` 的 `Width` 或 `Height`；
- 减小 `FontSize`（如果支持）；
- 检查 `UsePercent` 是否导致尺寸计算异常。

## 13.注意事项

- 数字控件的滚动效果会消耗一定性能，页面中大量使用时应谨慎；
- 建议根据实际数字位数调整控件宽度，避免数字被裁剪；
- 动态数据模式下，确保 `SensingData` 模块和 AppPod 配置正确；
- 不同版本的数字控件支持的参数可能不同，具体以实际 DLL 为准。
