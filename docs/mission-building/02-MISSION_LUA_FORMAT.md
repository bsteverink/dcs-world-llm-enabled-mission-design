# Mission Lua Format

The `mission` file is the core of a DCS mission, containing all units, weather, triggers, and mission parameters.

## Top-Level Structure

```lua
mission = {
    -- Mission metadata
    ["date"] = { ... },
    ["start_time"] = 28800,  -- Seconds from midnight (8:00 AM)
    ["theatre"] = "Caucasus",
    ["sortie"] = "DictKey_sortie_5",
    ["version"] = 23,
    ["currentKey"] = 100,
    ["maxDictId"] = 10,
    
    -- Coalition definitions
    ["coalitions"] = { ... },
    ["coalition"] = { ... },
    
    -- Environment
    ["weather"] = { ... },
    
    -- Mission logic
    ["trig"] = { ... },
    ["triggers"] = { ... },
    ["trigrules"] = {},
    
    -- Results/Goals
    ["result"] = { ... },
    ["goals"] = {},
    
    -- Map display
    ["map"] = { ... },
    
    -- Briefing content (DictKey references)
    ["descriptionText"] = "DictKey_descriptionText_1",
    ["descriptionBlueTask"] = "DictKey_descriptionBlueTask_3",
    ["descriptionRedTask"] = "DictKey_descriptionRedTask_2",
    ["descriptionNeutralsTask"] = "DictKey_descriptionNeutralsTask_4",
    
    -- Briefing images
    ["pictureFileNameB"] = {},
    ["pictureFileNameR"] = {},
    ["pictureFileNameN"] = {},
    ["pictureFileNameServer"] = {},
    
    -- Other settings
    ["groundControl"] = { ... },
    ["requiredModules"] = { ... },
    ["failures"] = {},
    ["forcedOptions"] = {},
}
```

## Date and Time

```lua
["date"] = {
    ["Year"] = 2024,
    ["Month"] = 6,   -- 1-12
    ["Day"] = 15,    -- 1-31
},
["start_time"] = 28800,  -- Seconds from midnight (00:00:00)
```

**Time Conversion:**
- 08:00 = 28800 seconds
- 12:00 = 43200 seconds
- 18:00 = 64800 seconds

Formula: `hours * 3600 + minutes * 60 + seconds`

## Coalition Country Assignment

Defines which countries belong to each coalition:

```lua
["coalitions"] = {
    ["blue"] = {
        [1] = 2,   -- USA (country.id.USA = 2)
        [2] = 4,   -- UK
        [3] = 5,   -- France
        -- ... more country IDs
    },
    ["red"] = {
        [1] = 0,   -- Russia
        [2] = 34,  -- Iran
        -- ... more country IDs
    },
    ["neutrals"] = {
        [1] = 22,  -- Switzerland
        -- ... more country IDs
    },
},
```

## Coalition Data Structure

Contains all units and groups for each side:

```lua
["coalition"] = {
    ["blue"] = {
        ["bullseye"] = {
            ["x"] = -291014,
            ["y"] = 617414,
        },
        ["nav_points"] = {},
        ["name"] = "blue",
        ["country"] = {
            [1] = {
                ["id"] = 2,  -- USA
                ["name"] = "USA",
                ["plane"] = { ["group"] = { ... } },
                ["helicopter"] = { ["group"] = { ... } },
                ["vehicle"] = { ["group"] = { ... } },
                ["ship"] = { ["group"] = { ... } },
                ["static"] = { ["group"] = { ... } },
            },
            -- ... more countries
        },
    },
    ["red"] = { ... },
    ["neutrals"] = { ... },
},
```

## Weather Configuration

```lua
["weather"] = {
    ["atmosphere_type"] = 0,  -- 0 = static, 1 = dynamic
    ["type_weather"] = 0,
    ["modifiedTime"] = false,
    ["name"] = "Clear Sky",
    
    -- Temperature
    ["season"] = {
        ["temperature"] = 20,  -- Celsius at sea level
    },
    
    -- Pressure
    ["qnh"] = 760,  -- mmHg (standard: 760)
    
    -- Wind at different altitudes
    ["wind"] = {
        ["atGround"] = {
            ["speed"] = 0,    -- m/s
            ["dir"] = 0,      -- degrees (direction wind comes FROM)
        },
        ["at2000"] = {
            ["speed"] = 0,
            ["dir"] = 0,
        },
        ["at8000"] = {
            ["speed"] = 0,
            ["dir"] = 0,
        },
    },
    
    -- Visibility
    ["visibility"] = {
        ["distance"] = 80000,  -- meters (max: 80000)
    },
    
    -- Clouds
    ["clouds"] = {
        ["preset"] = "Preset2",  -- Cloud preset name or "nil"
        ["base"] = 2500,         -- Cloud base in meters
        ["density"] = 0,         -- 0-10
        ["thickness"] = 200,     -- meters
        ["iprecptns"] = 0,       -- 0=none, 1=rain, 2=thunderstorm
    },
    
    -- Fog
    ["enable_fog"] = false,
    ["fog"] = {
        ["visibility"] = 0,   -- meters
        ["thickness"] = 0,    -- meters
    },
    
    -- Dust (desert maps)
    ["enable_dust"] = false,
    ["dust_density"] = 0,
    
    -- Ground turbulence
    ["groundTurbulence"] = 0,  -- 0-10
    
    -- Cyclones (dynamic weather)
    ["cyclones"] = {},
    
    -- Halo effects
    ["halo"] = {
        ["preset"] = "auto",
    },
},
```

### Cloud Presets

| Preset | Description |
|--------|-------------|
| `Preset1` | Few clouds |
| `Preset2` | Light scattered |
| `Preset3` | Scattered clouds |
| `Preset4` | Broken clouds |
| `Preset5` | Overcast thin |
| `Preset6` | Overcast |
| `Preset7` | Overcast thick |
| `RaijinPreset1-7` | Rain presets |

## Ground Control (Combined Arms)

```lua
["groundControl"] = {
    ["isPilotControlVehicles"] = false,
    ["passwords"] = {
        ["artillery_commander"] = {},
        ["instructor"] = {},
        ["observer"] = {},
        ["forward_observer"] = {},
    },
    ["roles"] = {
        ["artillery_commander"] = {
            ["red"] = 0,
            ["blue"] = 0,
            ["neutrals"] = 0,
        },
        ["instructor"] = { ... },
        ["observer"] = { ... },
        ["forward_observer"] = { ... },
    },
},
```

## Required Modules

Specifies DLC/modules required to play the mission:

```lua
["requiredModules"] = {
    ["F-16C"] = "F-16C",
    ["FA-18C"] = "FA-18C_hornet",
    ["AH-64D"] = "AH-64D_BLK_II",
},
```

## Triggers Structure

The `trig` table contains trigger logic:

```lua
["trig"] = {
    ["actions"] = {
        [1] = "a]do_script(\"trigger.action.outText(\\\"Hello World\\\", 10)\")",
    },
    ["events"] = {},
    ["custom"] = {},
    ["func"] = {
        [1] = "if ... then ... end",
    },
    ["flag"] = {
        [1] = true,  -- Flag starting values
    },
    ["conditions"] = {
        [1] = "return(c_time_after(5))",
    },
    ["customStartup"] = {},
    ["funcStartup"] = {},
},
```

## Trigger Zones

```lua
["triggers"] = {
    ["zones"] = {
        [1] = {
            ["name"] = "Zone1",
            ["x"] = -285000,
            ["y"] = 678000,
            ["radius"] = 1000,
            ["color"] = {1, 0, 0, 0.15},  -- RGBA
            ["type"] = 0,  -- 0 = circle, 2 = quad
            ["hidden"] = false,
        },
        -- Quad zone example
        [2] = {
            ["name"] = "QuadZone",
            ["type"] = 2,
            ["x"] = -285000,
            ["y"] = 678000,
            ["verticies"] = {
                [1] = {["x"] = -285000, ["y"] = 678000},
                [2] = {["x"] = -284000, ["y"] = 678000},
                [3] = {["x"] = -284000, ["y"] = 679000},
                [4] = {["x"] = -285000, ["y"] = 679000},
            },
        },
    },
},
```

## Map Display Settings

```lua
["map"] = {
    ["centerX"] = -285000,  -- Map center X coordinate
    ["centerY"] = 680000,   -- Map center Y coordinate
    ["zoom"] = 100000,      -- Zoom level
},
```

## Mission Results

```lua
["result"] = {
    ["total"] = 0,
    ["offline"] = {
        ["conditions"] = {},
        ["actions"] = {},
        ["func"] = {},
    },
    ["blue"] = {
        ["conditions"] = {},
        ["actions"] = {},
        ["func"] = {},
    },
    ["red"] = {
        ["conditions"] = {},
        ["actions"] = {},
        ["func"] = {},
    },
},
["goals"] = {},
```

## Forced Options

Override player options:

```lua
["forcedOptions"] = {
    ["fuel"] = true,       -- Force realistic fuel
    ["weapons"] = true,    -- Force realistic weapons
    ["labels"] = false,    -- Disable labels
    ["externalViews"] = false,
    ["RBDAI"] = false,     -- Disable RB DAI
},
```

## Complete Minimal Mission Example

```lua
mission = {
    ["date"] = {
        ["Year"] = 2024,
        ["Day"] = 15,
        ["Month"] = 6,
    },
    ["start_time"] = 28800,
    ["theatre"] = "Caucasus",
    ["version"] = 23,
    ["currentKey"] = 100,
    ["maxDictId"] = 5,
    ["sortie"] = "DictKey_sortie_5",
    ["descriptionText"] = "DictKey_descriptionText_1",
    ["descriptionBlueTask"] = "DictKey_descriptionBlueTask_3",
    ["descriptionRedTask"] = "DictKey_descriptionRedTask_2",
    ["descriptionNeutralsTask"] = "DictKey_descriptionNeutralsTask_4",
    ["pictureFileNameB"] = {},
    ["pictureFileNameR"] = {},
    ["pictureFileNameN"] = {},
    ["pictureFileNameServer"] = {},
    ["groundControl"] = {
        ["isPilotControlVehicles"] = false,
        ["passwords"] = {
            ["artillery_commander"] = {},
            ["instructor"] = {},
            ["observer"] = {},
            ["forward_observer"] = {},
        },
        ["roles"] = {
            ["artillery_commander"] = { ["neutrals"] = 0, ["blue"] = 0, ["red"] = 0 },
            ["instructor"] = { ["neutrals"] = 0, ["blue"] = 0, ["red"] = 0 },
            ["observer"] = { ["neutrals"] = 0, ["blue"] = 0, ["red"] = 0 },
            ["forward_observer"] = { ["neutrals"] = 0, ["blue"] = 0, ["red"] = 0 },
        },
    },
    ["requiredModules"] = {},
    ["weather"] = {
        ["atmosphere_type"] = 0,
        ["type_weather"] = 0,
        ["name"] = "Clear",
        ["modifiedTime"] = false,
        ["season"] = { ["temperature"] = 20 },
        ["qnh"] = 760,
        ["groundTurbulence"] = 0,
        ["wind"] = {
            ["atGround"] = { ["speed"] = 0, ["dir"] = 0 },
            ["at2000"] = { ["speed"] = 0, ["dir"] = 0 },
            ["at8000"] = { ["speed"] = 0, ["dir"] = 0 },
        },
        ["visibility"] = { ["distance"] = 80000 },
        ["clouds"] = {
            ["preset"] = "Preset2",
            ["base"] = 2500,
            ["density"] = 0,
            ["thickness"] = 200,
            ["iprecptns"] = 0,
        },
        ["enable_fog"] = false,
        ["fog"] = { ["visibility"] = 0, ["thickness"] = 0 },
        ["enable_dust"] = false,
        ["dust_density"] = 0,
        ["cyclones"] = {},
        ["halo"] = { ["preset"] = "auto" },
    },
    ["coalitions"] = {
        ["blue"] = { [1] = 2 },  -- USA
        ["red"] = { [1] = 0 },   -- Russia
        ["neutrals"] = {},
    },
    ["coalition"] = {
        ["blue"] = {
            ["bullseye"] = { ["x"] = -291014, ["y"] = 617414 },
            ["nav_points"] = {},
            ["name"] = "blue",
            ["country"] = {},
        },
        ["red"] = {
            ["bullseye"] = { ["x"] = 11557, ["y"] = 371700 },
            ["nav_points"] = {},
            ["name"] = "red",
            ["country"] = {},
        },
        ["neutrals"] = {
            ["bullseye"] = { ["x"] = 0, ["y"] = 0 },
            ["nav_points"] = {},
            ["name"] = "neutrals",
            ["country"] = {},
        },
    },
    ["trig"] = {
        ["actions"] = {},
        ["events"] = {},
        ["custom"] = {},
        ["func"] = {},
        ["flag"] = {},
        ["conditions"] = {},
        ["customStartup"] = {},
        ["funcStartup"] = {},
    },
    ["triggers"] = { ["zones"] = {} },
    ["trigrules"] = {},
    ["result"] = {
        ["total"] = 0,
        ["offline"] = { ["conditions"] = {}, ["actions"] = {}, ["func"] = {} },
        ["blue"] = { ["conditions"] = {}, ["actions"] = {}, ["func"] = {} },
        ["red"] = { ["conditions"] = {}, ["actions"] = {}, ["func"] = {} },
    },
    ["goals"] = {},
    ["map"] = {
        ["centerX"] = -285000,
        ["centerY"] = 680000,
        ["zoom"] = 100000,
    },
    ["failures"] = {},
    ["forcedOptions"] = {},
}
```
