---
name: sensing-platform-config
description: "Use when authoring, editing, or reviewing XML configuration files for the SensingPlatform low-code framework. Trigger on any task involving UIControlDict.xml, DataActivators.xml, EventFirer.xml, Pages.xml, Data.xml, or page-level XML files. Also trigger when the user asks about SensingPlatform controls, events, data sources, modules, or pages, or mentions the SensingPlatformDocs repo. This skill guides correct XML syntax, event wiring, control registration, data binding, and module integration."
---

# SensingPlatform XML Config Skill

SensingPlatform is a Windows low-code platform driven entirely by XML configuration. There is no source code to edit in a typical project — authors hand-write XML files that the runtime (`TronSensingShow.exe`) loads at startup. This skill encodes the platform's grammar, primitives, and common mistakes so generated configs are valid on the first try.

The platform's docs site is built from `D:\gits\SensingPlatformDocs` (MkDocs, Chinese). **The `docs/` folder and its `.md` files are documentation-only and do not ship to runtime projects.** This skill is for **authoring runtime configs**, not editing the docs.

## Project detection and folder structure

Before generating or editing configs, verify the working directory is actually a SensingPlatform project:

```bash
# A valid project contains at minimum:
#   TronSensingShow.exe          (runtime launcher)
#   SysConfig/                   (global registrations)
#   Shell/ or <ProjectFolder>/   (project-specific pages and data)
#   Resources/ or Resource/      (shared assets)
```

Typical project layout:

```
SensingProject/
├── TronSensingShow.exe          # Launcher (encrypted, do not modify)
├── *.dll                        # Runtime assemblies
├── TronSensingShow.dll.config   # App-level settings (modules, ProjectFolder, etc.)
├── SysConfig/
│   ├── UIControlDict.xml        # Control type registrations
│   ├── DataActivators.xml       # Data source type registrations
│   ├── EventFirer.xml           # Event action registrations
│   └── ConfigFragments.xml      # Reusable config fragments
├── Shell/                         # Default project folder (configurable)
│   ├── System.xml               # App-level config (resolution, screensaver, input)
│   ├── Pages/
│   │   ├── Pages.xml            # Page registry
│   │   ├── FrontPages.xml       # Foreground pages (persistent across navigation)
│   │   ├── BackPages.xml        # Background pages (persistent across navigation)
│   │   └── <PageName>/
│   │       ├── <PageName>.xml   # Page definition
│   │       └── resource/        # Page-local assets
│   └── Data/
│       ├── Data.xml             # Data source instances
│       └── <DataName>/          # Data source local files
├── Resource/ or Resources/      # Shared assets (images, audio, video, effects)
│   ├── splash.png               # Startup splash image
│   ├── Media/                   # Default media (click.wav, etc.)
│   └── Effect/                  # Transition effects (mostly built-in now)
└── Log/                         # Runtime logs (auto-generated)
```

### Configurable project folder

The project folder name defaults to `Shell` but can be changed in `TronSensingShow.dll.config`:

```xml
<appSettings>
  <add key="ProjectFolder" value="Shell"/>
</appSettings>
```

If the user says their project folder is named something else (e.g. `MyProject`, `Demo`), resolve all `Shell\...` paths against that folder name instead. The `ProjectFolder` setting also affects `UriKind="Application"` resolution for project assets.

### Key file roles

| File/Folder | Purpose |
|---|---|
| `TronSensingShow.dll.config` | App settings: `ProjectFolder`, module list (`<modules>`), `IsUseWebView`, `IsUseFFmpeg`, `FFmpegFolder` |
| `SysConfig/UIControlDict.xml` | Registers every control type that can appear in a page |
| `SysConfig/DataActivators.xml` | Registers every data source type that can appear in `Data.xml` |
| `SysConfig/EventFirer.xml` | Registers event actions that can be fired from `ClickEvent` / modules |
| `Shell/System.xml` | Resolution, display bounds, screensaver, audio, input device |
| `Shell/Pages/Pages.xml` | Registry of all navigable pages |
| `Shell/Data/Data.xml` | Instances of registered data sources with connection/config details |

## New project bootstrap

When the user wants to create a **new** SensingPlatform project from scratch, follow this order. Do not skip steps — the runtime loads configs in a fixed sequence and fails early if prerequisites are missing.

### Step 0: Verify runtime binaries exist

If the working directory does **not** contain `TronSensingShow.exe`, `SysConfig/`, and `Resource/` (or `Resources/`), stop and tell the user they need a valid runtime distribution first. These folders ship with the encrypted runtime binaries and should **not** be created from scratch — they come pre-populated with default registrations and shared assets. The user obtains them from the Troncell product release (NAS) or an existing project template.

What you should find in a valid runtime package:

```
ProjectRoot/
├── TronSensingShow.exe          # Already present
├── *.dll                        # Already present
├── TronSensingShow.dll.config   # Already present (edit in Step 2)
├── SysConfig/                   # Already present (edit registrations in Step 3)
│   ├── UIControlDict.xml        # May be empty or have defaults
│   ├── DataActivators.xml       # May be empty or have defaults
│   ├── EventFirer.xml           # May be empty or have defaults
│   └── ConfigFragments.xml      # Already present
├── Resource/ or Resources/      # Already present (add assets in Step 7)
│   ├── splash.png
│   └── Media/
└── Log/                         # Auto-created on first run
```

The only folder the user typically **creates** is the project content folder (default `Shell/`) and its subdirectories.

### Step 1: Create the project content folder (`Shell/`)

Create `Shell/` and its subdirectories. Everything else (`SysConfig/`, `Resource/`, `TronSensingShow.exe`) should already exist from the runtime package.

```
Shell/
├── System.xml
├── Pages/
│   ├── Pages.xml
│   └── <PageName>/
│       ├── <PageName>.xml
│       └── resource/
└── Data/
    ├── Data.xml
    └── <DataName>/
```

### Step 2: Configure `TronSensingShow.dll.config`

Set `ProjectFolder`, load required modules, and configure global flags. See [references/xml-patterns.md](references/xml-patterns.md) pattern 6 for the full skeleton.

### Step 3: Register primitives in `SysConfig/`

Populate the three registration files with the primitives the project will actually use. Do **not** copy every possible control — only register what the project needs, to keep startup fast.

1. **`SysConfig/UIControlDict.xml`** — register control types (e.g. `ImageElement`, `ImageButton`, `TextElement`, `FlipViewElement`).
2. **`SysConfig/DataActivators.xml`** — register data source types (e.g. `FolderData`, `ExcelData`) if the project uses dynamic data.
3. **`SysConfig/EventFirer.xml`** — register event firers (e.g. `ToDeviceDataEvent`) if the project talks to external devices.

### Step 4: Create `Shell/System.xml`

Define resolution, display bounds, screensaver, input device, and global audio. This is the runtime's first config file after registration.

### Step 5: Create the first page

1. Add the page to `Shell/Pages/Pages.xml` with `IsHome="True"`.
2. Create the folder `Shell/Pages/<PageName>/`.
3. Write `<PageName>.xml` with a basic `SysPage` + `UIDisplay` + at least one control (e.g. `ImageElement` background + `ImageButton`).

### Step 6: Add data sources (if needed)

Create `Shell/Data/Data.xml` and define instances of the data sources registered in Step 3.

### Step 7: Add resources

Place images, videos, and audio into:
- `Resource/` for shared assets
- `Shell/Pages/<PageName>/resource/` for page-local assets

### Step 8: Test and iterate

Run `TronSensingShow.exe`. If it fails, check `Log/` for XML parse errors or missing registration messages. The most common first-run failures are:
- Missing `UIControlDict.xml` registration for a control used in a page
- `Pages.xml` references a page folder that does not exist
- `Data.xml` references a data source type not registered in `DataActivators.xml`

## Five primitives

Every config task touches one or more of these:

1. **Page** (`Shell/Pages/<PageName>/<PageName>.xml`) — the smallest renderable unit. Pages are registered in `Shell/Pages/Pages.xml`, navigated by `F2` (next page), `F3` (home page), or `Navigate` events.
2. **Control / Element** — an XML node inside a page. Every control type must first be registered in `SysConfig/UIControlDict.xml` (binding `ViewType` to a CLR `TypeName` in a specific DLL) before it can be used. If no built-in control fits, you can develop a custom .NET 10 WPF control and host it via `CustomerElement` (see pattern 13).
3. **Data source** — registered globally in `SysConfig/DataActivators.xml` (binding `ConfigType` to a provider DLL), instantiated per-app in `Shell/Data/Data.xml`, referenced from controls via `<DataProvider>`.
4. **Event** — URL-shaped string (`Action?key1=value1&key2=value2`) emitted from `ClickEvent` / control hooks, dispatched on a bus.
5. **Module** — runtime extension (e.g. `Module.InputManager`, `Module.Camera`) loaded via `<modules>` in `TronSensingShow.dll.config` and wired into the event bus.

## Pre-registration rule (critical)

Before any control, data source, or event action can be used in a page, it must be **registered once** in the corresponding SysConfig file:

| Primitive | Registration file | Example |
|---|---|---|
| Control | `SysConfig/UIControlDict.xml` | `<Element ViewType="ImageElement" AssemblyFile="UI.Common.dll" TypeName="..." />` |
| Data source | `SysConfig/DataActivators.xml` | `<Data ConfigType="DbData" AssemblyFile="Data.Common" TypeName="..." />` |
| Event action | `SysConfig/EventFirer.xml` | `<Firer ActionName="ToDeviceDataEvent" AssemblyFile="..." TypeName="..." />` |

If a user asks for a config using a control that isn't registered, **add the registration snippet first** before generating the page XML.

## Authoring rules

### XML case-sensitivity
SensingPlatform XML is case-sensitive. `ViewType="ImageElement"` is valid; `viewtype="imageelement"` fails silently at runtime.

### `&amp;` escaping in event URLs
Event URLs live inside XML text nodes. The separator `&` **must** be escaped as `&amp;`:

```xml
<!-- Correct -->
<ClickEvent>Navigate?Page=HomePage&amp;TrackingData=welcome</ClickEvent>

<!-- Wrong -->
<ClickEvent>Navigate?Page=HomePage&TrackingData=welcome</ClickEvent>
```

When there is only one event, you can put the URL directly on `<ClickEvent>`. When there are multiple events, wrap each in `<Event>`:

```xml
<ClickEvent>
  <Event>PopupEvent?TargetPageName=HomePage&amp;...</Event>
  <Event>ClosePopup?TargetPageName=HomePage&amp;...</Event>
</ClickEvent>
```

### UriKind resolution (critical for file paths)

**`UriKind` is the #1 cause of missing images and broken popups.** Every `<ImageSource>`, `<FileSource>`, `<VideoSource>`, and event `EventPath`/`PathSource` must specify the correct `UriKind` or the runtime will not find the file.

| UriKind | Resolves against | Typical path style | Common use |
|---|---|---|---|
| `Relative` | Directory of the current `.xml` file | `resource\bg.png`, `Page\Detail.xml` | Page-local assets in the same folder |
| `Application` | App start directory (where `TronSensingShow.exe` lives) | `Shell\Pages\HomePage\resource\bg.png` | Most common — any asset under `Shell\` or `Resource\` |
| `Project` | The `Shell` folder | `Pages\HomePage\resource\bg.png` | Event URLs (`EventPath`, `PathSource`) that omit the `Shell\` prefix |
| `Absolute` | Physical disk path | `C:\Images\bg.png`, `D:\Media\video.mp4` | External/USB/network paths |
| `Web` | HTTP/HTTPS URL | `https://example.com/image.png` | `WebBrowserElement.DefaultAddress` |

**Common mistakes:**
- Using `UriKind="Application"` with a path that is actually relative to the page XML file → use `Relative`.
- Forgetting `UriKind` entirely → defaults to `Relative`, which breaks if the file is not next to the XML.
- Using `Project` with `Shell\Pages\...` prefix → `Project` already starts at `Shell`, so drop the `Shell\` part.
- Mixing `Application` and `Project` in the same project for the same folder → pick one and stay consistent.

### `{$Variable}` substitution
- Works **only** inside `<Template>` children bound via `<DataProvider>`.
- The variable name must match a column/field name exposed by the data source.
- Static controls without `<DataProvider>` cannot use `{$Var}`.
- Default runtime variables: `{$DataPath}` = `/Shell/Data`, `{$BasePath}` = `/Shell/Data/<DataName>`.

### DataProvider URL grammar
```
DataSourceName?CSTable=TableName&Where=[col like %value%]&Orderby=[DESC Name]&CustomKey=Value
```
- `CSTable` = the table/folder/sheet name inside the data source.
- `Where=[...]` and `Orderby=[...]` use square-bracket syntax.
- Any additional key/value pairs are passed to dynamic SQL (for `DbData`) or ignored by other providers.
- `TemplateID="{$Name}==Google"` on `<Template>` enables conditional template selection.

### Global event keys (reserved)
These work on **every** event action. Do **not** reuse these names as per-action parameters:
- `EDelay=1000` — delay before firing (ms)
- `TargetControl` / `TargetControlName` — send event to a specific control
- `UriKind` — path resolution mode
- `Loop=-1` — repeat forever; `StopLoop=True` to cancel
- `Async=true` — fire asynchronously to backend module (default `false` = UI thread)

### Transition easing triplet
The `Easing` attribute uses a three-part format: `Function,Mode,Parameter`.
Example: `Easing="CircularEase,EaseIn,1.0"`.
Functions: `BackEase, BounceEase, CircleEase, CubicEase, ElasticEase, ExponentialEase, Linear, QuadraticEase, QuarticEase, QuinticEase, SineEase`.

### Version awareness
The platform has three runtime generations:
- **V10+** (2026-01+) — .NET 10
- **V8.x** (2022-10+) — .NET 8
- **V7 and below** — .NET Framework 4.6

Some controls/events may be runtime-gated. When in doubt, keep configs compatible with the user's stated version.

## Validation checklist

Before accepting any generated SensingPlatform XML, verify:

1. [ ] Control `ViewType` is registered in `UIControlDict.xml` (include registration if missing).
2. [ ] Data source `Name`/`ConfigType` is registered in `DataActivators.xml` and defined in `Data/Data.xml`.
3. [ ] Event `Action` exists in the platform event list (see [references/events-reference.md](references/events-reference.md)).
4. [ ] `{$Variables}` in templates have a matching data source column.
5. [ ] All `&` inside event URLs are escaped as `&amp;`.
6. [ ] **Every `UriKind` is correct** — wrong UriKind is the #1 cause of missing images. `Application` for `Shell\...`, `Relative` for same-dir page assets, `Project` for event paths that omit `Shell\`.
7. [ ] `ZIndex` for popups is `>= 6` so they render above normal controls.
8. [ ] XML attribute names use exact casing (case-sensitive runtime).

## Reference files

- **[controls-reference.md](references/controls-reference.md)** — full catalog of ~46 control types, assemblies, and GroupView status.
- **[events-reference.md](references/events-reference.md)** — event actions, parameters, global keys, and multi-event syntax.
- **[data-sources-reference.md](references/data-sources-reference.md)** — data source types, `DataProvider` grammar, caching, and default variables.
- **[xml-patterns.md](references/xml-patterns.md)** — copy-pasteable XML skeletons for controls, transitions, data-bound templates, popups, and module registration.
- **[docs-lookup.md](references/docs-lookup.md)** — maps every control, event, data source, and module to its original Chinese doc file in `D:\gits\SensingPlatformDocs\docs\`. Use this to find which `.md` file to read for granular parameters.

Load the relevant reference file when the user needs granular details (e.g. "what parameters does PopupEvent accept?" or "show me a FlipView template example").

### Reading the original documentation

The Chinese markdown files in `D:\gits\SensingPlatformDocs\docs\` are the **authoritative source** for every control's `CustomerConfig` parameters, event arguments, and data source options. The skill's reference files summarize common patterns, but they do **not** reproduce every per-control parameter.

**Before generating XML for a specific control, event, or data source, read its original doc file.** Use [references/docs-lookup.md](references/docs-lookup.md) to find the correct file path.

Key rule: **Always read `docs/控件一览/CommonElement.md` first** when working with any control — it defines the universal `UIDisplay`, `ImageSource`, `DataProvider`, and `Items` syntax that every control uses. Then read the control-specific `.md` for its `CustomerConfig` parameters.
