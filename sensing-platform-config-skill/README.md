# SensingPlatfoRm Config Skill

This is a Claude Code skill that helps author XML configuration files for the SensingPlatform low-code framework.

## Installation

Copy this folder to your Claude Code skills directory:

```bash
# Windows
xcopy /E /I "sensing-platform-config-skill" "%USERPROFILE%\.claude\skills\sensing-platform-config"

# Or from the repo root
mkdir -p ~/.claude/skills
rsync -av sensing-platform-config-skill/ ~/.claude/skills/sensing-platform-config/
```

Then restart Claude Code. The skill will auto-trigger when you work with SensingPlatform XML configs.

## What it covers

- **Controls**: ~46 UI element types, their assemblies, and registration in `UIControlDict.xml`
- **Events**: URL-shaped event syntax, global keys, and all platform event actions
- **Data sources**: `DataActivators.xml` registration, `DataProvider` URL grammar, template binding
- **Modules**: `Module.InputManager` (UDP/TCP/Serial/SignalR) and `Module.Camera`
- **XML patterns**: Copy-pasteable skeletons for pages, controls, transitions, popups, video players, etc.

## When to use

Invoke or let auto-trigger when:
- Writing/editing `UIControlDict.xml`, `DataActivators.xml`, `EventFirer.xml`, `Pages.xml`, `Data.xml`
- Writing page-level XML files (`Shell/Pages/**/*.xml`)
- Configuring modules in `TronSensingShow.dll.config`
- Asking about SensingPlatform controls, events, data sources, or modules

## File layout

```
sensing-platform-config/
├── SKILL.md                           # Core skill (rules, model, checklist)
└── references/
    ├── controls-reference.md          # Control catalog (~46 types)
    ├── events-reference.md            # Event actions and global keys
    ├── data-sources-reference.md      # Data source types and DataProvider grammar
    └── xml-patterns.md                # Copy-pasteable XML skeletons
```

## Updating

This copy is tracked in the repo. After editing, copy back to `~/.claude/skills/sensing-platform-config/` and restart Claude Code.
