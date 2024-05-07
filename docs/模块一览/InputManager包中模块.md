## 1. Module.InputManager 模块
 InputManager中主要是集成包含第三方的外设交付，UdpServerInput(Udp交互)，TcpServerInput(TCP交付)，SerialPortInput(串口交互)，SannerInput(扫描枪输入)
 ### 1.1 UdpServerInput模块集成，主要功能是接受和发送Udp协议的消息
 1.  在TronSensingShow.exe.config文件中的modules节点的最后配置UdpServerInput模块
 ```xml
<module assemblyFile="Module.InputManager.dll" moduleType="Module.InputManager.UdpServerInput, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" moduleName="Module.InputManager" startupLoaded="true" />
 ```
 2. 在SysConfig文件夹的EventFirer.xml文件中配置udp发送的事件
 ```xml
<Firer ActionName="ToDeviceDataEvent" AssemblyFile="Module.InputManager.dll" TypeName="Module.InputManager.Event.Fires.ToDeviceDataEventFirer, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  </Firer>
 ```
 3. 配置udp的相关信息，在InputManager.xml进行配置
 
    Type为类型，分为Client(作为Udp客户端)和Server(作为Udp服务端)， 同时都可以进行消息的收或发
    Enable是否启用，Id为唯一的，方便后续发送消息使用，指定特定的Udp，
    其中的Command就是接受到特定的命令后，做的一些动作，可进行配置
 ```xml
<?xml version="1.0" encoding="utf-8" ?>
<inputs>
  <Udps>
    <Udp Id="001" Ip="127.0.0.1" Port="6666" Type="Server" Enable="true" Provider="">
      <Commands>
        <Command Text="P1">
          <ClickEvent>Navigate?Page=6Page&amp;TrackingData=合伙人介绍页面</ClickEvent>
        </Command>
        <Command Text="P2">
          <ClickEvent>Navigate?Page=6Page&amp;TrackingData=合伙人介绍页面</ClickEvent>
        </Command>
      </Commands>
    </Udp>
    <Udp Id="002" Ip="127.0.0.1" Port="9895" Type="Client" Enable="false" Provider="">
      <Commands>
        <Command Text="P1">
          <ClickEvent>Navigate?Page=6Page&amp;TrackingData=合伙人介绍页面</ClickEvent>
        </Command>
        <Command Text="P2">
          <ClickEvent>Navigate?Page=6Page&amp;TrackingData=合伙人介绍页面</ClickEvent>
        </Command>
      </Commands>
    </Udp>
  </Udps>
</inputs>

```
4. 界面上的动作按钮的配置
    Protocol是协议类型, 目前支持UDP/SerialPort/Scanner,，Id是Udp的之前配置的唯一Id，Data发送到Udp的数据
 ```xml
      <ImageButton name="AboutUs.png">
        <UIDisplay Left="456" Top="701" Width="290" Height="94" IsShow="True" ZIndex="2" UsePercent="False" />
        <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\签到BUTTON.png</ImageSource>
        <ClickEvent>
          ToDeviceDataEvent?Id=003&amp;Protocol=UDP&amp;Data=right
        </ClickEvent>
      </ImageButton>
```
### 1.2 TcpServerInput模块集成，主要功能是接受和发送Tcp协议的消息
 1.  在TronSensingShow.exe.config文件中的modules节点的最后配置UdpServerInput模块
 ```xml
<module assemblyFile="Module.InputManager.dll" moduleType="Module.InputManager.TcpServerInput, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" moduleName="Module.InputManager" startupLoaded="true" />
 ```
 2. 在SysConfig文件夹的EventFirer.xml文件中配置udp/tcp等发送的事件
 ```xml
<Firer ActionName="ToDeviceDataEvent" AssemblyFile="Module.InputManager.dll" TypeName="Module.InputManager.Event.Fires.ToDeviceDataEventFirer, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  </Firer>
 ```
 3. 配置Tcp的相关信息，在InputManager.xml进行配置
 
    Type为类型，分为Client(作为Udp客户端)和Server(作为Udp服务端)， 同时都可以进行消息的收或发
    Enable是否启用，Id为唯一的，方便后续发送消息使用，指定特定的Udp，
    IsHex表示接受后的值会转成成HEX字符(16进制字符)
    其中的Command就是接受到特定的命令后，做的一些动作，可进行配置
 ```xml
<?xml version="1.0" encoding="utf-8" ?>
<inputs>
  <Tcps>
    <Tcp Id="001" Ip="127.0.0.1" Port="6666" Type="Server" Enable="true" IsHex="True" Provider="">
      <Commands>
        <Command Text="P1">
          <ClickEvent>Navigate?Page=6Page&amp;TrackingData=合伙人介绍页面</ClickEvent>
        </Command>
        <Command Text="P2">
          <ClickEvent>Navigate?Page=6Page&amp;TrackingData=合伙人介绍页面</ClickEvent>
        </Command>
      </Commands>
    </Tcp>
    <Tcp Id="002" Ip="127.0.0.1" Port="9895" Type="Client" Enable="false" Provider="">
      <Commands>
        <Command Text="P1">
          <ClickEvent>Navigate?Page=6Page&amp;TrackingData=合伙人介绍页面</ClickEvent>
        </Command>
        <Command Text="P2">
          <ClickEvent>Navigate?Page=6Page&amp;TrackingData=合伙人介绍页面</ClickEvent>
        </Command>
      </Commands>
    </Tcp>
  </Udps>
</inputs>

```
4. 界面上的动作按钮的配置
    Protocol是协议类型, 目前支持UDP/TCP/SerialPort/Scanner,，Id是TCP的之前配置的唯一Id，Data发送到Udp的数据，,IsHex表示是否以4bit作为16进制发送，比如1Byte AA
 ```xml
      <ImageButton name="AboutUs.png">
        <UIDisplay Left="456" Top="701" Width="290" Height="94" IsShow="True" ZIndex="2" UsePercent="False" />
        <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\签到BUTTON.png</ImageSource>
        <ClickEvent>
          ToDeviceDataEvent?Id=003&amp;Protocol=TCP&amp;Data=11001A&amp;IsHex=true
        </ClickEvent>
      </ImageButton>
```
