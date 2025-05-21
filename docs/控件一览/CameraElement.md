摄像头数据流控件（CameraElement）

## 控件作用

数据流控件现在摄像头等数据。

## 控件 UI 效果

就是摄像头

## 配置文件样例

```xml
<CameraElement>
  <UIDisplay Left="220" Top="165" Width="300" Height="300" IsShow="True" ZIndex="20" UsePercent="False" />
  <CustomerConfig>
    <Stream CameraId="001" Display="Color/Depth"></Stream> <!-- 只能选一个Color或者Depth，Color是彩色图像 -->
    <!具体摄像头功能设置请看moudule.Camera/>
  </CustomerConfig>
</CameraElement>

```

## 配置说明

### 摄像头节点

#### 属性说明

    CameraId 摄像头注册的ID
    Display 深度和彩色图像

## UIControlDict.xml 添加数据流控件

如果使用摄像头数据流控件则需要在 UIControlDict.xml 中添加摄像头数据流控件

```
 <!--UI.Camera 控件包-->

<Element ViewType="CameraElement" AssemblyFile="UI.Camera.dll" TypeName="UI.Camera.CameraControl, UI.Camera, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Camera.dll" TypeName="UI.Camera.CameraControlViewModel, UI.Camera, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.Camera End-->
```

