## 1. Module.InputManager 模块

InputManager 中主要是集成包含第三方的外设交付，UdpServerInput(Udp 交互)，TcpServerInput(TCP 交付)，SerialPortInput(串口交互)，SannerInput(扫描枪输入)

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

### 1.3 SerialInput 模块集成
