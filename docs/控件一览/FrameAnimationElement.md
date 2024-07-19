
# 帧动画控件（FrameAnimationElement）

## 控件作用

帧动画控件以序列帧的方式播放动画，它的特点是支持png透明图片的动画，建议一些小动画用这总方式，大图片序列帧的方式，可能对影响有影响。

## 控件 UI 效果

![输入图片说明](https://sensingstore.oss-cn-shanghai.aliyuncs.com/Troncell/SensingPlatfrom/FrameAnimation1.gif)

![输入图片说明](https://sensingstore.oss-cn-shanghai.aliyuncs.com/Troncell/SensingPlatfrom/FrameAnimation2.gif)

## 配置文件样例

```xml
<FrameAnimationElement>
      <UIDisplay Left="100" Top="100" Width="515" Height="292" IsShow="True" ZIndex="1" UsePercent="false" IsUseCache="True" />
      <!-- PathSource帧动画资源路径:
        UriKind: 资源路径类型，Application表示应用内路径，Absolute表示绝对路径，Relative表示相对路径，Project表示工程路径
        Filter: 资源过滤器，支持多个格式，用逗号分隔
      -->
      <PathSource UriKind="Application" Filter="*.png,*.jpg,*.bmp">Shell\Pages\StarPWallPage\仙鹤序列帧</PathSource>
      <CustomerConfig>
        <!-- 帧的Image控制展示:
          AutoHeight: 是否自适应高度
          Stretch: 图片拉伸方式，None表示不拉伸，Fill表示填充，Uniform表示等比例缩放，UniformToFill
           -->
        <Image AutoHeight="true" Stretch="None"/>
        <!-- Frame控制帧率:
          Interval: 帧率间隔，单位ms
          Repeat: 重复次数，Forever表示无限循环
          AutoPlay:是否加载后自动播放动画，默认是自动播放 
           -->
        <Frame Interval="50" Repeat="1" AutoPlay="False" />
      </CustomerConfig>
    </FrameAnimationElement>
```

## 配置说明

详细的配置说明，请参照配置样例中的注释文件

## 支持的事件

Control事件，用于控制动画的播放，暂停以及停止，如 Action=Play/Pause/Stop

## UIControlDict.xml 添加飞图控件

如果使用帧动画控件则需要在 UIControlDict.xml 中添加帧动画控件

```
 <!--UI.Common 控件包-->
  <Element ViewType="FrameAnimationElement" AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingControl.FrameAnimationControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
    <DataContext AssemblyFile="UI.Common.dll" TypeName="UI.Common.SensingView.FrameAnimationElementViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
  </Element>
  <!--UI.Common  END-->
```
