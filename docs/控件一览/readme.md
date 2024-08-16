### 控件的通用配置介绍
  一个基础的UI控件，一般由以下的几个通用的配置项组成:
  1. UIDisplay，必须项， 用于控制UI加载的位置相关的信息
  2. Transitions 可选项，用于控制UI加载的动画部分
  3. 
      BackEase
      模拟倒退效果，即动画开始或结束时先倒退一小段距离，然后再往前。
      具有 Amplitude 属性，控制倒退的幅度。
     
      BounceEase
      
      模拟弹跳效果。
      具有 Bounces 属性，控制弹跳次数。
      具有 Bounciness 属性，控制每次弹跳的弹性。
     
      CircleEase
      
      模拟圆形曲线运动。
      使用圆形运动的方式实现缓动效果。
     
      CubicEase
      
      模拟立方曲线运动。
      使用立方曲线实现缓动效果。
     
      ElasticEase
      
      模拟弹性运动。
      具有 Oscillations 属性，控制振荡次数。
      具有 Springiness 属性，控制弹性系数。
     
      ExponentialEase
      
      模拟指数曲线运动。
      具有 Exponent 属性，控制指数的大小。
     
      QuadraticEase
      
      模拟二次方曲线运动。
      使用二次方曲线实现缓动效果。
     
      QuarticEase
      
      模拟四次方曲线运动。
      使用四次方曲线实现缓动效果。
     
      QuinticEase
      
      模拟五次方曲线运动。
      使用五次方曲线实现缓动效果。
     
      SineEase
      
      模拟正弦曲线运动。
      使用正弦曲线实现缓动效果
     
  5. DataProvider 可选项，用户控制UI展示的数据源，
  6. CustomerConfig 可选项, 用于控制UI具体的表现形式的参数，每个控件都不太一样，详细参考每个特定的控件的配置
```xml
<?xml version="1.0" encoding="utf-8"?>
<SysPage Name="PWallPage">
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="True" IsUseCache="True" />
  <Controls>
    <ImageButton Name="resource">
      <!-- UIDisplay的配置说明:
        Left: 控件左上角的X坐标
        Top: 控件左上角的Y坐标
        Width: 控件的宽度
        Height: 控件的高度
        IsShow: 控件是否显示，目前支持的状态有：True, False
        ZIndex: 控件的层级，数值越大，层级越高
        UsePercent: 控件的位置和大小是否使用百分比，目前支持的状态有：True, False
        Rotate: 控件的旋转角度
        IsUseCache: 是否使用缓存，目前支持的状态有：True, False
      -->
      <UIDisplay Left="1065" Top="1000" Width="155" Height="80" IsShow="True" ZIndex="5" UsePercent="False" Rotate="35" />

      <!-- DataProvider的配置说明:
        wyfData: 数据源的名称
        CSTable: 数据源的具体分项表
        -->
      <DataProvider>wyfData?CSTable=Floors</DataProvider>
      <ImageSource UriKind="Application">Shell\Pages\Common\VideoPlayer\icon-Play.png</ImageSource>
      <ClickEvent>ToDeviceDataEvent?Id=001&amp;Protocol=TCP&amp;Data=11050000FF008EAA&amp;IsHex=True</ClickEvent>
      <Transitions>
        <!-- Transition的配置说明:
          Name: 动画名称，用于唯一标识一个动画,可不配置，如果配置的话，必须唯一，主要用户动画的控制，可通过事件进行控制，事件为Transition?TargetControlName=animation&TransitionName=move&Action=Play&Reverse=True
          Type: 动画类型，目前支持的动画类型有：Translate, Scale, Rotate, Fade, Color
          Delay: 动画延迟时间，单位为毫秒
          Duration: 动画持续时间，单位为毫秒
          From: 动画起始值，如Translate Scale 时格式为"x,y"，x和y为数值,如果是Color类型，格式为"#FF0000" 或者"#FF000000" ，如果是Fade时，格式为"0.1" 表示透明度，0表示全透明   
          To: 动画结束值，如Translate Scale 时格式为"x,y"，x和y为数值,如果是Color类型，格式为"#FF0000" 或者"#FF000000" ，如果是Fade时，格式为"1" 表示不透明，1表示全不透明
          TransitionOn: 动画触发时机，目前支持的触发时机有：Program（仅事件控制，默认不播放),Once,OnLoaded, DataContextChanged,Visibility
          Ease: 动画缓动效果，目前支持的缓动效果有：Linear, Quadratic, Cubic, Quartic, Quintic, Sinusoidal, Exponential, Circular, Elastic, Back, Bounce
          ReverseEase: 动画反向缓动效果，目前支持的缓动效果有：Linear, Quadratic, Cubic, Quartic, Quintic, Sinusoidal, Exponential, Circular, Elastic, Back, Bounce
          Fill: 动画结束后的状态，目前支持的状态有：HoldEnd, Stop
          AutoReverse: 动画是否自动反向播放，目前支持的状态有：True, False
          Repeat: 动画重复次数，目前支持的状态有：Forever, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
         -->
        <Transition Name="move" Type="Translate" Delay="0" Duration="1000" From='0,0' To="300,0" TransitionOn="Loaded" Easing="CircularEase,EaseIn,1.0" ReverseEasing="BackEase,EaseIn,1.0" Fill="HoldEnd" AutoReverse="False" Repeat="1" />
        <Transition Type="Scale" Delay="100" Duration="1000" From='0.8,0.8' To="1.2,1.2" TransitionOn="Loaded" Easing="Linear,EaseIn,1.0" ReverseEasing="Linear,EaseIn,1.0" Fill="Stop" AutoReverse="True" Repeat="Forever" />
        <Transition Type="Fade" Delay="0" Duration="1000" From='0.0' To="1.0" TransitionOn="Loaded" Easing="Linear,EaseIn,1.0" ReverseEasing="Linear,EaseIn,1.0" Fill="HoldEnd" AutoReverse="False" Repeat="1" />
      </Transitions>
      <CustomerConfig>
        <!--是针对此UI控件的一些特殊的配置，每个控件都不一样，详细参照每个UI控件的详细配置说明 -->
      </CustomerConfig>
    </ImageButton>
  </Controls>
</SysPage>
```
