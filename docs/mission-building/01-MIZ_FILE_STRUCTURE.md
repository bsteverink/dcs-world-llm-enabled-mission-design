# MIZ File Structure

The `.miz` file format is the container format for DCS World missions. It is essentially a ZIP archive containing Lua table definitions and optional resources.

## Archive Structure

```
mission.miz (ZIP archive)
├── mission                    # Main mission definition (required)
├── options                    # Mission options/settings (required)
├── theatre                    # Map/theatre name (required)
├── warehouses                 # Warehouse/airbase configs (required)
├── l10n/
│   └── DEFAULT/
│       ├── dictionary         # Localization strings (required)
│       └── mapResource        # Map resource references (required)
├── scripts/                   # Optional Lua scripts
│   └── *.lua
├── sounds/                    # Optional sound files
│   └── *.ogg, *.wav
├── images/                    # Optional briefing images
│   └── *.jpg, *.png
└── kneeboards/               # Optional kneeboard images
    └── *.jpg, *.png
```

## Required Files

### 1. `mission`

The main mission file containing all mission data as a Lua table.

```lua
mission = {
    ["date"] = { Year = 2024, Month = 6, Day = 15 },
    ["theatre"] = "Caucasus",
    ["coalition"] = { ... },
    ["weather"] = { ... },
    ["triggers"] = { ... },
    -- ... more fields
}
```

**See:** [Mission Lua Format](./02-MISSION_LUA_FORMAT.md)

### 2. `options`

Mission difficulty and gameplay options.

```lua
options = {
    ["difficulty"] = {
        ["fuel"] = false,
        ["weapons"] = false,
        ["labels"] = 0,
        ["map"] = true,
        -- ... more options
    },
    ["miscellaneous"] = { ... },
    ["graphics"] = { ... },
    -- ... more sections
}
```

### 3. `theatre`

A single line specifying the map name.

```lua
Caucasus
```

Valid values: `Caucasus`, `Nevada`, `Normandy`, `PersianGulf`, `TheChannel`, `Syria`, `MarianaIslands`, `SouthAtlantic`, `Sinai`, `Kola`, `Afghanistan`

### 4. `warehouses`

Airport and warehouse configuration.

```lua
warehouses = {
    ["airports"] = {
        [12] = {  -- Airport ID
            ["coalition"] = "NEUTRAL",
            ["unlimitedMunitions"] = true,
            ["unlimitedFuel"] = true,
            ["unlimitedAircrafts"] = true,
            -- ... more settings
        },
    },
    ["warehouses"] = {},
}
```

### 5. `l10n/DEFAULT/dictionary`

Localization strings for briefing text.

```lua
dictionary = {
    ["DictKey_descriptionText_1"] = "Mission briefing text here",
    ["DictKey_descriptionBlueTask_3"] = "Blue team objectives",
    ["DictKey_descriptionRedTask_2"] = "Red team objectives",
    ["DictKey_descriptionNeutralsTask_4"] = "Neutral objectives",
    ["DictKey_sortie_5"] = "Mission sortie name",
}
```

### 6. `l10n/DEFAULT/mapResource`

Map resource references (usually empty for basic missions).

```lua
mapResource = {}
```

## Optional Resources

### Scripts
Lua script files that can be loaded via triggers:
- Place in `scripts/` directory
- Reference using `DO SCRIPT FILE` trigger action
- File is embedded in the .miz archive

### Sounds
Audio files for radio transmissions or effects:
- Supported formats: `.ogg`, `.wav`
- Place in `sounds/` directory
- Reference in triggers via `trigger.action.outSound()`

### Briefing Images
Images displayed in mission briefing:
- Supported formats: `.jpg`, `.png`
- Reference in mission using `pictureFileNameB`, `pictureFileNameR`, etc.

### Kneeboard Images
Custom kneeboard pages:
- Place in `kneeboards/` directory
- Format: `AIRCRAFT_TYPE/PAGE_##.jpg`

## Creating a MIZ File Programmatically

### Python Example

```python
import zipfile
import os

def create_miz(output_path, mission_data, options_data, theatre, 
               warehouses_data, dictionary_data):
    """
    Create a DCS .miz mission file.
    
    Args:
        output_path: Path for the output .miz file
        mission_data: Lua string for mission file
        options_data: Lua string for options file
        theatre: Theatre name string
        warehouses_data: Lua string for warehouses file
        dictionary_data: Lua string for dictionary file
    """
    with zipfile.ZipFile(output_path, 'w', zipfile.ZIP_DEFLATED) as miz:
        # Write required files
        miz.writestr('mission', mission_data)
        miz.writestr('options', options_data)
        miz.writestr('theatre', theatre)
        miz.writestr('warehouses', warehouses_data)
        
        # Write localization files
        miz.writestr('l10n/DEFAULT/dictionary', dictionary_data)
        miz.writestr('l10n/DEFAULT/mapResource', 'mapResource = {}\n')
    
    print(f"Created mission: {output_path}")
```

### Node.js Example

```javascript
const JSZip = require('jszip');
const fs = require('fs');

async function createMiz(outputPath, missionData, optionsData, theatre, 
                         warehousesData, dictionaryData) {
    const zip = new JSZip();
    
    // Add required files
    zip.file('mission', missionData);
    zip.file('options', optionsData);
    zip.file('theatre', theatre);
    zip.file('warehouses', warehousesData);
    
    // Add localization files
    zip.file('l10n/DEFAULT/dictionary', dictionaryData);
    zip.file('l10n/DEFAULT/mapResource', 'mapResource = {}\n');
    
    // Generate and save
    const content = await zip.generateAsync({ type: 'nodebuffer' });
    fs.writeFileSync(outputPath, content);
    
    console.log(`Created mission: ${outputPath}`);
}
```

## File Encoding

- All Lua files should be UTF-8 encoded
- Line endings can be LF or CRLF (DCS accepts both)
- No BOM (Byte Order Mark) should be present

## Validation

To validate a mission file:

1. **Quick Check:** Open in DCS Mission Editor
2. **Structure Check:** Extract ZIP and verify all required files exist
3. **Lua Syntax:** Parse Lua files to check for syntax errors
4. **Schema Validation:** Verify required fields are present

## Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| Mission won't load | Invalid Lua syntax | Check for missing commas, brackets |
| Units don't appear | Invalid unit type | Verify unit type strings match DCS database |
| Wrong map loads | Theatre mismatch | Ensure `theatre` file matches `mission.theatre` |
| Missing aircraft | Module not owned | Check `requiredModules` list |
| Spawn failures | Invalid coordinates | Verify x/y are valid for the map |
