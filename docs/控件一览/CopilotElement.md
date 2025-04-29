
# 智能助手控件（CopilotElement）

## 控件作用

可以进行对整个seingplayform进行控制。

## 控件 UI 效果

<!-- <img alt="CircleElement Preview Image" src="../images/CircleElement.png" width="900"> -->

暂无效果

## 配置文件样例

```
<?xml version="1.0" encoding="utf-8" ?>
<CopilotElement>
	<UIDisplay Left="220" Top="165" Width="300" Height="300" IsShow="True" ZIndex="20" UsePercent="False" />
	<CustomerConfig>
		<LLMs>
			<LLM Source="DeepSeek" Data="InConfig" />
		</LLMs>
		<McpServer></McpServer>

		<Director Id="001" Name="鸟头运动的导演" Enable="True" IsLoop="True" IsAutoPlay="True">
			<Chapter Type="Prepare" Id="001-001" WaitTime="00:00:00 000"  Name="回零章节" >
				<Event Name="回零" WaitTime="00:00:00 000" Duration="00:00:20 000" EndTriggerEvent="">
					ToDeviceDataEvent?Id=COM2&amp;Protocol=SerialPort&amp;Data=3f 08 a0 04 02 00 00 20 c7 21&amp;IsHex=true
				</Event>
				<Event Name="回初始运动位置" WaitTime="00:00:05 000" Duration="00:00:10 000" EndTriggerEvent="">
					ToDeviceDataEvent?Id=COM2&amp;Protocol=SerialPort&amp;Data=3f 08 a0 04 02 00 00 10 c7 21&amp;IsHex=true
				</Event>
			</Chapter>
			<Chapter Type="Perform" Id="001-002"  Name="向前章节" >
				<Event Name="向前运动" WaitTime="00:00:10 000" Duration="00:00:02 000" EndTriggerEvent="">
					ToDeviceDataEvent?Id=COM2&amp;Protocol=SerialPort&amp;Data=3f 08 a0 04 02 00 00 11 87 24&amp;IsHex=true
				</Event>
				<Event Name="向后运动" WaitTime="00:00:10 000" Duration="00:00:02 000" EndTriggerEvent="">
					ToDeviceDataEvent?Id=COM2&amp;Protocol=SerialPort&amp;Data=3f 08 a0 04 02 00 00 12 87 24&amp;IsHex=true
				</Event>
			</Chapter>
		</Director>
	</CustomerConfig>
</CopilotElement>

```

## 配置说明

### 参数具体详解
```
    该节点主要设置整个环形360的形态。

    属性说明

    LLM  =暂无
    Id  = 唯一标识符
    Name =名称
    WaitTime = 结束这个章节后的等待时间
    IsLoop = 这个章节是否要循环
    IsAutoPlay = 是否自动运行
    Type = 有两种选择Prepare  Perform  Prepare开始时只运行一次，Perform 如果循环则一直运行
    Duration = 这个程序运行时间
    WaitTime = 运行结束后等待时间
    EndTriggerEvent = 后期被动触发运行
ToDeviceDataEvent?Id=COM2&amp;Protocol=SerialPort&amp;Data=3f 08 a0 04 02 00 00 11 87  = 命令

```	
    
## UIControlDict.xml 添加环形卡片控件

如果使用环形卡片控件则需要在 UIControlDict.xml 中添加环形卡片控件

```
<!--UI.Copilot 控件包-->
<Element ViewType="CopilotElement" AssemblyFile="UI.Copilot.dll" TypeName="UI.Copilot.CopilotControl, UI.Copilot, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Copilot.dll" TypeName="UI.Copilot.CopilotControlViewModel, Copilot, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>

  </Element>
```
