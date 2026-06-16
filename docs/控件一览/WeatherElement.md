# 天气控件（WeatherElement）

## 1.控件作用

天气控件用于在页面或弹出框中显示指定城市的实时天气信息，包括天气图标、温度和城市管理名称。控件通过高德地图天气 API 获取数据，并每 2 小时自动刷新一次。

## 2.适用场景

- 展厅首页天气展示
- 智慧楼宇/城市项目中的天气看板
- 需要实时天气信息的页面

## 3.前置依赖

使用天气控件前，必须满足以下条件：

1. 项目目录中存在 `UI.BdWeather.dll` 及其依赖 `Newtonsoft.Json`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `WeatherElement`；
3. 准备一个有效的高德地图 Web 服务 API Key，并配置在 `AmapApiKey` 节点中；
4. 确保运行环境可访问互联网（调用高德天气 API）。

## 4.控件 UI 效果

![Placeholder](../images/weather.png)

## 5.配置文件样例

```xml
<WeatherElement>
	<UIDisplay Left="0" Top="0" Width="500" Height="254" IsShow="True" ZIndex="5" UsePercent="false" />
	<CustomerConfig>
				<WeatherImage Left="40" Top="20" Width="96" Height="96" IsShow="true" ZIndex="5"/>
				<Temperature Left="160" Top="45" Width="180" Height="70" Size="56" ForegroundColor="#FFFFFFFF" Family="微软雅黑" IsShow="true" ZIndex="4" />
				<City Left="60" Top="130" Width="240" Height="40" Size="28" ForegroundColor="#FFFFFFFF" Family="微软雅黑" ShowText="无锡" Value="无锡" />
				<AmapApiKey Value="8115ff966647cf762d247ae9d1a73733" />
	</CustomerConfig>
</WeatherElement>

```

## UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。

## CustomerConfig 参数说明

### WeatherImage 节点

配置天气图标的位置与大小。

| 属性     | 必填 | 类型     | 默认值 | 说明                |
| -------- | ---- | -------- | ------ | ------------------- |
| `Left`   | 否   | `double` | `0`    | 图标左上角 X 坐标。 |
| `Top`    | 否   | `double` | `0`    | 图标左上角 Y 坐标。 |
| `Width`  | 否   | `double` | `0`    | 图标宽度。          |
| `Height` | 否   | `double` | `0`    | 图标高度。          |
| `IsShow` | 否   | `bool`   | `True` | 是否显示。          |
| `ZIndex` | 否   | `int`    | `0`    | 显示层级。          |

#### 天气图标资源

天气图标存储于应用根目录的 `Resource\Weather\` 下：

- `day\`：白天天气图标（6:00 ~ 18:00 使用）；
- `night\`：夜间天气图标（其他时间使用）；
- `undefined.png`：未获取到天气数据时的默认图标。

图标文件名需与高德 API 返回的天气状况一致，例如 `晴.png`、`多云.png`。
其中7:00-18:00为白天，其他为晚上

## Temperature(对应的温度)

配置温度文本的位置、大小与样式。

| 属性              | 必填 | 类型     | 默认值     | 说明                                         |
| ----------------- | ---- | -------- | ---------- | -------------------------------------------- |
| `Left`            | 否   | `double` | `0`        | 文本左上角 X 坐标。                          |
| `Top`             | 否   | `double` | `0`        | 文本左上角 Y 坐标。                          |
| `Width`           | 否   | `double` | `0`        | 文本区域宽度。                               |
| `Height`          | 否   | `double` | `0`        | 文本区域高度。                               |
| `IsShow`          | 否   | `bool`   | `True`     | 是否显示。                                   |
| `ZIndex`          | 否   | `int`    | `0`        | 显示层级。                                   |
| `Size`            | 否   | `double` | `0`        | 字体大小。                                   |
| `ForegroundColor` | 否   | `string` | `FFFFFFFF` | 字体颜色，格式为 `#AARRGGBB` 或 `AARRGGBB`。 |
| `Family`          | 否   | `string` | `微软雅黑` | 字体名称。                                   |

## City

配置城市名称的位置、大小与样式。

| 属性              | 必填 | 类型     | 默认值     | 说明                                                    |
| ----------------- | ---- | -------- | ---------- | ------------------------------------------------------- |
| `Left`            | 否   | `double` | `0`        | 文本左上角 X 坐标。                                     |
| `Top`             | 否   | `double` | `0`        | 文本左上角 Y 坐标。                                     |
| `Width`           | 否   | `double` | `0`        | 文本区域宽度。                                          |
| `Height`          | 否   | `double` | `0`        | 文本区域高度。                                          |
| `IsShow`          | 否   | `bool`   | `True`     | 是否显示。                                              |
| `ZIndex`          | 否   | `int`    | `0`        | 显示层级。                                              |
| `Size`            | 否   | `double` | `0`        | 字体大小。                                              |
| `ForegroundColor` | 否   | `string` | `FFFFFFFF` | 字体颜色。                                              |
| `Family`          | 否   | `string` | `微软雅黑` | 字体名称。                                              |
| `ShowText`        | 否   | `string` | `WuXi`     | 页面上显示的城市名称。                                  |
| `Value`           | 否   | `string` | 空字符串   | 用于查询天气的城市名称，需与高德 API 支持的城市名一致。 |

## AmapApiKey(对应的ApiKey)

    配置高德地图 Web 服务 API Key，用于获取实时天气数据。

| 属性    | 必填 | 类型     | 默认值   | 说明               |
| ------- | ---- | -------- | -------- | ------------------ |
| `Value` | 是   | `string` | 空字符串 | 高德地图 API Key。 |

> 如果没有配置 `AmapApiKey` 或城市名为空，控件将无法获取天气数据，会显示默认的 `undefined.png` 图标和 `No°` 温度。

## UIControlDict.xml 添加天气控件

如果使用天气控件则需要在 UIControlDict.xml 中添加天气控件，并且启用SensingData模块，并且通过AppPod配置软件

```xml
  <!-- 天气 -->
  <Element ViewType="WeatherElement" AssemblyFile="UI.BdWeather.dll" TypeName="UI.BdWeather.WeatherInfoControl, UI.BdWeather, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
	  <DataContext AssemblyFile="UI.BdWeather.dll" TypeName="UI.BdWeather.WeatherInfoViewModel, UI.BdWeather, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```

## 部署说明

1. 确认项目目录中存在 `UI.BdWeather.dll` 和 `Newtonsoft.Json.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 申请高德地图 Web 服务 API Key；
4. 准备天气图标资源，按 `Resource\Weather\day\`、`Resource\Weather\night\` 目录放置；
5. 在页面 XML 中使用 `WeatherElement`，配置 `UIDisplay`、`CustomerConfig` 和 `AmapApiKey`。

## 常见问题

### 天气不显示

- 检查 `UI.BdWeather.dll` 是否存在于应用根目录；
- 检查 `UIControlDict.xml` 中是否已注册 `WeatherElement`；
- 检查 `AmapApiKey` 是否配置正确且有效；
- 检查运行环境是否能访问互联网。

### 天气图标不显示

- 检查 `Resource\Weather\day\` 或 `Resource\Weather\night\` 下是否存在对应天气状况的图标文件；
- 图标文件名需与高德 API 返回的 `weather` 字段一致，例如 `晴.png`；
- 检查 `WeatherImage` 的 `IsShow` 是否为 `True`。

### 温度显示为 `No°`

- 检查 `City/Value` 是否为空；
- 检查 `AmapApiKey` 是否有效；
- 检查网络连接是否正常；
- 查看日志确认高德 API 返回的错误信息。

### 城市名称显示不正确

- 检查 `City/ShowText` 是否为想要显示的名称；
- 检查 `City/Value` 是否为高德 API 支持的城市名（如 `无锡`、`北京`）。

## 注意事项

- 当前实现使用高德地图实时天气 API，不再使用中国天气网；
- 控件每 2 小时自动刷新一次天气数据；
- 白天/夜间判断为 6:00 ~ 18:00 使用 `day` 目录图标，其他时间使用 `night` 目录图标；
- 建议为 `AmapApiKey` 配置独立的 Web 服务 Key，并注意 Key 的日调用量限制；
- 事件 URL 中的 `&` 必须转义为 `&amp;`。
