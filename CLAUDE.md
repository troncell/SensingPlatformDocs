# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A **documentation-only** repository for **SensingPlatform** — a Windows-based, XML-configured low-code platform for interactive large-screen / touch installations (developed by Troncell). The actual platform binaries (`TronSensingShow.exe` and supporting DLLs) are **not** in this repo and are described as encrypted/internal-use-only. This repo only contains the user-facing MkDocs site that explains how to configure the platform.

**Documentation language is Chinese (zh-CN).** All filenames, headings, and prose are in Chinese. Do not translate existing pages to English when editing — match the existing Chinese style. Image alt text, code samples, and XML attribute names stay in English/ASCII.

## Build & serve commands

```bash
pip install mkdocs mkdocs-material   # one-time setup
mkdocs serve                         # local preview at http://127.0.0.1:8000
mkdocs build                         # static site → ./site/
```

There are no tests, no linters, and no formatting tools configured.

## Publishing pipeline

`.github/workflows/main.yml` runs on every push/PR to `master`:

1. `mkdocs build` → `./site/`
2. `zip -r SensingPlatform.zip ./*` inside `site/`
3. `ossutil cp` uploads `SensingPlatform.zip` to `oss://troncell-docs/zips/` (Aliyun OSS, `oss-cn-shanghai`).

Credentials live in the GitHub repo secrets `ACCESSKEYID` / `ACCESSKEYSECRET`. Do not break the workflow — a failed build means the published zip stops updating.

## Site structure (`docs/`)

The MkDocs nav in `mkdocs.yml` is **incomplete** — it lists only a curated subset. Many `.md` files exist that aren't in the nav (e.g. several control pages, `数据一览/*`, `事件一览/README.md`, `模块一览/*`, `产品介绍/System配置说明.md`). When adding a new control/data/event/module doc, decide whether it should also be added to `mkdocs.yml` `nav`; not every page needs to be.

The five top-level documentation areas mirror the platform's runtime architecture:

| Folder | Topic | Platform XML it documents |
|---|---|---|
| `docs/产品介绍/` | Product intro: deployment, usage, config layout | `TronSensingShow.dll.config`, `System.xml` |
| `docs/控件一览/` | **UI controls** — one `.md` per Element (~45 files) | `SysConfig/UIControlDict.xml`, page XMLs |
| `docs/数据一览/` | **Data sources** — DbData, ExcelData, FolderData, WebAPI, etc. | `SysConfig/DataActivators.xml`, `Shell/Data/Data.xml` |
| `docs/事件一览/` | **Events** — Navigate, PopupEvent, Control, SourceChanged, etc. (all in one README) | `SysConfig/EventFirer.xml` + per-control `ClickEvent` |
| `docs/模块一览/` | **Modules** — InputManager (UDP/TCP/Serial/SignalR), Camera, etc. | `<modules>` in `TronSensingShow.dll.config` |

`docs/控件一览/readme.md` (lowercase) is the **shared control-config primer** — it explains the universal `UIDisplay`, `Transitions`, `DataProvider`, `CustomerConfig` sections that every control doc references. New control pages should follow its conventions instead of re-explaining these common sections.

## Mental model of what's being documented

Understanding the four concepts below makes editing any page much easier — they are the platform's only abstractions, and almost every doc page exists to explain one of them.

1. **Page** (`Shell/Pages/<PageName>/<PageName>.xml`) — the smallest renderable unit. Pages are registered in `Shell/Pages/Pages.xml`, navigated by `F2` / `F3` keys or `Navigate` events.
2. **Control / Element** (e.g. `ImageElement`, `VideoPlayerElement`, `FlipViewElement`) — XML node inside a page. Every control type must first be registered in `SysConfig/UIControlDict.xml` (binding a `ViewType` to a CLR `TypeName` in a specific DLL) before it can be used on a page.
3. **Data source** — registered globally in `SysConfig/DataActivators.xml` (binding `ConfigType` to a provider DLL), instantiated per-app in `Shell/Data/Data.xml`, referenced from controls via `<DataProvider>Name?CSTable=...&Where=[...]&Key=Value</DataProvider>` (URL-shaped query string).
4. **Event** — URL-shaped string (`Action?key1=value1&key2=value2`) emitted from `ClickEvent` / control hooks, dispatched on a bus. Global keys (`EDelay`, `TargetControl`, `UriKind`, `Loop`, `Async`) work on every event; per-action keys live in `事件一览/README.md`.

Modules (e.g. `Module.InputManager`) extend the runtime via `<modules>` in `TronSensingShow.dll.config` and feed events into the bus from external devices.

## When editing docs

- **XML in code blocks must be runnable as-is** — readers copy/paste it. Don't add prose-only attributes that the platform doesn't actually parse.
- `&amp;` is intentional inside `<ClickEvent>` and `<Event>` bodies (it's the XML-escaped `&` that separates query params); don't "fix" these to bare `&`.
- Cross-reference style: link by relative path within `docs/` (e.g. `'./控件一览/ImageElement.md'`) the way `mkdocs.yml` does, not by absolute GitHub URL — except in the legacy `docs/README.md` table where absolute GitHub links are the existing convention.
- Images go into the nearest `image/` or `images/` folder and are referenced with relative paths.
- Filenames mixing Chinese and English are normal here (e.g. `产品基础使用说明.md`, `Camera模块.md`); preserve that convention rather than renaming to all-English.

## Versioning notes worth knowing

The product has three major runtime generations referenced throughout the deployment doc:

- **V10+** (current, since 2026-01) — built on **.NET 10**, requires .NET SDK 10.0.
- **V8.x** (since 2022-10) — built on **.NET Core / .NET 8**.
- **V7 and below** — built on **.NET Framework 4.6**.

When updating deployment / system-requirements text, keep all three sections in sync rather than silently dropping the older ones (existing customers still run V7/V8).

## SensingPlatform XML config authoring

For authoring or reviewing SensingPlatform XML runtime configs (e.g. `UIControlDict.xml`, `DataActivators.xml`, `EventFirer.xml`, `Pages.xml`, `Data.xml`, or page-level XML files), invoke the `sensing-platform-config` skill. It encodes the platform's grammar, control catalog, event syntax, data source patterns, and common gotchas so generated configs are valid on the first try.

The skill source lives in `sensing-platform-config-skill/` (tracked in this repo) and is installed at `~/.claude/skills/sensing-platform-config/`. See `sensing-platform-config-skill/README.md` for installation instructions.
