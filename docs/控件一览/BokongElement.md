播控控件（BoKongElement）

## 控件作用

通过远程控制播放内容。

## 控件 UI 效果

![Placeholder](../images/BoKong.png)

## 配置文件样例

```xml
<BoKongElement>
      <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
      <CustomerConfig>
        <BoKong Host = "http://192.168.3.101:8080" DeviceId="22" AreaDeviceId="43" ShowModelId="23">
        </BoKong>

      </CustomerConfig>
</BoKongElement>

```

## 配置说明

### 节点 BoKong

#### 属性说明

Host 服务器地址
DeviceId 设备ID
AreaDeviceId 区域设备ID  
ShowModelId 显示模式ID  

## UIControlDict.xml 添加播控控件

如果使用电子书控件则需要在 UIControlDict.xml 中添加电子书控件，并且启用SensingData模块，并且通过AppPod配置软件

```
  <!-- 播控 -->
  <Element ViewType="BoKongElement" AssemblyFile="UI.BoKong.dll" TypeName="UI.BoKong.BoKongControl, UI.BoKong, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="BoKong.dll" TypeName="UI.BoKong.BoKongViewModel, UI.BoKong, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
```


