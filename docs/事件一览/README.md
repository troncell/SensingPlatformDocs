## SensingPlatform 平台中的事件说明

事件配置和Http 中 Url Request 类似，采用如下格式进行：
Action?key1=value1&key2=value2
> [!NOTE]
> Action为事件的名称，后面的Query为事件所需要的参数，各个事件所需的参数都不一样，理解事件的过程就是理解参数逻辑的过程。

系统默认的全局Key如下:

**1. EDelay=1000 : 表示配置的事件会延时1000ms(毫秒)=1秒，触发该事件** 
**2. TargetControl=flipViewList : 表示配置的事件会触发给特定的UI控件，同时该组件有能力处理此事件，详细说明查看控件的具体配置** 
**3. UriKind= : 表示配置的事件，会用到文件或者路径之类的参数，用于定于获取文件的路径方式，Relative(相对当前控件的目录，如有Name的话，会有对应的文件夹),Application(程序的启动目录),Project(具体工程目录，默认为Shell的文件夹下** 
**4. ImageSource=trocell_logo.png : 表示配置的事件会用到图片，通常和UriKind参数一起使用，用于改变图片的显示，具体业务要去对应的控件上参考具体的配置功能，ImageElement就支持** 
**5. PathSource=troncell : 表示配置的事件会用到文件夹下的资源，通常和UriKind参数一起使用，用于改变资源的显示，具体业务要去对应的控件上参考具体的配置功能，FrameElement就支持** 

> [!WARNING]
> 这些全局的Key不要在特定事件中用同样的Key名称

平台事件可以在ImageButton下的ClickEvent下配置，

### 1. Navigate (导航事件)

此节点是按钮点击后触发事件的核心，也是框架配置项的核心。

在 ClickEvent 中根据不同的配置会做出不同的事件响应，以下配置文件样例中就是不同的响应效果；

#### 1.1 点击图片，可以跳转对应得页面

##### 1.1.1 跳页面

```xml
<!-- 点图片跳页面-->
 <ImageButton>
                <UIDisplay Left="1291" Top="595" Width="441" Height="261" IsShow="True" ZIndex="1" UsePercent="False" />
                <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\知识产权.png</ImageSource>
                <ClickEvent>Navigate?Page=StarPWallPageA&TrackingData=知识产权</ClickEvent>
              </ImageButton>
```

**说明**

Navigate 为响应方式（页面跳转）

Page=StarPWallPageA 就是所跳到的目标页面；


##### 1.1.2 发两个事件

```xml
<!-- 发出两个事件-->
<ImageButton Name="turnoff">
    <UIDisplay Left="1865" Top="985" Width="50" Height="50" IsShow="True"  ZIndex="10" UsePercent="False"/>
    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\turnoff.png</ImageSource>
    <ClickEvent>
        <Event IsLocal="True" SyncType="Client">Navigate?Page=GraphicPage</Event>
        <Event IsLocal="True" SyncType="Client">Navigate?Page=SweepPanelPage</Event>
    </ClickEvent>
</ImageButton>

```

#### 1.2 点击图片，可以跳转对应得弹出框

##### 1.2.1 跳弹框

```xml
<!-- 点图片跳弹出框-->
   <ImageButton>
                        <UIDisplay Left="516" Top="66" Width="134" Height="38" IsShow="True"
                          ZIndex="4" UsePercent="False" />
                        <ImageSource UriKind="Application">Shell\Pages\choutiPage\resource\more.png</ImageSource>
                        <ClickEvent>
                          PopupEvent?TargetPageName=CatalogPage&TargetControlName=MorePop&X=0&Y=0&Height=1080&Width=1920&EventID=More&UriKind=Application&EventPath=Shell\Pages\CatalogPage\PopItems&ThingId={$Id}&Id={$Id}
                        </ClickEvent>
                      </ImageButton>
```

**说明**

PopupEvent：是响应方式(打开悬浮控件)，

TargetPageName：在指定页面使用悬浮控件

&amp;是&的转义字符：表示与、和、连接的意思

TagetControlName：为所需使用悬浮控件的名称，弹出窗口的名称

X：为距左边框距离； Y：距上边框距离 ；Width：宽度； Height：高度,

EventId ：为所要使用到的悬浮控件的模板，如果是对应表格里得字段 EventID={$Photo}，photo 下得每一个在 PopItems 文件加下都对应一个文件夹和 xml

UriKind ：为配置路径的类型

Relative ：是相对于当前 xml 的位置

Application ：是相对于整个 demo 的位置。Absolute 是真实的物理路径，如 c:\Images\，EventPath 为模板所在的路径位置，此处还可以向控件传递参数，如示例中的 PageName(多个之间&amp;连接)，以上为指定固定位置出现悬浮控件，若想使得所需弹出的悬浮控件在随着点击位置改变而改变则需加入 LocationKind=Relative 即可；

##### 1.2.2 关闭弹框

```xml
<!-- 关闭弹出框-->
 <ImageButton>
        <UIDisplay Left="1765" Top="1000" Width="155" Height="80" IsShow="True" ZIndex="5" UsePercent="False" />
        <ImageSource UriKind="Application">Shell\Pages\CirclePage\resource\gohome.png</ImageSource>
        <ClickEvent>ChangePopupState?State=Close&Args=imageButton</ClickEvent>
      </ImageButton>
```

**说明**

ChangePopupState 是响应方式(改变悬浮控件的状态)

State=Close 状态为关闭。

##### 1.2.3 自动点击

```xml
<!-- 弹出后得页面上配置，某个按钮会自动点击 -->
<ImageButton>
    <UIDisplay Left="228" Top="1413" Width="622" Height="163" IsShow="True" ZIndex="2" UsePercent="False" />
    <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\FFZQHD\HDSP\非法证券活动按钮1高亮.png</ImageSource>
    <ClickEvent>PopupEvent?TargetPageName=HomePage&TargetControlName=FFZQHDSPPop&X=0&Y=0&SP=A2.mp4&Height=1080&Width=1920&EventID=FFZQHDSPEvent1&UriKind=Application&EventPath=Shell\Pages\HomePage\PopItems</ClickEvent>
    <CustomerConfig>
        <Button AutoClick="True" />
    </CustomerConfig>
</ImageButton>
```

**说明**

AutoClick：跳转页面默认选中点击。

### 2.CheckedEvent

和 ToggleButton 相结合，在自动跳转后得页面，通过 AutoClick，自动点击 ImageSourceChecked 得图片按钮，并跳转显示对应内容

```xml
<ToggleButton>
    <UIDisplay Left="790" Top="1005" Width="300" Height="90" IsShow="True" ZIndex="4" UsePercent="False" />
    <CustomerConfig>
      <ImageSource UriKind="Application">Shell\Pages\daoshiPage\img2\2fh.png</ImageSource>
      <ImageSourceChecked UriKind="Application">Shell\Pages\daoshiPage\img2\2fb.png</ImageSourceChecked>
      <CheckedEvent> PopupEvent?TargetPageName=daoshiPage&amp;TargetControlName=erlou&amp;X=0&amp;Y=0&amp;Height=1080&amp;Width=1920&amp;EventID=erlou&amp;UriKind=Application&amp;EventPath=Shell\Pages\daoshiPage\PopItems</CheckedEvent>
       <GroupName>img</GroupName>
       <Button AutoClick="True" />
      <IsChecked>False</IsChecked>
    </CustomerConfig>
</ToggleButton>
```
