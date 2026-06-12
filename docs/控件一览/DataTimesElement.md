# 时间控件（DateTimesElement）

## 1.控件作用

时间控件用于在页面上自动显示当前计算机的日期、时间和星期信息。支持自定义显示格式、字体、颜色、位置等样式，适用于信息展示页、首页状态栏、展厅导览页等场景。

## 2.适用场景

- 首页或信息展示页显示当前时间
- 展厅页面右上角状态栏
- 需要显示日期、星期、时间的任何页面

## 3.前置依赖

使用时间控件前，必须满足以下条件：

1. 项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `DateTimesElement`。

## 4.控件 UI 效果

![Placeholder](../images/DataTimesElement.png)

## 5.配置文件样例

### 样例一：基础配置

```XML
<DateTimesElement>
	<UIDisplay Left="500" Top="0" Width="600" Height="110" IsShow="True" ZIndex="5" UsePercent="false" />
      <CustomerConfig>
        <Date Foreground="#FFFFFFFF" Family="微软雅黑" FontSize="30" CultureInfo="zh-CN" Alignment="Center" Left="0" Top="0" Format="yyyy-MM-dd"></Date>
        <Week Foreground="#FFFFFFFF" Family="微软雅黑" FontSize="30" CultureInfo="zh-CN" Alignment="Center" Left="200" Top="0" Format="dddd"></Week>
        <Time Foreground="#FFFFFFFF" Family="微软雅黑" FontSize="30" CultureInfo="zh-CN" Alignment="Center" Left="300" Top="0" Format="HH:mm:ss"></Time>
      </CustomerConfig>
</DateTimesElement>

```

### 样例二：完整样式配置

```XML
 <DateTimesElement>
                <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="6" UsePercent="False" />
                <CustomerConfig>
                  <!--LineStyle：ALine/TwoLine,可选配置-->
                  <Time FontFamily="[HarmonyOS Sans SC]" FontSize="50" FontWeight="Normal" Left="1541" Top="36" Format="HH : mm" Foreground="white" Culture="ZH-CN" />
                  <Date FontFamily="[HarmonyOS_Sans_SC]" Left="1721" Top="30" FontSize="27" FontWeight="Normal" Format="yyyy/MM/dd" Foreground="white" Culture="ZH-CN" />
                  <Week FontFamily="[HarmonyOS_Sans_SC]" FontSize="26" FontWeight="Normal" Left="1721" Top="66" Format="dddd" Foreground="white" Culture="ZH-CN" />
                </CustomerConfig>
              </DateTimesElement>

```

## UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。针对时间控件：

- `Width` / `Height`：定义时间控件的显示区域大小；
- `ZIndex`：如果时间显示在页面顶部或状态栏，建议设置较高层级；
- `UsePercent`：若需要按父容器百分比布局，可设为 `True`。

## CustomerConfig 参数说明

`CustomerConfig` 内可以配置 `Date`、`Week`、`Time` 三个节点，分别显示日期、星期和时间。

### 公共属性

| 属性                      | 必填 | 说明                                                     | 示例                             |
| ------------------------- | ---- | -------------------------------------------------------- | -------------------------------- |
| `Foreground`              | 否   | 字体颜色，支持颜色名称或十六进制值                       | `#FFFFFFFF`、`white`             |
| `Family` / `FontFamily`   | 否   | 字体名称                                                 | `微软雅黑`、`HarmonyOS Sans SC`  |
| `FontSize`                | 否   | 字体大小                                                 | `30`、`50`                       |
| `FontWeight`              | 否   | 字体粗细，如 `Normal`、`Bold`                            | `Normal`                         |
| `Culture` / `CultureInfo` | 否   | 区域文化，影响日期格式和语言，中文为 zh-CN，美国为 en-US | `zh-CN`、`en-US`、`ZH-CN`        |
| `Alignment`               | 否   | 文本对齐方式，如 `Left`、`Center`、`Right`               | `Center`                         |
| `Left`                    | 否   | 相对于控件的左边距                                       | `0`、`1541`                      |
| `Top`                     | 否   | 相对于控件的上边距                                       | `0`、`36`                        |
| `Format`                  | 否   | 日期/时间格式字符串                                      | `yyyy-MM-dd`、`HH:mm:ss`、`dddd` |

### Date 节点

用于显示日期。

| 属性     | 说明     | 示例                       |
| -------- | -------- | -------------------------- |
| `Format` | 日期格式 | `yyyy-MM-dd`、`yyyy/MM/dd` |

### Week 节点

用于显示星期。

| 属性     | 说明     | 示例                                  |
| -------- | -------- | ------------------------------------- |
| `Format` | 星期格式 | `dddd`（完整星期名称）、`ddd`（缩写） |

### Time 节点

用于显示时间。

| 属性     | 说明     | 示例                              |
| -------- | -------- | --------------------------------- |
| `Format` | 时间格式 | `HH:mm:ss`、`HH : mm`、`hh:mm tt` |

### LineStyle 属性

部分版本支持 `LineStyle` 配置：

| 取值      | 说明     |
| --------- | -------- |
| `ALine`   | 单行显示 |
| `TwoLine` | 双行显示 |

### 常用时间格式说明

| 格式符 | 含义          | 示例               |
| ------ | ------------- | ------------------ |
| `yyyy` | 四位年份      | `2023`             |
| `MM`   | 两位月份      | `03`               |
| `dd`   | 两位日期      | `17`               |
| `dddd` | 完整星期名称  | `星期五`、`Friday` |
| `ddd`  | 星期缩写      | `周五`、`Fri`      |
| `HH`   | 24小时制小时  | `14`               |
| `hh`   | 12小时制小时  | `02`               |
| `mm`   | 分钟          | `30`               |
| `ss`   | 秒钟          | `45`               |
| `tt`   | 上午/下午标记 | `PM`               |

更多格式说明请参考 [.NET 自定义日期和时间格式字符串](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-date-and-time-format-strings)。

# UIControlDict.xml 添加时间控件

如果使用时间控件，需要在 `UIControlDict.xml` 中添加注册节点。注册信息可能因拼写差异而不同，请选择与实际 DLL 匹配的一项：

### DateTimesElement

```XML

 <Element ViewType="DateTimesElement" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.DateTimesInfoControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.DateTimesViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```

## 部署说明

1. 确认项目目录中存在 `UI.Common.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 在页面 XML 中使用 `DateTimesElement` （与注册一致），配置 `UIDisplay` 和 `CustomerConfig`。

## 常见问题

### 时间不显示

- 检查 `UIDisplay` 的 `IsShow` 是否为 `True`；
- 检查 `Foreground` 颜色是否与背景色相同导致看不见；
- 检查 `ZIndex` 是否被其他控件遮挡。

### 时间不走动

- 时间控件通常会自动读取计算机系统时间，确保系统时间正常；
- 检查控件是否被其他异常中断导致定时器未启动。

### 日期/星期格式不对

- 检查 `Culture` / `CultureInfo` 是否设置为期望的区域，如 `zh-CN`；
- 检查 `Format` 字符串是否正确。

### 字体显示异常

- 检查 `Family` / `FontFamily` 指定的字体是否已安装在系统中；
- 字体名称中包含空格时，部分版本需要用方括号包裹，如 `[HarmonyOS Sans SC]`。

### 注册后运行时找不到控件

- 确认 `ViewType` 与 XML 标签拼写一致；
- 确认 `AssemblyFile` 和 `TypeName` 正确；
- 检查 `UI.Common.dll` 是否存在于应用根目录。

## 版本说明

- 该控件在不同版本中可能存在拼写差异，常见为 `DateTimesElement` ；
- 不同版本中属性名可能略有不同，如 `Family` 与 `FontFamily`、`CultureInfo` 与 `Culture`；
- 配置时请保持 `UIControlDict.xml` 中的 `ViewType`、XML 标签和文档描述一致。
