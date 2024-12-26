## 1. Module.InputManager 模块

InputManager 中主要是集成包含第三方的外设交付，UdpServerInput(Udp 交互)，TcpServerInput(TCP 交互)，SerialPortInput(串口交互)，SannerInput(扫描枪输入),SignalR(SignalR 交互)

### 1.1 UdpServerInput 模块集成，主要功能是接受和发送 Udp 协议的消息

1. 在 TronSensingShow.exe.config 文件中的 modules 节点的最后配置 UdpServerInput 模块

```xml
<module assemblyFile="Module.InputManager.dll" moduleType="Module.InputManager.UdpServerInput, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" moduleName="Module.InputManager" startupLoaded="true" />
```

2. 在 SysConfig 文件夹的 EventFirer.xml 文件中配置 udp 发送的事件

```xml
<Firer ActionName="ToDeviceDataEvent" AssemblyFile="Module.InputManager.dll" TypeName="Module.InputManager.Event.Fires.ToDeviceDataEventFirer, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
 </Firer>
```

3. 配置 udp 的相关信息，在 InputManager.xml 进行配置

   Type 为类型，分为 Client(作为 Udp 客户端)和 Server(作为 Udp 服务端)， 同时都可以进行消息的收或发
   Enable 是否启用，Id 为唯一的，方便后续发送消息使用，指定特定的 Udp，
   其中的 Command 就是接受到特定的命令后，做的一些动作，可进行配置

```xml
<?xml version="1.0" encoding="utf-8" ?>
<inputs>
 <Udps>
   <Udp Id="001" Ip="127.0.0.1" Port="6666" Type="Server" Enable="true" Provider="">
     <Commands>
       <Command Text="P1">
         <ClickEvent>Navigate?Page=6Page&TrackingData=合伙人介绍页面</ClickEvent>
       </Command>
       <Command Text="P2">
         <ClickEvent>Navigate?Page=6Page&TrackingData=合伙人介绍页面</ClickEvent>
       </Command>
     </Commands>
   </Udp>
   <Udp Id="002" Ip="127.0.0.1" Port="9895" Type="Client" Enable="false" Provider="">
     <Commands>
       <Command Text="P1">
         <ClickEvent>Navigate?Page=6Page&TrackingData=合伙人介绍页面</ClickEvent>
       </Command>
       <Command Text="P2">
         <ClickEvent>Navigate?Page=6Page&TrackingData=合伙人介绍页面</ClickEvent>
       </Command>
     </Commands>
   </Udp>
 </Udps>
</inputs>

```

4. 界面上的动作按钮的配置
   Protocol 是协议类型, 目前支持 UDP/SerialPort/Scanner,，Id 是 Udp 的之前配置的唯一 Id，Data 发送到 Udp 的数据

```xml
     <ImageButton name="AboutUs.png">
       <UIDisplay Left="456" Top="701" Width="290" Height="94" IsShow="True" ZIndex="2" UsePercent="False" />
       <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\签到BUTTON.png</ImageSource>
       <ClickEvent>
         ToDeviceDataEvent?Id=003&Protocol=UDP&Data=right
       </ClickEvent>
     </ImageButton>
```

### 1.2 TcpServerInput 模块集成，主要功能是接受和发送 Tcp 协议的消息

1. 在 TronSensingShow.exe.config 文件中的 modules 节点的最后配置 UdpServerInput 模块

```xml
<module assemblyFile="Module.InputManager.dll" moduleType="Module.InputManager.TcpServerInput, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" moduleName="Module.InputManager" startupLoaded="true" />
```

2. 在 SysConfig 文件夹的 EventFirer.xml 文件中配置 udp/tcp 等发送的事件

```xml
<Firer ActionName="ToDeviceDataEvent" AssemblyFile="Module.InputManager.dll" TypeName="Module.InputManager.Event.Fires.ToDeviceDataEventFirer, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
 </Firer>
```

3. 配置 Tcp 的相关信息，在 InputManager.xml 进行配置

   Type 为类型，分为 Client(作为 Udp 客户端)和 Server(作为 Udp 服务端)， 同时都可以进行消息的收或发
   Enable 是否启用，Id 为唯一的，方便后续发送消息使用，指定特定的 Udp，
   IsHex 表示接受后的值会转成成 HEX 字符(16 进制字符)
   其中的 Command 就是接受到特定的命令后，做的一些动作，可进行配置

```xml
<?xml version="1.0" encoding="utf-8" ?>
<inputs>
 <Tcps>
   <Tcp Id="001" Ip="127.0.0.1" Port="6666" Type="Server" Enable="true" IsHex="True" Provider="">
     <Commands>
       <Command Text="P1">
         <ClickEvent>Navigate?Page=6Page&TrackingData=合伙人介绍页面</ClickEvent>
       </Command>
       <Command Text="P2">
         <ClickEvent>Navigate?Page=6Page&TrackingData=合伙人介绍页面</ClickEvent>
       </Command>
     </Commands>
   </Tcp>
   <Tcp Id="002" Ip="127.0.0.1" Port="9895" Type="Client" Enable="false" Provider="">
     <Commands>
       <Command Text="P1">
         <ClickEvent>Navigate?Page=6Page&TrackingData=合伙人介绍页面</ClickEvent>
       </Command>
       <Command Text="P2">
         <ClickEvent>Navigate?Page=6Page&TrackingData=合伙人介绍页面</ClickEvent>
       </Command>
     </Commands>
   </Tcp>
 </Udps>
</inputs>

```

4. 界面上的动作按钮的配置
   Protocol 是协议类型, 目前支持 UDP/TCP/SerialPort/Scanner,，Id 是 TCP 的之前配置的唯一 Id，Data 发送到 Udp 的数据，,IsHex 表示是否以 4bit 作为 16 进制发送，比如 1Byte AA

```xml
     <ImageButton name="AboutUs.png">
       <UIDisplay Left="456" Top="701" Width="290" Height="94" IsShow="True" ZIndex="2" UsePercent="False" />
       <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\签到BUTTON.png</ImageSource>
       <ClickEvent>
         ToDeviceDataEvent?Id=003&Protocol=TCP&Data=11001A&IsHex=true
       </ClickEvent>
     </ImageButton>
```

### 1.3 SerialPortInput 模块
SerialPortInput 模块主要用于与串口设备的通讯
开启功能需要在TronSensingShow.exe.config 文件中的 modules 节点配置 SerialPortInput 模块
  ```xml
<module assemblyFile="Module.InputManager.dll" moduleType="Module.InputManager.SerialPortInput, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" moduleName="Module.InputManager.SerialPortInput" startupLoaded="true"/>
  ```
  
#### 配置：
```xml

<Serials>
		<!-- port 串口名，Baudrate 波特率 ，Parity 奇偶校验位 ， Databits 数据位 ，Stopbits 停止位 -->
		<!-- 接入内置设备 Vender : 接入的设备，目前只有美斯特蓝牙 ，Interval ： 设备停止之后的事件触发时间，单位是毫秒-->
		<Serial Port="COM7" Baudrate="115200" Parity="None" Databits="8" Stopbits="One" Interval = "3000" Vender="Meisite">
			<Commands >
				<!-- <Command PairName = "ID" PairValue="22290054">

					<EnterEvent> PopupEvent?TargetPageName=APage&amp;TargetControlName=ShowPopItems&amp;X=0&amp;Y=0&amp;Height=1080&amp;Width=1920&amp;EventID=AEvent1&amp;UriKind=Application&amp;EventPath=Shell\Pages\APage\PopItems&amp;DeviceID=255887&amp;Device={$ID}
					</EnterEvent>
					<LeaveEvent> ClosePopup?TargetPageName=APage&amp;TargetControlName=ShowPopItems&amp;EventID=AEvent1
					</LeaveEvent>
				</Command> -->
				<Command PairName = "ID" PairValue="*">

					<!-- <Events> -->
					<!-- Type in Input in UI, from stepper- output, Both for UI and stepper's output -->
					<EnterEvent>
						<Event>PopupEvent?TargetPageName=StarPWallPage&amp;TargetControlName=PopItems&amp;X=0&amp;Y=0&amp;Height=1920&amp;Width=1080&amp;EventID=Introduce&amp;UriKind=Application&amp;EventPath=Shell\Pages\StarPWallPage\PopItems&amp;DeviceId={$ID}</Event>
						<Event> PopupEvent?TargetPageName=APage&amp;TargetControlName=ShowPopItems&amp;X=0&amp;Y=0&amp;Height=1080&amp;Width=1920&amp;EventID=AEvent1&amp;UriKind=Application&amp;EventPath=Shell\Pages\APage\PopItems&amp;DeviceId={$ID}</Event>
					</EnterEvent>
					<LeaveEvent>
						<Event>ClosePopup?TargetPageName=APage&amp;TargetControlName=ShowPopItems&amp;EventID=AEvent1
						</Event>
						<Event>ClosePopup?TargetPageName=StarPWallPage&amp;TargetControlName=PopItems&amp;EventID=Introduce
						</Event>
					</LeaveEvent>
				</Command>
			</Commands>
		</Serial>

    <Serial Port="COM19" Baudrate="115200" Parity="None" Databits="8" Stopbits="One" Interval = "100">
		<!-- Type in Input in UI, from stepper- output, Both for UI and stepper's output -->
		<Commands>

			<Command Text="A1" StartPulse="100" EndPulse="924">

				<!-- <Events> -->
				<!-- Type in Input in UI, from stepper- output, Both for UI and stepper's output -->
				<ClickEvent>
					<Event Type="Both">PopupEvent?TargetPageName=HomePage&amp;TargetControlName=PopItems2&amp;X=0&amp;Y=0&amp;Height=1080&amp;Width=1920&amp;EventID=AA&amp;UriKind=Application&amp;EventPath=Shell\Pages\HomePage\PopItems</Event>
				</ClickEvent>

			  </Command>
      </Commands>
    </Serial>
	</Serials>
```

如果不配置Vender的话，则只是一般的串口设备，如果配置了Vender，则需要配置对应的设备，目前支持美斯特蓝牙
配置Vender之后，由vender设备控制没配置，则通过串口设备控制


### 1.4  SignalR模块
SignalR模块用于远程控制，也可以用于SensingPlatFrom的跨设备传递事件
开启模块功能需要在TronSensingShow.exe.config 文件中的 modules 节点配置: 

```xml
<module assemblyFile="Module.InputManager.dll" 
			moduleType="Module.InputManager.SignalRClientInput, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" 
			moduleName="Module.InputManager.SignalR" startupLoaded="true"/>
```
使用，要在Module.InputManager.dll.config配置
```xml
<appSettings>
    <!-- Subkey 设备key，Addr 服务器地址 -->
		<add key="Subkey" value="1657500e9e8a491d8eb1d830b59162fd" />
		<add key="Addr" value="http://192.168.0.34:8080" />
	</appSettings>
	<Commands>
		<Command Id="P1">
			<Event>Navigate?Page=PartnerPage&amp;TrackingData=合伙人介绍页面</Event>
			<Event>Navigate?Page=PartnerPage&amp;TrackingData=合伙人介绍页面</Event>
			<Event>Navigate?Page=PartnerPage&amp;TrackingData=合伙人介绍页面</Event>
		</Command>
		<Command Id="P2">
			<Event>Navigate?Page=PartnerPage&amp;TrackingData=合伙人介绍页面</Event>
		</Command>
		<Command Id="P3">
			<Event>Navigate?Page=PartnerPage&amp;TrackingData=合伙人介绍页面</Event>
		</Command>
		<Command Id="P4">
			<Event>Navigate?Page=PartnerPage&amp;TrackingData=合伙人介绍页面</Event>
		</Command>
		<Command Id="P5">
			<Event>Navigate?Page=PartnerPage&amp;TrackingData=合伙人介绍页面</Event>
		</Command>
	</Commands>
```
