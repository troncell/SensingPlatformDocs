## 1. SyncManager 模块

SyncManager 用于实现多台设备之间的动作同步。典型场景：一台设备作为主控端（Server），其余设备作为接收端（Client），主控端上的页面跳转、弹窗等事件会自动广播到所有客户端。

该模块的实现位于 `SensingPlatform.Foundation.ScsCommunicator.SyncManager`，属于 Foundation 层。若不需要同步功能，可不在 `TronSensingShow.exe.config` 中注册该模块。

### 1.1 模块注册

在 `TronSensingShow.exe.config` 的 `modules` 节点中添加：

```xml
<module assemblyFile="SensingPlatform.Foundation.dll"
        moduleType="SensingPlatform.Foundation.ScsCommunicator.SyncManager, SensingPlatform.Foundation, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"
        moduleName="SyncManager"
        startupLoaded="true" />
```

### 1.2 同步参数配置

在 `SysConfig/System.xml` 中配置 `<Sync>` 节点：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<System>
  <Resolution Width="1920" Height="1080" />
  <DisplayBound Left="0" Top="0" Width="1920" Height="1080" />
  
  <!-- 多机同步配置 -->
  <Sync>
    <Server Enable="true" Address="192.168.1.100" Port="2500" />
    <Client Enable="false" Address="192.168.1.100" Port="2500" />
  </Sync>
</System>
```

| 属性 | 说明 |
| --- | --- |
| Server.Enable | 是否作为服务端。为 `true` 时，本机接收客户端连接并广播事件。 |
| Server.Address | 服务端监听的 IP 地址。 |
| Server.Port | 服务端监听的端口。 |
| Client.Enable | 是否作为客户端。为 `true` 时，本机连接到服务端并接收服务端广播的事件。 |
| Client.Address | 客户端要连接的服务端 IP。 |
| Client.Port | 客户端要连接的服务端端口。 |

同一台设备只能作为 Server 或 Client 之一，不能同时启用两者。

### 1.3 事件同步规则

配置完成后，本地触发的事件（如 `Navigate`、`PopupEvent` 等）在广播时会根据事件 URI 的同步类型决定如何发送：

- 事件 URI 未指定同步类型：默认向所有连接发送。
- 事件 URI 指定 `SyncType=Server`：仅当本机为 Server 时发送。
- 事件 URI 指定 `SyncType=Client`：仅当本机为 Client 时发送。
- 事件 URI 指定 `SyncType=None`：不同步，只在本地执行。

示例：让某个按钮点击事件只在 Server 端触发并同步到 Client：

```xml
<ImageButton name="SyncButton.png">
  <UIDisplay Left="100" Top="100" Width="200" Height="80" IsShow="True" ZIndex="2" UsePercent="False" />
  <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\btn.png</ImageSource>
  <ClickEvent>
    Navigate?Page=NextPage&amp;SyncType=Server
  </ClickEvent>
</ImageButton>
```

### 1.4 注意事项

1. 服务端和客户端必须能通过网络互通，防火墙需放行对应端口。
2. 同步消息为文本格式，接收端收到后会重新解析为本地事件并执行，因此两端的事件、页面、控件名称需要保持一致。
3. 如果不需要同步，建议不要注册该模块，避免事件分发产生额外网络开销。
4. 项目中还存在一个独立的 `Module.SyncManager.dll`，它通过自身 `dll.config` 配置。该模块是旧版/可选实现，与 Foundation 内置的 SyncManager 功能类似，通常二者选其一即可。
