# CameraData数据源

## 数据源用途

主要用于显示VCA摄像头的实时数据(目前提供年人数，月人数以及日人数)，和签名的互动数据(通过UDP服务-默认5678端口和GameServer服务来实现-默认5001的端口)，当数据有更新的时候，CameraData会进行实施的分发出去

## 数据的配置

```xml
  <CameraData Name="CameraLocalData">
    <AutoFreshData Enable="true" IntervalTime="00:00:20"></AutoFreshData>
    <CustomerConfig>
      <Tables>
        <Table Name="Counters" IsRealtimeLoad="True">
          <DataQuery Value="select sum(increment) TotalCount,MonthCount,TodayCount from CounterEntity"></DataQuery>
        </Table>
      </Tables>
      <Game>
        <!--UDP的端口号-->
        <Port>5678</Port>
        <!--是否是调试模式-->
        <Debug>false</Debug>
        <!--签名退出时间-->
        <ExitPhotoTime>30</ExitPhotoTime>
        <!--显示最近的签名天数-->
        <SignatureDay>360</SignatureDay>
        <!--每块屏的区间位置 cm -->
        <SecurityKey>8d76984284fd4107b09472bea921d067</SecurityKey>
        <!--Camera列表-->
        <Cameras>
          <Camera Ip="192.168.3.143" Port="2555"/>
        </Cameras>
        <!--计数器的名称配置-->
        <Counters>
          <Counter>Counter 0</Counter>
        </Counters>
        <!--签名图片的本地服务器    -->
        <LocalServer>http://localhost:5001</LocalServer>
        <!--开始签名的事件    -->
        <Start>Navigate?Page=StarPWallPage&amp;IgnoreInput=False&amp;TrackingData=合伙人介绍页面</Start>
        <!--签名后的事件-->
        <Signature>ChangeWebViewSource?TargetPageName=StarPWallPage&amp;TargetControlName=popChrome&amp;SourcePath=\Shell\Pages\StarPWallPage\popChrome\wall\index.html?name={$FilePath}</Signature>
      </Game>
    </CustomerConfig>
  </CameraData>
```

## 配置讲解

这种数据源不能自定义数据列，目前提供就一条Counter的Table的数据，而且始终只有一条数据，字段为三个，分别为TotalCount，MonthCount，TodayCount。
其它的相关配置放在Game下的，具体的Game配置参考如下
### Game节点的配置
1. Port ，接受本机的UDP的端口
2. Cameras ，实时监控的摄像头的配置，包含IP地址和端口号
3. Counters ，摄像头下的计数器的名称，用于统计数据用的
4. LocalServer，用户接受签名的服务器地址，就是GameServer的地址(后续会用SensingHub)
5. Start, 接收到开始签名的触发的事件，可配置为和ClickEvent中的所有事件
6. Signature, 接受签名完成后的事件，可配置为和ClickEvent中的所有事件，其中{$FilePath}就是签名的图片