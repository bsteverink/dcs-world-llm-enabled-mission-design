# DCS World Mission Building Documentation

This documentation provides comprehensive information for programmatically generating DCS World missions using the `.miz` file format.

## Overview

DCS World missions are stored as `.miz` files, which are ZIP archives containing Lua table files that define all aspects of a mission. This documentation is based on information from the [Hoggit DCS World Wiki](https://wiki.hoggitworld.com/view/Hoggit_DCS_World_Wiki) and analysis of actual mission files.

## Documentation Index

| Document | Description |
|----------|-------------|
| [**Prompt Guide**](./PROMPT_GUIDE.md) | **How to write prompts that generate working missions** |
| [**AI System Rules**](./AI_SYSTEM_RULES.md) | **Rules to import into Claude/ChatGPT for mission generation** |
| [MIZ File Structure](./01-MIZ_FILE_STRUCTURE.md) | The ZIP archive structure and required files |
| [Mission Lua Format](./02-MISSION_LUA_FORMAT.md) | Complete mission file structure and fields |
| [Units and Groups](./03-UNITS_AND_GROUPS.md) | How to define aircraft, vehicles, ships, and static objects |
| [Tasks and Waypoints](./04-TASKS_AND_WAYPOINTS.md) | Route definitions and AI tasking |
| [Enumerators Reference](./05-ENUMERATORS.md) | Country codes, coalition sides, unit types, etc. |
| [Scripting Engine](./06-SCRIPTING_ENGINE.md) | Lua scripting capabilities and triggers |
| [Examples](./07-EXAMPLES.md) | Complete mission examples |

## Quick Start

To create a basic DCS mission programmatically:

1. **Create the required Lua files:**
   - `mission` - Main mission definition
   - `options` - Mission options/difficulty settings
   - `theatre` - Map name (e.g., "Caucasus")
   - `warehouses` - Airport/warehouse configurations
   - `l10n/DEFAULT/dictionary` - Localization strings
   - `l10n/DEFAULT/mapResource` - Map resource references

2. **Package as ZIP:**
   - Combine all files into a ZIP archive
   - Rename the extension from `.zip` to `.miz`

3. **Load in DCS:**
   - Open the mission in DCS World Mission Editor to validate
   - Or load directly in single/multiplayer

## Supported Theatres (Maps)

| Theatre Name | Description |
|--------------|-------------|
| `Caucasus` | Black Sea region (free map) |
| `Nevada` | NTTR - Nevada Test and Training Range |
| `Normandy` | WWII Normandy |
| `PersianGulf` | Persian Gulf / Strait of Hormuz |
| `TheChannel` | English Channel (WWII) |
| `Syria` | Syria/Eastern Mediterranean |
| `MarianaIslands` | Pacific - Mariana Islands |
| `SouthAtlantic` | Falkland Islands region |
| `Sinai` | Sinai Peninsula |
| `Kola` | Kola Peninsula |
| `Afghanistan` | Afghanistan |

## Key Concepts

### Coalitions
DCS missions have three sides:
- **Blue** - NATO/Western forces (coalition.side = 2)
- **Red** - OPFOR/Eastern forces (coalition.side = 1)
- **Neutral** - Non-combatant (coalition.side = 0)

### Units Organization
- **Groups** contain one or more **Units**
- Aircraft/helicopters are in `plane` or `helicopter` categories
- Ground vehicles are in `vehicle` category
- Ships are in `ship` category
- Static objects are separate from units

### Coordinate System
DCS uses a Cartesian coordinate system:
- **x** - East-West position (negative = West)
- **y** - North-South position (positive = North)
- **alt** - Altitude in meters
- Coordinates are in meters, specific to each theatre

## External Resources

- [Hoggit DCS World Wiki](https://wiki.hoggitworld.com/view/Hoggit_DCS_World_Wiki)
- [DCS Scripting Engine Documentation](https://wiki.hoggitworld.com/view/Simulator_Scripting_Engine_Documentation)
- [MIST Documentation](https://wiki.hoggitworld.com/view/Mission_Scripting_Tools_Documentation)
- [MOOSE Framework](http://flightcontrol-master.github.io/MOOSE/)
- [Lua 5.2 Reference Manual](http://www.lua.org/manual/5.2/)
