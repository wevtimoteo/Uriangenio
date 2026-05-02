<img src="https://github.com/wevtimoteo/Uriangenio/raw/main/images/logo.png" align="right" width="260px"/>

# Uriangenio

[![GitHub release](https://img.shields.io/github/release/wevtimoteo/Uriangenio.svg)](https://github.com/wevtimoteo/Uriangenio/releases/)
[![.NET](https://github.com/wevtimoteo/Uriangenio/actions/workflows/dotnet.yml/badge.svg)](https://github.com/wevtimoteo/Uriangenio/actions/workflows/dotnet.yml)

Uriangenio is a fork of [Echoglossian](https://github.com/lokinmodar/Echoglossian), the realtime Final Fantasy XIV game text translator originally created and maintained by [lokinmodar](https://github.com/lokinmodar).

This fork exists to publish an independent Patch 7.5 / Dalamud API 15 build under a separate plugin identity while the upstream project remains the source of the original work.

## Credits

All original Echoglossian concept, architecture, plugin work, branding history, and the long-running project stewardship belong to [lokinmodar](https://github.com/lokinmodar). This fork keeps that lineage visible and should not be read as a replacement for the upstream project.

Additional thanks to the original Echoglossian contributors and references:

- annaclemens for XivCommon
- midorikami for AddonLifecycle
- goaats and the Dalamud/FFXIVQuickLauncher maintainers
- haplo for ChatTranslator plugin
- Eternita-S, Bluefissure, Soreepeong/Kizer, samulopez, and pbzweihander for their contributions
- Critical-Impact projects such as InventoryTools, AllaganMarket, CriticalCommonLib, LuminaSupplemental, DalaMock, and AllaganLib for practical Lumina/data-access patterns
- Era-FFXIV QuestShare.Plugin for quest progression and quest-sheet resolution patterns
- HaselDebug for addon inspection and probe patterns
- DelvUI and DelvCD for tooltip/hover UX patterns
- ChatBubbles for bubble-style addon handling references

## Installation

Add the custom plugin repository URL in Dalamud:

```text
https://github.com/wevtimoteo/Uriangenio/releases/latest/download/pluginmaster.json
```

In game:

1. Run `/xlsettings`.
2. Open the `Experimental` tab.
3. Add the URL above under `Custom Plugin Repositories`.
4. Save, then open `/xlplugins`.
5. Search for `Uriangenio` and install it.

Uriangenio uses `InternalName` `Uriangenio`, so it is separate from the official `Echoglossian` plugin entry.

## Chat Commands

`/uriangenio` opens the plugin configuration window.

Diagnostic commands are also available:

- `/uriangeniodbmanager`
- `/uriangenioaddonprobe`
- `/uriangenioquestprobe`

## Usage

Enable the desired translations and configure the available options through the configuration window.

## Development

Development notes are in [CONTRIBUTING.md](CONTRIBUTING.md).

## Upstream

For the original project, issues, history, and upstream development, see [lokinmodar/Echoglossian](https://github.com/lokinmodar/Echoglossian).

###### Final Fantasy XIV (c) 2010-2026 SQUARE ENIX CO., LTD. All Rights Reserved. This project is not affiliated with SQUARE ENIX CO., LTD.
