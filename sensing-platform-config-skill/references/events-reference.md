# Events Reference

Events in SensingPlatform are URL-shaped strings:

```
Action?key1=value1&key2=value2
```

Inside XML they use `&amp;` as the separator.

## Global keys (work on every event)

| Key | Meaning | Example |
|---|---|---|
| `EDelay` | Delay before firing (ms) | `EDelay=1000` |
| `TargetControl` / `TargetControlName` | Target control to receive the event | `TargetControlName=flipView` |
| `UriKind` | Path resolution mode | `UriKind=Application` |
| `Loop` | Repeat count; `-1` = forever | `Loop=3` |
| `StopLoop` | Cancel a running loop | `StopLoop=True` |
| `Async` | `true` = backend module; `false` = UI thread (default) | `Async=true` |
| `ImageSource` | New image resource (for `SourceChanged`) | `ImageSource=logo.png` |
| `PathSource` | New folder path (for `SourceChanged`) | `PathSource=troncell` |

> Do **not** reuse these names as per-action parameters in custom events.

## Event actions

### Navigate
Page navigation.

```xml
<ClickEvent>Navigate?Page=StarPWallPage&amp;TrackingData=知识产权</ClickEvent>
```

| Param | Meaning |
|---|---|
| `Page` | Target page name (must be registered in `Pages.xml`) |
| `TrackingData` | Optional tracking tag |
| `IgnoreInput` | `True`/`False` |

### PopupEvent
Open a popup overlay.

```xml
<ClickEvent>PopupEvent?TargetPageName=BriefingPage&amp;TargetControlName=PageLeftSecondShow&amp;X=0&amp;Y=0&amp;Height=841&amp;Width=1604&amp;EventID=PageHotBigBookShow&amp;UriKind=Application&amp;EventPath=Shell\Pages\BriefingPage\Items\PopupItems\SecondSho&amp;PageName={$PageName}</ClickEvent>
```

| Param | Meaning |
|---|---|
| `TargetPageName` | Page where the popup lives |
| `TargetControlName` | Name of the `PopupShowElement` control |
| `X`, `Y`, `Width`, `Height` | Popup geometry |
| `EventID` | Template folder name under `EventPath` |
| `EventPath` | Base path to popup template folders |
| `LocationKind=Relative` | Position popup at click location |
| `IsAllowMove` | `True`/`False` |
| `IsAllowRotate` | `True`/`False` |

### ClosePopup
Close a specific popup (or all popups on a page).

```xml
<ClickEvent>ClosePopup?TargetPageName=HomePage&amp;TargetControlName=StorePop&amp;EventID=Store&amp;UriKind=Application&amp;EventPath=Shell\Pages\HomePage\CategoryPopItems&amp;Filter=[LargeClassId={$Id}]</ClickEvent>
```

| Param | Meaning |
|---|---|
| `TargetControlName=ALL` | Closes **all** popups on the target page |

### ChangePopupState
Change popup behavior without closing it.

```xml
<ClickEvent>ChangePopupState?State=Close&amp;Args=imageButton</ClickEvent>
```

| `State` value | Effect |
|---|---|
| `Close` | Close the popup |
| `Pin` | Fix in place, no longer movable |
| `Unpin` | Allow moving again |

### Control
Generic control command (animation, video, PPT, buttons).

```xml
<ClickEvent>
  <Event>Control?Action=Play&amp;Index=0&amp;IndexString=Pre&amp;TargetControlName=imageButton</Event>
  <Event>Control?TargetPageName=HomePage&amp;TargetControlName=Fenli&amp;Action=Click</Event>
  <Event>Control?TargetPageName=SlidingScreen&amp;TargetGroup=A&amp;TargetControlName=2006&amp;Action=Check</Event>
</ClickEvent>
```

| `Action` | Effect |
|---|---|
| `Play` | Start playback |
| `Stop` | Stop |
| `Pause` | Pause |
| `Prev` / `Next` | Previous / next item |
| `Index` | Jump to numeric index |
| `Click` | Trigger an `ImageButton` click |
| `Check` / `UnCheck` | Trigger `ToggleButton` state |

### IndexChanged
Jump to a specific index in scrollable / flip controls.

```xml
<ClickEvent>IndexChanged?TargetControlName=FlipView&amp;Index=0&amp;IndexString=Pre&amp;Args=imageButton</ClickEvent>
```

| Param | Meaning |
|---|---|
| `Index` | Numeric index to jump to |
| `IndexString` | `Pre` / `Next` / `ToIndex` |
| `Move` | `ToIndex` with `Index` param |
| `ToInput` | `true`/`false` |

### SourceChanged
Change the source of an `ImageElement`, `ImageButton`, video, or frame folder.

```xml
<ClickEvent>SourceChanged?UriKind=Project&amp;TargetControlName=imageButton&amp;ImageSource=Page\HomePage\CheckBg.png</ClickEvent>
```

| Param | Meaning |
|---|---|
| `ImageSource` | New image path |
| `VideoSource` | New video path |
| `PathSource` | New folder path |

### Transition
Control a named animation on a control.

```xml
<Event>Transition?TargetControlName=animation&amp;TransitionName=move&amp;Action=Play&amp;Reverse=True</Event>
```

| Param | Meaning |
|---|---|
| `TransitionName` | Name of the `<Transition>` to target |
| `Action` | `Play` / `Stop` |
| `Reverse` | `True` reverses From/To |

### ChangeWebViewSource
Change the URL loaded in a `WebBrowserElement`.

```xml
<Event>ChangeWebViewSource?TargetPageName=StarPWallPage&amp;TargetControlName=popChrome&amp;SourcePath=\Shell\Pages\StarPWallPage\popChrome\wall\index.html?name={$FilePath}</Event>
```

### ToDeviceDataEvent
Send data to an external device via InputManager.

```xml
<Event>ToDeviceDataEvent?Id=001&amp;Protocol=UDP&amp;Data=right&amp;IsHex=False</Event>
```

| Param | Meaning |
|---|---|
| `Id` | Device/command ID |
| `Protocol` | `UDP` / `TCP` / `SerialPort` / `SignalR` |
| `Data` | Payload string |
| `IsHex` | `True` if data is hex-encoded |
| `SubKey` | Target device sub-key (SignalR) |

### Shutdown
Restart or shut down.

```xml
<Event>Shutdown?Type=Computer</Event>
```

| `Type` | Effect |
|---|---|
| `Application` | Close the app |
| `Computer` | Shut down the PC |
| `Reboot` | Restart the PC |
