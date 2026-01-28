# DCS World LLM-Enabled Mission Design

A comprehensive documentation and tooling repository for programmatically generating DCS World missions using AI/LLM assistants (Claude, ChatGPT, etc.).

## Overview

DCS World missions are stored as `.miz` files—ZIP archives containing Lua table definitions. This repository provides detailed documentation of the `.miz` file format, enabling AI assistants to generate complete, valid mission files from natural language prompts.

**Key Features:**
- Complete `.miz` file format specification
- AI system rules for Claude Projects and ChatGPT Custom GPTs  
- Prompt templates for various mission types
- Reference documentation for units, weapons, and enumerators
- Demo mission with real-world examples

## Quick Start

### For AI Mission Generation

1. **Claude Projects:** Add the contents of [`AI_SYSTEM_RULES.md`](./docs/mission-building/AI_SYSTEM_RULES.md) to your Project Instructions
2. **ChatGPT Custom GPT:** Paste the system rules into your GPT's Instructions field
3. **Single Conversation:** Include the rules at the start of your chat

Then use prompts like:

```
Generate a DCS World mission with:
- Map: Caucasus
- Time: 10:00, clear weather
- Blue: 2x F-16C at Kobuleti, CAP mission, player slots
- Red: 4x MiG-29A spawning from the north after 10 minutes
```

### For Manual Mission Creation

See the [Prompt Guide](./docs/mission-building/PROMPT_GUIDE.md) for detailed templates and examples.

## Documentation

| Document | Description |
|----------|-------------|
| [**AI System Rules**](./docs/mission-building/AI_SYSTEM_RULES.md) | System instructions for AI assistants |
| [**Prompt Guide**](./docs/mission-building/PROMPT_GUIDE.md) | How to write effective mission prompts |
| [MIZ File Structure](./docs/mission-building/01-MIZ_FILE_STRUCTURE.md) | ZIP archive structure and required files |
| [Mission Lua Format](./docs/mission-building/02-MISSION_LUA_FORMAT.md) | Complete mission file schema |
| [Units and Groups](./docs/mission-building/03-UNITS_AND_GROUPS.md) | Aircraft, vehicles, ships, and static objects |
| [Tasks and Waypoints](./docs/mission-building/04-TASKS_AND_WAYPOINTS.md) | Route definitions and AI tasking |
| [Enumerators Reference](./docs/mission-building/05-ENUMERATORS.md) | Country codes, unit types, constants |
| [Scripting Engine](./docs/mission-building/06-SCRIPTING_ENGINE.md) | Lua scripting and triggers |
| [Examples](./docs/mission-building/07-EXAMPLES.md) | Complete mission examples |

## Repository Structure

```
├── docs/
│   └── mission-building/
│       ├── AI_SYSTEM_RULES.md      # AI/LLM system instructions
│       ├── PROMPT_GUIDE.md         # Mission prompt templates
│       ├── 01-MIZ_FILE_STRUCTURE.md
│       ├── 02-MISSION_LUA_FORMAT.md
│       ├── 03-UNITS_AND_GROUPS.md
│       ├── 04-TASKS_AND_WAYPOINTS.md
│       ├── 05-ENUMERATORS.md
│       ├── 06-SCRIPTING_ENGINE.md
│       └── 07-EXAMPLES.md
├── missions/
│   └── demo-mission/               # Example mission files
│       ├── mission                 # Main mission Lua table
│       ├── options                 # Mission options
│       ├── warehouses              # Airbase configurations
│       ├── theatre                 # Map name
│       └── l10n/DEFAULT/
│           ├── dictionary          # Localization strings
│           └── mapResource         # Map resources
└── README.md
```

## Supported Maps (Theatres)

| Theatre | Description |
|---------|-------------|
| `Caucasus` | Black Sea region (free map) |
| `Nevada` | NTTR - Nevada Test and Training Range |
| `PersianGulf` | Persian Gulf / Strait of Hormuz |
| `Syria` | Syria / Eastern Mediterranean |
| `MarianaIslands` | Pacific - Mariana Islands |
| `SouthAtlantic` | Falkland Islands region |
| `Sinai` | Sinai Peninsula |
| `Kola` | Kola Peninsula |
| `Afghanistan` | Afghanistan |
| `Normandy` | WWII Normandy |
| `TheChannel` | WWII English Channel |

## Creating a Mission File

A DCS `.miz` file is a ZIP archive containing these files:

```
mission.miz
├── mission           # Main mission definition (required)
├── options           # Mission options/settings (required)
├── theatre           # Map name string (required)
├── warehouses        # Airbase configurations (required)
└── l10n/DEFAULT/
    ├── dictionary    # Briefing text (required)
    └── mapResource   # Map resources (required)
```

### From AI-Generated Output

1. Have the AI generate each file as a separate code block
2. Save files with the correct names (no extensions for `mission`, `options`, `warehouses`, `theatre`)
3. Create the `l10n/DEFAULT/` folder structure
4. ZIP all files together
5. Rename `.zip` to `.miz`

### Programmatic Example (Python)

```python
import zipfile

def create_miz(output_path, mission_data, options_data, 
               theatre, warehouses_data, dictionary_data):
    with zipfile.ZipFile(output_path, 'w', zipfile.ZIP_DEFLATED) as miz:
        miz.writestr('mission', mission_data)
        miz.writestr('options', options_data)
        miz.writestr('theatre', theatre)
        miz.writestr('warehouses', warehouses_data)
        miz.writestr('l10n/DEFAULT/dictionary', dictionary_data)
        miz.writestr('l10n/DEFAULT/mapResource', 'mapResource = {}\n')
```

## Key Concepts

### Coordinates
- DCS uses a Cartesian coordinate system (meters)
- `x` = East-West (negative = West)
- `y` = North-South (positive = North)
- Heading is in **radians** (0 = North, π/2 = East)
- Speed is in **m/s** (not knots)
- Altitude is in **meters** (not feet)

### Coalitions
- **Blue (2):** NATO/Western forces
- **Red (1):** OPFOR/Eastern forces
- **Neutral (0):** Non-combatant

### Unit Organization
- **Groups** contain one or more **Units**
- Each group/unit needs a unique `groupId`/`unitId`
- Each group/unit needs a unique `name`

### Common Unit Types

**Aircraft:**
```
F-16C_50, FA-18C_hornet, F-15C, F-15ESE, A-10C_2
AH-64D_BLK_II, UH-60L, AH-6J
Su-27, MiG-29A, MiG-29S, Su-25T, Mi-24P, Ka-50
```

**Ground Vehicles:**
```
M1A2, Leopard-2, T-72B3, T-80UD, T-90
M-2 Bradley, BTR-80, BMP-2, BMP-3
SA-11 Buk LN 9A310M1, Patriot ln, ZSU-23-4 Shilka
```

## Validation Checklist

Before loading a generated mission:

- [ ] All `groupId` values are unique
- [ ] All `unitId` values are unique  
- [ ] All group/unit names are unique
- [ ] Theatre name matches exactly (case-sensitive)
- [ ] Unit type strings match DCS database exactly
- [ ] Heading is in radians (0 to 2π)
- [ ] Speed is in m/s, altitude in meters
- [ ] Every group has at least one unit
- [ ] Every group has a route with at least one waypoint
- [ ] Aircraft have payload defined

## External Resources

- [Hoggit DCS World Wiki](https://wiki.hoggitworld.com/view/Hoggit_DCS_World_Wiki)
- [DCS Scripting Engine Documentation](https://wiki.hoggitworld.com/view/Simulator_Scripting_Engine_Documentation)
- [MIST - Mission Scripting Tools](https://wiki.hoggitworld.com/view/Mission_Scripting_Tools_Documentation)
- [MOOSE Framework](http://flightcontrol-master.github.io/MOOSE/)

## Contributing

Contributions are welcome! Areas where help is needed:

- Additional unit type strings and weapon CLSIDs
- Map-specific coordinate references
- More mission examples
- Validation tooling

## License

This documentation is provided for educational purposes. DCS World is a product of Eagle Dynamics.
