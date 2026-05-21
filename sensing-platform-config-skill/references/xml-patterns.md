# XML Patterns

Copy-pasteable skeletons for common SensingPlatform config tasks.

## UriKind quick reference

Wrong `UriKind` is the most common cause of missing images and broken paths. Use this table to pick the right one.

```xml
<!-- Relative: resolves against the current .xml file's directory -->
<ImageSource UriKind="Relative">resource\bg.png</ImageSource>

<!-- Application: resolves against the app start dir (TronSensingShow.exe) -->
<ImageSource UriKind="Application">Shell\Pages\HomePage\resource\bg.png</ImageSource>

<!-- Project: resolves against the Shell folder (omit the Shell\ prefix) -->
<ClickEvent>PopupEvent?EventPath=Pages\HomePage\PopItems&amp;UriKind=Project</ClickEvent>

<!-- Absolute: full physical path -->
<ImageSource UriKind="Absolute">C:\Images\bg.png</ImageSource>

<!-- Web: HTTP URL -->
<WebBrowserElement>
  <CustomerConfig>
    <WebBrowser DefaultAddress="https://example.com" />
  </CustomerConfig>
</WebBrowserElement>
```

| UriKind | Base directory | Path example | Use for |
|---|---|---|---|
| `Relative` | Same folder as the `.xml` file | `resource\bg.png` | Page-local assets |
| `Application` | App start directory | `Shell\Pages\...` | Most shared assets |
| `Project` | `Shell` folder | `Pages\HomePage\...` | Event URLs (`EventPath`) |
| `Absolute` | Physical disk | `C:\Images\...` | External/USB/network paths |
| `Web` | HTTP/HTTPS | `https://...` | `WebBrowserElement` only |

## 1. Minimal page

```xml
<?xml version="1.0" encoding="utf-8"?>
<SysPage Name="HomePage">
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
  <Controls>
    <ImageElement Name="Background">
      <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" IsUseCache="True" />
      <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\bg.jpg</ImageSource>
    </ImageElement>
  </Controls>
</SysPage>
```

## 2. Grouping controls with XYContainerElement

`XYContainerElement` wraps multiple controls inside `<Controls>` so they move and scale as a single unit. This is the standard way to build composite UI pieces (e.g. an icon + label + button grouped together).

```xml
<XYContainerElement Name="navGroup">
  <UIDisplay Left="100" Top="100" Width="400" Height="300" IsShow="True" ZIndex="2" UsePercent="False" />
  <Controls>
    <ImageElement Name="icon">
      <UIDisplay Left="0" Top="0" Width="80" Height="80" IsShow="True" ZIndex="1" UsePercent="False" />
      <ImageSource UriKind="Relative">resource\icon.png</ImageSource>
    </ImageElement>
    <TextElement Name="label">
      <UIDisplay Left="100" Top="20" Width="200" Height="40" IsShow="True" ZIndex="1" UsePercent="False" />
      <TextSource>Navigation</TextSource>
    </TextElement>
    <ImageButton Name="btn">
      <UIDisplay Left="0" Top="100" Width="120" Height="50" IsShow="True" ZIndex="2" UsePercent="False" />
      <ImageSource UriKind="Relative">resource\btn.png</ImageSource>
      <ClickEvent>Navigate?Page=NextPage</ClickEvent>
    </ImageButton>
  </Controls>
</XYContainerElement>
```

Tips:
- Child coordinates are relative to the `XYContainerElement`'s `Left`/`Top`.
- `XYContainerElement` itself is a `GroupView` container, so it can be targeted by `Control` events using `TargetGroup`.

## 4. Control with transitions

```xml
<ImageButton Name="cta">
  <UIDisplay Left="1065" Top="1000" Width="155" Height="80" IsShow="True" ZIndex="5" UsePercent="False" />
  <ImageSource UriKind="Application">Shell\Pages\Common\btn.png</ImageSource>
  <ClickEvent>Navigate?Page=NextPage&amp;TrackingData=cta</ClickEvent>
  <Transitions>
    <Transition Name="move" Type="Translate" Delay="0" Duration="1000"
      From="0,0" To="300,0" TransitionOn="Loaded"
      Easing="CircularEase,EaseIn,1.0" Fill="HoldEnd"
      AutoReverse="False" Repeat="1" />
    <Transition Type="Scale" Delay="100" Duration="1000"
      From="0.8,0.8" To="1.2,1.2" TransitionOn="Loaded"
      Easing="Linear,EaseIn,1.0" Fill="Stop"
      AutoReverse="True" Repeat="Forever" />
    <Transition Type="Fade" Delay="0" Duration="1000"
      From="0.0" To="1.0" TransitionOn="Loaded"
      Easing="Linear,EaseIn,1.0" Fill="HoldEnd"
      AutoReverse="False" Repeat="1" />
  </Transitions>
</ImageButton>
```

Transition attributes:
- `Type`: `Translate | Scale | Rotate | Fade | Color`
- `TransitionOn`: `Program | Once | OnLoaded | DataContextChanged | Visibility`
- `Easing`: `Function,Mode,Parameter` — e.g. `CircularEase,EaseIn,1.0`
- `Fill`: `HoldEnd | Stop`
- `Repeat`: `Forever | 1..10`

## 3. Data-bound FlipView

```xml
<FlipViewElement Name="flipView">
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" />
  <DataProvider>AboutServiceData?CSTable=AboutService</DataProvider>
  <Items IsCacheUI="True">
    <Template Left="0" Top="0" Width="1920" Height="1080" TemplateID="10001">
      <XYContainerElement>
        <UIDisplay Left="0" Top="0" Width="1920" Height="1080" />
        <Controls>
          <ImageElement Name="resource">
            <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" IsUseCache="True" />
            <ImageSource UriKind="Application">Shell\Pages\AboutServicePage\resource\{$ImageName}</ImageSource>
          </ImageElement>
          <ImageButton Name="left">
            <UIDisplay Left="7" Top="474" Width="61" Height="102" IsShow="True" ZIndex="2" UsePercent="False" />
            <ImageSource UriKind="Application">Shell\Pages\AboutServicePage\resource\2.png</ImageSource>
            <ClickEvent>IndexChanged?Index={$LeftImage}&amp;Args=imageButton</ClickEvent>
          </ImageButton>
          <ImageButton Name="right">
            <UIDisplay Left="1852" Top="474" Width="61" Height="102" IsShow="True" ZIndex="2" UsePercent="False" />
            <ImageSource UriKind="Application">Shell\Pages\AboutServicePage\resource\1.png</ImageSource>
            <ClickEvent>IndexChanged?Index={$RightImage}</ClickEvent>
          </ImageButton>
        </Controls>
      </XYContainerElement>
    </Template>
  </Items>
  <CustomerConfig>
    <FlipView SliderFactor="0.2" Orientation="Horizontal" IsLoop="True" CanAutoPlay="False" IdleTime="10000" PageReload="False" />
  </CustomerConfig>
</FlipViewElement>
```

## 5. Popup with shared template

**Caller page (`HomePage.xml`):**

```xml
<PopupShowElement Name="PopItems">
  <IncludeTemplate>
    <FileSource UriKind="Application">Resource\CanMovePopup\PopupShow.xml</FileSource>
  </IncludeTemplate>
</PopupShowElement>

<ImageButton Name="openPopup">
  <UIDisplay Left="100" Top="100" Width="200" Height="100" IsShow="True" ZIndex="5" UsePercent="False" />
  <ImageSource UriKind="Application">Shell\Pages\HomePage\resource\btn.png</ImageSource>
  <ClickEvent>PopupEvent?TargetPageName=HomePage&amp;TargetControlName=PopItems&amp;X=0&amp;Y=0&amp;Height=1080&amp;Width=1920&amp;EventID=Detail&amp;UriKind=Application&amp;EventPath=Shell\Pages\HomePage\PopItems</ClickEvent>
</ImageButton>
```

**Shared template (`Resource/CanMovePopup/PopupShow.xml`):**

```xml
<Template>
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="6" UsePercent="False" />
  <CustomerConfig>
    <LayoutManager LayoutType="PopupShowLayout" CanContraint="True"
      BounceRect.X="0" BounceRect.Y="0"
      BounceRect.Width="1920" BounceRect.Height="1080"
      MaxScale="2" MinScale="0.45" ScaleMode="Disppear" />
  </CustomerConfig>
</Template>
```

**Popup content (`Shell/Pages/HomePage/PopItems/Detail/Detail.xml`):**

```xml
<Template>
  <SysPage>
    <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="1" UsePercent="False" />
    <Controls>
      <ImageButton>
        <UIDisplay Left="1480" Top="950" Width="158" Height="42" IsShow="True" ZIndex="5" UsePercent="False" />
        <ImageSource UriKind="Application">Resource\Picture\Others\close.png</ImageSource>
        <ClickEvent>ChangePopupState?State=Close&amp;Args=imageButton</ClickEvent>
      </ImageButton>
    </Controls>
  </SysPage>
</Template>
```

## 6. Video player

```xml
<VideoPlayerElement>
  <UIDisplay Left="43" Top="60" Width="780" Height="505" IsShow="True" ZIndex="2" UsePercent="False" />
  <FinishEvent>Navigate?Page=HomePage&amp;Args=imageButton</FinishEvent>
  <CustomerConfig>
    <VideoPlayer PlayMode="AutoPlay" LoopMode="One">
      <Player>
        <UIDisplay Left="0" Top="0" Width="780" Height="505" IsShow="True" ZIndex="1" UsePercent="False" />
        <VideoSource UriKind="Application">Shell\Pages\Common\test.wmv</VideoSource>
      </Player>
      <Controller>
        <UIDisplay Left="0" Top="507" Width="700" Height="48" IsShow="True" ZIndex="1" UsePercent="False" />
        <PlayButton>
          <UIDisplay Left="0" Top="0" Width="48" Height="48" IsShow="True" ZIndex="1" UsePercent="False" />
          <ImageSource UriKind="Application">Shell\Pages\icon-Play.png</ImageSource>
        </PlayButton>
        <PauseButton>
          <UIDisplay Left="0" Top="0" Width="48" Height="48" IsShow="True" ZIndex="1" UsePercent="False" />
          <ImageSource UriKind="Application">Shell\Pages\icon-Pause.png</ImageSource>
        </PauseButton>
        <Slider>
          <UIDisplay Left="70" Top="15" Width="623" Height="16" IsShow="True" ZIndex="1" UsePercent="False" />
          <Track>
            <ImageSource UriKind="Application">Shell\Pages\SliderMid.png</ImageSource>
          </Track>
          <Thumb>
            <ImageSource UriKind="Application">Resource\SliderMid.png</ImageSource>
          </Thumb>
        </Slider>
      </Controller>
    </VideoPlayer>
  </CustomerConfig>
</VideoPlayerElement>
```

## 7. Web browser with JS↔WPF bridge (WebBrowserElement)

`WebBrowserElement` embeds a full browser (Edge WebView2 or Chrome CEF). On **Edge mode**, JavaScript inside the page can send and receive messages with the WPF runtime, enabling HTML/JS UI to trigger platform events (Navigate, PopupEvent, etc.).

**Page XML:**

```xml
<WebBrowserElement Name="webBrowser">
  <UIDisplay Left="100" Top="100" Width="1720" Height="880" IsShow="True" ZIndex="1" UsePercent="False" />
  <CustomerConfig>
    <WebBrowser Type="Edge" Zoom="100">
      <!-- UriKind="Web" for HTTP; UriKind="Application" for local HTML files -->
      <DefaultAddress UriKind="Web">https://example.com</DefaultAddress>
    </WebBrowser>
  </CustomerConfig>
</WebBrowserElement>
```

**JavaScript bridge (Edge / WebView2 only):**

Save as `troncell-quorra-edge-1.0.js` next to your HTML, then import it:

```javascript
// troncell-quorra-edge-1.0.js — WPF WebView2 message bridge
export default {
    onMessage(fn) {
        const wv = window.chrome?.webview;
        if (wv) {
            wv.addEventListener('message', e => fn(e.data));
        } else {
            console.log('[WpfBridge] WebView2 not found');
        }
    },
    send(msg) {
        const wv = window.chrome?.webview;
        if (wv) {
            wv.postMessage(msg);
        } else {
            console.log('[WpfBridge] WebView2 not found, msg:', msg);
        }
    }
};
```

**HTML page using the bridge:**

```javascript
import bridge from './troncell-quorra-edge-1.0.js';

// Receive messages FROM WPF
bridge.onMessage(msg => {
    console.log(msg.Action, msg.Payload);
});

// Send messages TO WPF (trigger platform events)
bridge.send({
    WebPageName: 'controlEvent',
    WebControlName: 'Button',
    WebActionName: 'Click',
    Data: ['Navigate?Page=StarPWallPageA&amp;TrackingData=welcome'],
    Timestamp: Date.now()
});
```

**WPF → JS events:**

| Event | Purpose |
|---|---|
| `WebViewCallToJS` | Send a message from WPF to the JS bridge |
| `WebViewDoRefresh` | Refresh the browser (use `Control` event in newer versions) |
| `WebViewSourceChanged` | Change the loaded URL (use `SourceChanged` event in newer versions) |

Tips:
- `Type="Edge"` is required for the JS↔WPF bridge; CEF mode does not support two-way communication.
- `Zoom` is WPF-only scaling (100 = 100%).
- `DefaultAddress` accepts `UriKind="Web"` for URLs or `UriKind="Application"` for local `Shell\...\index.html` files.

## 8. App config (`TronSensingShow.dll.config`)

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <appSettings>
    <!-- Project folder name (default: Shell) -->
    <add key="ProjectFolder" value="Shell" />
    <!-- WebView support -->
    <add key="IsUseWebView" value="True" />
    <!-- FFmpeg video support -->
    <add key="IsUseFFmpeg" value="True" />
    <add key="FFmpegFolder" value="C:\\ffmpeg" />
    <!-- Product info -->
    <add key="ProductName" value="SensingPlatform Main" />
    <add key="ProjectName" value="SensingPlatform Main" />
  </appSettings>
  <modules>
    <module assemblyFile="Module.InputManager.dll"
      moduleType="Module.InputManager.UdpServerInput, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"
      moduleName="Module.InputManager" startupLoaded="true" />
    <module assemblyFile="Module.Camera.dll"
      moduleType="Module.Camera.CameraModule, Module.Camera, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"
      moduleName="Module.Camera" startupLoaded="true" />
  </modules>
</configuration>
```

## 9. EventFirer registration (`SysConfig/EventFirer.xml`)

```xml
<Firer ActionName="ToDeviceDataEvent" AssemblyFile="Module.InputManager.dll"
  TypeName="Module.InputManager.Event.Fires.ToDeviceDataEventFirer, Module.InputManager, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
```

## 10. System.xml skeleton

```xml
<?xml version="1.0" encoding="utf-8"?>
<System>
  <Resolution Width="1920" Height="1080" />
  <DisplayBound Left="0" Top="0" Width="1920" Height="1080" />
  <CultureInfo Value="zh-CN" />
  <DebugMode Value="True" />
  <ScreenSaver WaitingTime="00:00:20" SaverPage="ScreenPage" ToPage="WelcomePage">
    <Event>ToDeviceDataEvent?Id=001&amp;Protocol=UDP&amp;Data=right</Event>
  </ScreenSaver>
  <Shell>
    <MainRegion>
      <UIDisplay Left="0" Top="0" Width="1" Height="1" IsShow="True" ZIndex="1" UsePercent="True" />
    </MainRegion>
  </Shell>
  <Audios>
    <Audio Name="A" IsDefault="false" IsLoop="true" UriKind="Application">AudioSource/音频1.mp3</Audio>
  </Audios>
  <InputDevice Value="Mouse, Touch" />
</System>
```

## 11. Pages.xml registration

```xml
<?xml version="1.0" encoding="utf-8"?>
<Pages>
  <Page Name="HomePage" Folder="HomePage" IsHome="True" />
  <Page Name="DetailPage" Folder="DetailPage" />
</Pages>
```

Rules:
- `Name` must be unique; `Folder` defaults to `Name` if omitted.
- `IsHome="True"` marks the startup page. If omitted, the first page is the default home.
- Each page needs a matching folder under `Shell/Pages/` containing `<PageName>.xml`.

## 12. WPF XAML host (XamlElement)

Because the runtime is .NET 10 WPF, `XamlElement` can host any standard WPF markup — `TextBlock`, `TextBox`, `Border`, `Grid`, `StackPanel`, gradients, animations, etc. Paste XAML copied from Blend for Visual Studio or Visual Studio directly inside the `<Xaml>` node.

```xml
<XamlElement Name="wpfHost">
  <UIDisplay Left="0" Top="0" Width="1920" Height="1080" IsShow="True" ZIndex="2" UsePercent="False" />
  <Xaml>
    <!-- Option A: inline XAML -->
    <Border xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation">
      <Border.Background>
        <LinearGradientBrush>
          <LinearGradientBrush.GradientStops>
            <GradientStop Color="#FF008000" Offset="0" />
            <GradientStop Color="#FF0000FF" Offset="0.5" />
            <GradientStop Color="#FFFF0000" Offset="1" />
          </LinearGradientBrush.GradientStops>
        </LinearGradientBrush>
      </Border.Background>
      <TextBlock Text="Hello WPF" FontSize="48" Foreground="White" HorizontalAlignment="Center" VerticalAlignment="Center" />
    </Border>

    <!-- Option B: external file -->
    <!-- <FileSource UriKind="Application">Shell\Pages\HomePage\resource\custom.xaml</FileSource> -->
  </Xaml>
</XamlElement>
```

Tips:
- The root element inside `<Xaml>` can be any WPF `UIElement`.
- Use `xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"` on the root element.
- For complex layouts, design in Blend/VS, copy the generated XAML, and paste it here.

## 13. Custom WPF control (CustomerElement)

If no built-in control meets the requirement, develop a custom .NET 10 WPF control in Visual Studio / Blend, build it into a DLL, drop the DLL (and any PDB/EXE) into the app folder next to `TronSensingShow.exe`, then reference it via `CustomerElement`.

**Step 1: Register `CustomerElement` in `SysConfig/UIControlDict.xml`**

```xml
<Element ViewType="CustomerElement" AssemblyFile="UI.Common.dll"
  TypeName="UI.Common.SensingControl.CustomerControl, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
  <DataContext AssemblyFile="UI.Common.dll"
    TypeName="UI.Common.SensingView.CustomerControlViewModel, UI.Common, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
</Element>
```

**Step 2: Use the control on a page**

```xml
<CustomerElement Name="myCustomControl">
  <UIDisplay Left="100" Top="100" Width="400" Height="300" IsShow="True" ZIndex="2" UsePercent="False" />
  <Activator AssemblyFile="MyCustomControl.dll" TypeName="MyCustomControl.MyUserControl" />
</CustomerElement>
```

**Step 3: (Optional) Fire platform events from the custom control**

In the custom control's C# code:

```csharp
// Navigate to another page
SensingPlatformEventHelper.TriggerEvent("Navigate?Page=APage", this);

// Launch an external process
SensingPlatformEventHelper.TriggerEvent(
    "StartProcess?Path=C:\\Apps\\MyApp.exe&amp;Name=MyApp", this);
```

Tips:
- `AssemblyFile` = the DLL filename (no path; must be in the app folder).
- `TypeName` = the fully-qualified class name of the WPF user control.
- `CustomerElement` is itself a container, so child controls can be placed inside it just like `XYContainerElement`.
