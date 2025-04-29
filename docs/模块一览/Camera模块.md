
## 1. Module.Camera 模块

Camera中主要是集成了摄像头的外设模块，目前支持RealSense,Kinect,以及普通的摄像头处理摄像头的一些码流之外，还集成了一些视觉相关的算法，需要显示摄像头画面，可以和UI.Camera集合，详细请参考UI.Camera组件

### 1.1 CameraModule 模块集成，主要功能是接受和发送 Udp 协议的消息，以及传递图像信息和对图像进行处理

1. 在 TronSensingShow.exe.config 文件中的 modules 节点的最后配置 CameraModule 模块

```xml
<module assemblyFile="Module.Camera.dll" moduleType="Module.Camera.CameraModule, Module.Camera, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" moduleName="Module.Camera" startupLoaded="true" />
```

2. 在 SysConfig 文件夹的 EventFirer.xml 文件中配置Camera相关的事件发送的事件(目前还未定义相关事件,后续增加)

```xml
<Firer ActionName="ToDeviceDataEvent" AssemblyFile="Module.InputManager.dll" TypeName="Module.InputManager.Event.Fires.ToDeviceDataEventFirer, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
 </Firer>
```

3. 配置 Cameras 的相关信息，在CameraConfig.xml进行配置

   Type 为类型，分为 RealSense/Kinect/USB/Web
   Enable 是否启用，Id 为唯一的，方便后续发送消息使用，指定特定协议为Camera，
   目前Ojbect的Class仅支持Person，事件为人脸进入和人脸离开
   其中的 Event 就是接受到特定的命令后，做的一些动作，可进行配置

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Cameras>
	<!--Type="RealSense"/"Kinect"/"USB"/"Web"-->
	<Camera Id="001" Name="Com1" Type="RealSense" IP="" Port="Com3" Url="" Vendor="Intel" Algorithms="Face" IsShowControl="True" IsEnable="True" DetectionSkipFrameCount="1">
		<CustomerConfig>
			<ROIs IsShowRoiBox="True" IsShowFps="True" IsShowDistance="True">
				<ROI Data="10,10,1000,1000" Scale="1" >
					<!--DistanceMeterRange="*-1.2" - 第一个值是离摄像头距离近的值，第二个是离摄像头远的值
          例子 *-1.2 -> 表示1.2米内的物体有效
          -->
					<Object Class="Person"  DistanceMeterRange="0.5~0.9" EmotionRange="-1~-1" AgeRange="-1~-1">
						<EnterEvents>
							<Event>Navigate?Page=OPage</Event>
							<!--<Event>Navigate?Page=OPage</Event>
                <Event>Navigate?Page=OPage</Event>-->
						</EnterEvents>
						<LeaveEvents>
							<Event>Navigate?Page=AllPage</Event>
							<!--<Event>Navigate?Page=AllPage</Event>
                <Event>Navigate?Page=AllPage</Event>-->
						</LeaveEvents>
					</Object>
				</ROI>
			</ROIs>
		</CustomerConfig>
	</Camera>
</Cameras>



```

4. 界面上的动作按钮的配置
   Protocol 是协议类型, 目前支持 UDP/SerialPort/Scanner/Camera,Id是 Camera 的之前配置的唯一 Id，Data 发送到 Camera 的数据

```xml
     请参考UI.camera
```

```xml
5.配置功能解释
Id  =通过这个来找摄像头流
Name = 随意
Type = 目前支持的是realsense，后期会支持网络和kinent
IP = 网络摄像头的配置，等更新
Port = 端口摄像头的配置，等更新
Vendor = 哪个厂商的，目前只有interl，等更新
Algorithms = 功能模块，用于识别人脸还是其他，目前只支持face，其他等更新
IsShowControl = 是否更新画面
IsEnable = 是否启用
DetectionSkipFrameCount = 这个是跳帧，因为可以减少性能的消耗
Roi配置通过Data="10,10,1000,1000" 前两个值是框的左上角，后两个值是框的长和宽
Scale= 是图像的整体缩放

class = 这个功能是这个检测的class是什么 class=  类
DistanceMeterRange = 触发距离的 范围是多少 
EmotionRange = 暂定，不用
AgeRange = 暂定不用，年龄的范围
EnterEvents 是class进入范围后会进行触发
LeaveEvents = 是class离开返回后会触发，只要里面还有一个class都不会触发



测试模式：
IsShowRoiBox= 是否开启roi框，效果是roi的框和标记的框会显示在UI.Camera上
IsShowFps = 是否开启帧数显示，再左上角
IsShowDistance = 是否开启距离显示，会显示标记距离摄像头多远


```
