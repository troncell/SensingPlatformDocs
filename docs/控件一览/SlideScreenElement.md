# 推拉屏控件（SlideScreenElement）

## 1.控件作用

推拉屏控件用于监听物理推拉屏的位置变化，当屏幕移动到预设点位时触发相应事件。控件支持两种工作模式：

- **拉萨模式（`Vendor="lasa"`）**：电动滑轨屏，通过 UDP 与服务端通信，自动移动到目标比例位置；
- **上海模式（`Vendor="shanghai"`）**：手动推拉屏，通过 UDP 接收位置编号，到达指定屏幕时触发事件。

当屏幕切换到新的预设位置时，控件会触发配置的 `ClickEvent`，并可通过 `{$ScreenName}` 模板变量引用当前位置的名称。

## 2.适用场景

- 展厅电动滑轨屏随位置切换内容
- 手动推拉屏到达点位后联动弹窗或切换页面
- 需要联动 PopupEvent 展示不同内容的滑轨/推拉屏

## 3.前置依赖

使用推拉屏控件前，必须满足以下条件：

1. 项目目录中存在 `UI.SlideScreen.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中注册 `SlideScreenElement`；
3. 推拉屏硬件或模拟服务已就绪，并能通过 UDP 发送/接收协议数据。

## 4.控件UI效果

![1781493848482](image/SlideScreenElement/1781493848482.mp4)

## 5.配置文件样例

### 5.1拉萨模式（电动屏）

```xml
<SlideScreenElement Name="SlideScreen">
        <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
        <ClickEvent>PopupEvent?TargetPageName=CBPage&TargetControlName=CBPop&X=0&Y=0&Height=1920&Width=1080&EventID={$ScreenName}&sheet={$sheet}&weizhi={$weizhi}&UriKind=Application&EventPath=Shell\Pages\CBPage\PopItems</ClickEvent>
        <CustomerConfig>
            <SlideScreen Vendor="lasa">
                <Setting>
                    <IP>127.0.0.1</IP>
                    <Port>8002</Port>
                    <RecvPort>8888</RecvPort>
                    <Debug>true</Debug>

                    <!--判断移动误差-->
                    <Tolerance>0.01</Tolerance>
                    <!--每块屏的区间位置  -->
                    <ScreenPositions>
                        <ScreenPosition Rate="0" Index="0" Name="A"/>
                        <ScreenPosition Rate="0.25" Index="1" Name="B"/>
                        <ScreenPosition Rate="0.5" Index="2" Name="C"/>
                        <ScreenPosition Rate="0.75" Index="3" Name="D"/>
                        <ScreenPosition Rate="1" Index="4" Name="E"/>
                    </ScreenPositions>
                </Setting>
            </SlideScreen>
        </CustomerConfig>
    </SlideScreenElement>
```

### 5.2上海手动推拉屏配置

```xml
<SlideScreenElement Name="SlideScreen">
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
    <ClickEvent>PopupEvent?TargetPageName=HomePage&TargetControlName=HomePop&X=0&Y=0&Height=1920&Width=1080&EventID={$ScreenName}Event&UriKind=Application&EventPath=Shell\Pages\HomePage\PopItems</ClickEvent>
    <CustomerConfig>
    <SlideScreen Vendor="shanghai">
        <Setting>
        <IP>127.0.0.1</IP>
        <RecvPort>6666</RecvPort>
        <Debug>false</Debug>
        <ScreenPositions>
            <ScreenPosition  Index="0" Name="A"/>
            <ScreenPosition  Index="1" Name="B"/>
            <ScreenPosition  Index="2" Name="C"/>
            <ScreenPosition  Index="3" Name="D"/>
            <ScreenPosition  Index="4" Name="E"/>
        </ScreenPositions>
        </Setting>
    </SlideScreen>
    </CustomerConfig>
</SlideScreenElement>
```

### 5.3点击屏幕按钮发送移动指令

```xml
<!-- 下一页-->
<ImageButton>
    <UIDisplay Left="100" Top="0" Width="180" Height="180" IsShow="True" ZIndex="1" UsePercent="False"/>
    <ImageSource UriKind="Application">Shell\Pages\Common\bg.png</ImageSource>
    <Content>
        <TextElement >
            <UIDisplay Left="0" Top="0" Width="180" Height="180" IsShow="True" ZIndex="1" UsePercent="False"/>
            <TextSource ForegroundColor="#FFFF0000" Family="微软雅黑" Size="50" CultureInfo="zh-CN" Alignment="Center">下一页</TextSource>
        </TextElement>
    </Content>
    <ClickEvent>IndexChanged?TargetPageName=HomePage&TargetControlName=SlideScreen&IndexString=Next&Index=-1</ClickEvent>
</ImageButton>
```

```xml
<!-- 上一页-->
<ImageButton>
    <UIDisplay Left="500" Top="0" Width="180" Height="180" IsShow="True" ZIndex="1" UsePercent="False"/>
    <ImageSource UriKind="Application">Shell\Pages\Common\bg.png</ImageSource>
    <Content>
        <TextElement >
            <UIDisplay Left="0" Top="0" Width="180" Height="180" IsShow="True" ZIndex="1" UsePercent="False"/>
            <TextSource ForegroundColor="#FFFF0000" Family="微软雅黑" Size="50" CultureInfo="zh-CN" Alignment="Center">上一页</TextSource>
        </TextElement>
    </Content>
    <ClickEvent>IndexChanged?TargetPageName=HomePage&TargetControlName=SlideScreen&IndexString=Pre&Index=-1</ClickEvent>
</ImageButton>
```

## 6.UIDisplay 说明

`UIDisplay` 用法参考 [CommonElement.md](CommonElement.md)。

## 7.CustomerConfig 参数说明

### 7.1SlideScreen 节点

| 属性     | 必填 | 类型                | 说明                                               |
| -------- | ---- | ------------------- | -------------------------------------------------- |
| `Vendor` | 是   | `lasa` / `shanghai` | 推拉屏类型。`lasa` 为电动屏，`shanghai` 为手动屏。 |

### 7.2Setting 节点

| 属性              | 必填 | 类型     | 默认值      | 说明                                             |
| ----------------- | ---- | -------- | ----------- | ------------------------------------------------ |
| `IP`              | 否   | `string` | `127.0.0.1` | 服务端 IP 地址，仅 `lasa` 模式用于发送移动指令。 |
| `Port`            | 否   | `int`    | `8002`      | 服务端端口，仅 `lasa` 模式用于发送移动指令。     |
| `RecvPort`        | 否   | `int`    | `8888`      | 本机接收反馈数据的 UDP 端口。                    |
| `Debug`           | 否   | `bool`   | `false`     | 是否显示调试面板。                               |
| `Tolerance`       | 否   | `double` | `0`         | 位置匹配误差范围，仅 `lasa` 模式生效。           |
| `ScreenPositions` | 是   | 节点集合 | —           | 预设屏幕位置集合。                               |

### 7.3ScreenPosition 节点

| 属性    | 必填       | 类型     | 说明                                                       |
| ------- | ---------- | -------- | ---------------------------------------------------------- |
| `Index` | 是         | `int`    | 屏幕位置索引，从 0 开始。                                  |
| `Name`  | 是         | `string` | 屏幕位置名称，用于替换 `{$ScreenName}` 模板变量。          |
| `Rate`  | 视模式而定 | `double` | 屏幕在滑轨上的比例位置（`0` ~ `1`），**`lasa` 模式必填**。 |

## 8.可接受的事件

### 8.1ClickEvent 事件

当推拉屏切换到新的预设位置时触发。当前位置名称可通过 `{$ScreenName}` 模板变量引用。

```xml
<ClickEvent>PopupEvent?TargetPageName=CBPage&TargetControlName=CBPop&EventID={$ScreenName}&UriKind=Application&EventPath=Shell\Pages\CBPage\PopItems</ClickEvent>
```

| 变量            | 说明                               | 示例          |
| --------------- | ---------------------------------- | ------------- |
| `{$ScreenName}` | 当前 `ScreenPosition` 的 `Name` 值 | `A`、`B`、`C` |

事件：复用常规弹出框事件，其中 **{$ScreenName}** 对应ScreenPosition传入的Name，替换效果为：**EventID=AEvent**， **EventID=BEvent**

### 8.2IndexChanged 事件

通过 `IndexChanged` 事件可以控制 `lasa` 电动屏移动到上一屏或下一屏。

```xml
<!-- 下一页 -->
<ClickEvent>IndexChanged?TargetPageName=HomePage&TargetControlName=SlideScreen&IndexString=Next&Index=-1</ClickEvent>

<!-- 上一页 -->
<ClickEvent>IndexChanged?TargetPageName=HomePage&TargetControlName=SlideScreen&IndexString=Pre&Index=-1</ClickEvent>
```

| 参数                | 说明                                            | 示例          |
| ------------------- | ----------------------------------------------- | ------------- |
| `TargetPageName`    | 目标页面名称                                    | `HomePage`    |
| `TargetControlName` | 目标推拉屏控件名称                              | `SlideScreen` |
| `IndexString`       | 移动方向，`Next` 下一屏，`Pre` 上一屏           | `Next`        |
| `Index`             | 兼容字段，当前实现中配合 `IndexString` 使用即可 | `-1`          |

## 9.UIControlDict.xml 添加推拉屏控件

如果使用推拉屏控件，需要在 `UIControlDict.xml` 中添加注册节点：

```xml
<Element ViewType="SlideScreenElement" AssemblyFile="UI.SlideScreen.dll" TypeName="UI.SlideScreen.SlideScreenControl, UI.SlideScreen, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.SlideScreen.dll" TypeName="UI.SlideScreen.SlideScreenControlViewModel, UI.SlideScreen, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

## 10.部署说明

1. 确认项目目录中存在 `UI.SlideScreen.dll`；
2. 在 `SysConfig/UIControlDict.xml` 中添加上方注册节点；
3. 根据硬件类型配置 `Vendor` 为 `lasa` 或 `shanghai`；
4. 配置 `IP`、`Port`、`RecvPort` 与硬件或模拟服务一致；
5. 在页面 XML 中使用 `SlideScreenElement`，配置 `UIDisplay`、`ClickEvent` 与 `CustomerConfig`。

## 11.常见问题

### 推拉屏无响应

- 检查 `UIControlDict.xml` 中是否已注册 `SlideScreenElement`；
- 检查 `Vendor` 是否拼写正确（仅支持 `lasa` 或 `shanghai`）；
- 检查 `IP`、`Port`、`RecvPort` 与硬件/模拟服务是否一致；
- 检查防火墙是否放行了对应 UDP 端口。

### 位置切换后没有触发事件

- 检查 `ClickEvent` 是否配置正确；
- 确认事件 URL 中的 `&` 已转义为 `&amp;`；
- 检查 `ScreenPosition` 的 `Name` 是否正确；
- `lasa` 模式需确认 `Rate` 与 `Tolerance` 设置合理。

### 拉萨模式移动不准确

- 检查 `ScreenPosition` 的 `Rate` 是否覆盖目标比例范围；
- 调整 `Tolerance` 误差范围，过小可能匹配不到，过大可能误匹配；
- 确认服务端正常返回 `rate:0.5` 格式的反馈数据。

### 上海模式收不到位置

- 检查 `RecvPort` 是否与发送端配置一致；
- 确认发送数据格式为可被解析的位置编号（例如第二位为数字）。

## 12.注意事项

- `lasa` 模式下 `ScreenPosition` 必须配置 `Rate`，`shanghai` 模式不依赖 `Rate`；
- `{$ScreenName}` 是当前代码唯一内置替换的模板变量，配置中的其他变量不会自动替换；
- 事件 URL 中的 `&` 必须转义为 `&amp;`；
- 控件卸载时会停止 UDP 监听线程与定时器，避免资源泄漏；
- 调试模式开启后会在控件上显示调试面板，仅用于开发测试。

## 13.通信协议（拉萨模式）

`lasa` 模式下控件通过 UDP 与服务端交互，常用指令如下：

| 指令             | 方向 | 说明                                          |
| ---------------- | ---- | --------------------------------------------- |
| `get_rate:`      | 发送 | 查询当前滑轨比例位置，每 500ms 发送一次。     |
| `to_rate:{Rate}` | 发送 | 移动到指定比例位置。                          |
| `to_left:`       | 发送 | 向左持续移动。                                |
| `to_stop:`       | 发送 | 停止移动。                                    |
| `to_right:`      | 发送 | 向右持续移动。                                |
| `rate:{value}`   | 接收 | 服务端返回的当前比例位置，例如 `rate:0.544`。 |

## 14.测试工具下载(解压双击运行)

[lasa 推拉屏服务测试](../../tools/slidescreen_test_server_lasa.zip)

[shanghai 推拉屏服务测试工具](../../tools/slidescreen_test_server_shanghai.zip)

[湖南滑轨测试工具](../../tools/hunan.zip)
