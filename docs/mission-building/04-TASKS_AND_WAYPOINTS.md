# Tasks and Waypoints

Routes define the path that groups follow, and tasks define what actions they perform at each waypoint.

## Route Structure

```lua
["route"] = {
    ["points"] = {
        [1] = { ... },  -- Waypoint 1 (starting point)
        [2] = { ... },  -- Waypoint 2
        -- ... more waypoints
    },
    ["spans"] = {},  -- Optional: for ground units
},
```

## Waypoint Structure

### Aircraft/Helicopter Waypoint

```lua
{
    -- Position
    ["x"] = -317688,
    ["y"] = 636897,
    ["alt"] = 2000,              -- Altitude in meters
    ["alt_type"] = "BARO",       -- "BARO" (MSL) or "RADIO" (AGL)
    
    -- Waypoint type
    ["type"] = "Turning Point",
    ["action"] = "Turning Point",
    ["form"] = "Turning Point",  -- Formation template
    
    -- Speed
    ["speed"] = 138.89,          -- m/s
    ["speed_locked"] = true,     -- Lock speed
    
    -- Timing
    ["ETA"] = 0,                 -- Estimated time of arrival
    ["ETA_locked"] = true,       -- Lock to TOT
    
    -- Tasks at this waypoint
    ["task"] = {
        ["id"] = "ComboTask",
        ["params"] = {
            ["tasks"] = { ... },
        },
    },
    
    -- Airbase references (takeoff/landing)
    ["airdromeId"] = 24,         -- Airport ID
    
    -- Optional
    ["formation_template"] = "",
    ["name"] = "WP1",
},
```

### Waypoint Types

| Type | Action | Description |
|------|--------|-------------|
| `TakeOff` | `From Runway` | Takeoff from runway |
| `TakeOffParking` | `From Parking Area` | Takeoff from parking (cold) |
| `TakeOffParkingHot` | `From Parking Area Hot` | Takeoff from parking (hot) |
| `TakeOffGround` | `From Ground Area` | Takeoff from ground (cold) |
| `TakeOffGroundHot` | `From Ground Area Hot` | Takeoff from ground (hot) |
| `Turning Point` | `Turning Point` | Standard waypoint |
| `Fly Over Point` | `Fly Over Point` | Must fly directly over |
| `Land` | `Landing` | Land at airbase |
| `LandReFuAr` | `Landing Re-Arm/Re-Fuel` | Land, rearm, refuel |

### Ground Vehicle Waypoint

```lua
{
    ["x"] = -286189,
    ["y"] = 678515,
    ["alt"] = 35,                -- Terrain altitude
    ["alt_type"] = "BARO",
    
    ["type"] = "Turning Point",
    ["action"] = "Off Road",     -- Movement type
    ["form"] = "Off Road",
    
    ["speed"] = 5.5556,          -- m/s (20 km/h)
    ["speed_locked"] = true,
    
    ["ETA"] = 0,
    ["ETA_locked"] = true,
    
    ["task"] = { ... },
    ["formation_template"] = "",
},
```

### Ground Movement Actions

| Action | Description |
|--------|-------------|
| `Off Road` | Move off-road directly to waypoint |
| `On Road` | Use roads to reach waypoint |
| `Rank` | Rank formation |
| `Cone` | Cone formation |
| `Diamond` | Diamond formation |
| `Vee` | Vee formation |
| `EchelonL` | Echelon left |
| `EchelonR` | Echelon right |

## Task Structure

Tasks are wrapped in `ComboTask` containers:

```lua
["task"] = {
    ["id"] = "ComboTask",
    ["params"] = {
        ["tasks"] = {
            [1] = {
                ["number"] = 1,
                ["auto"] = false,
                ["id"] = "Orbit",
                ["enabled"] = true,
                ["params"] = { ... },
            },
            [2] = {
                ["number"] = 2,
                ["id"] = "EngageTargets",
                -- ...
            },
        },
    },
},
```

## Common Tasks

### Orbit (Loiter)

```lua
{
    ["id"] = "Orbit",
    ["params"] = {
        ["altitude"] = 2000,
        ["pattern"] = "Circle",      -- "Circle" or "Race-Track"
        ["speed"] = 138.89,          -- m/s
        -- For Race-Track only:
        ["point"] = { ["x"] = -285000, ["y"] = 680000 },
    },
},
```

### Engage Targets

```lua
{
    ["id"] = "EngageTargets",
    ["params"] = {
        ["maxDist"] = 50000,          -- Engagement range (m)
        ["maxDistEnabled"] = true,
        ["targetTypes"] = {
            [1] = "Air",
        },
        ["noTargetTypes"] = {
            [1] = "Cruise missiles",
        },
        ["priority"] = 0,
    },
},
```

### Engage Targets In Zone

```lua
{
    ["id"] = "EngageTargetsInZone",
    ["params"] = {
        ["x"] = -285000,
        ["y"] = 680000,
        ["zoneRadius"] = 10000,       -- Zone radius (m)
        ["targetTypes"] = { [1] = "Air" },
        ["priority"] = 0,
    },
},
```

### Attack Group

```lua
{
    ["id"] = "AttackGroup",
    ["params"] = {
        ["groupId"] = 5,              -- Target group ID
        ["weaponType"] = 1073741822,  -- Weapon type bitmask
        ["expend"] = "Quarter",       -- Ammo expenditure
        ["altitudeEnabled"] = false,
        ["directionEnabled"] = false,
    },
},
```

### Bombing

```lua
{
    ["id"] = "Bombing",
    ["params"] = {
        ["x"] = -285000,
        ["y"] = 680000,
        ["altitude"] = 500,
        ["weaponType"] = 2147485694,
        ["expend"] = "All",
        ["attackQtyLimit"] = false,
        ["altitudeEnabled"] = false,
        ["groupAttack"] = false,
    },
},
```

### FAC (Forward Air Controller)

```lua
{
    ["id"] = "FAC",
    ["params"] = {},
},
```

### FAC Attack Group

```lua
{
    ["id"] = "FAC_AttackGroup",
    ["params"] = {
        ["groupId"] = 1,
        ["weaponType"] = 9663676414,
        ["designation"] = "Laser",    -- "No", "WP", "IR-Pointer", "Laser", "Auto"
        ["laserCode"] = 1688,
        ["datalink"] = true,
        ["frequency"] = 135000000,    -- Hz
        ["modulation"] = 0,
        ["callname"] = 1,             -- JTAC callsign index
        ["number"] = 1,
    },
},
```

### Refueling

```lua
{
    ["id"] = "Refueling",
    ["params"] = {},
},
```

### AWACS

```lua
{
    ["id"] = "AWACS",
    ["params"] = {},
},
```

### Tanker

```lua
{
    ["id"] = "Tanker",
    ["params"] = {},
},
```

### Fire At Point (Artillery)

```lua
{
    ["id"] = "FireAtPoint",
    ["params"] = {
        ["x"] = -285000,
        ["y"] = 680000,
        ["zoneRadius"] = 0,
        ["expendQty"] = 20,
        ["expendQtyEnabled"] = true,
        ["weaponType"] = 1073741822,
        ["alt_type"] = 1,
    },
},
```

### Hold Position

```lua
{
    ["id"] = "Hold",
    ["params"] = {},
},
```

## Commands (WrappedAction)

Commands are wrapped in `WrappedAction`:

```lua
{
    ["id"] = "WrappedAction",
    ["params"] = {
        ["action"] = {
            ["id"] = "SetFrequency",
            ["params"] = {
                ["frequency"] = 251000000,
                ["modulation"] = 0,
                ["power"] = 10,
            },
        },
    },
},
```

### Common Commands

#### EPLRS (Enhanced Position Location Reporting System)

```lua
{
    ["id"] = "EPLRS",
    ["params"] = {
        ["value"] = true,
        ["groupId"] = 1,  -- EPLRS group ID
    },
},
```

#### Set Frequency

```lua
{
    ["id"] = "SetFrequency",
    ["params"] = {
        ["frequency"] = 251000000,  -- Hz
        ["modulation"] = 0,         -- 0 = AM, 1 = FM
        ["power"] = 10,
    },
},
```

#### Activate Beacon (TACAN)

```lua
{
    ["id"] = "ActivateBeacon",
    ["params"] = {
        ["type"] = 4,               -- Beacon type (4 = TACAN)
        ["system"] = 3,             -- System (3 = TACAN)
        ["channel"] = 74,
        ["modeChannel"] = "X",      -- "X" or "Y"
        ["callsign"] = "TKR",
        ["bearing"] = true,
        ["frequency"] = 1160000000, -- Hz
    },
},
```

#### Set Invisible

```lua
{
    ["id"] = "SetInvisible",
    ["params"] = {
        ["value"] = true,
    },
},
```

#### Set Immortal

```lua
{
    ["id"] = "SetImmortal",
    ["params"] = {
        ["value"] = true,
    },
},
```

## Options

Options control AI behavior:

```lua
{
    ["id"] = "WrappedAction",
    ["params"] = {
        ["action"] = {
            ["id"] = "Option",
            ["params"] = {
                ["name"] = 0,       -- Option ID (0 = ROE)
                ["value"] = 2,      -- Option value
            },
        },
    },
},
```

### ROE (Rules of Engagement) - Air

| Value | Name | Description |
|-------|------|-------------|
| 0 | WEAPON_FREE | Fire at any enemy |
| 1 | OPEN_FIRE_WEAPON_FREE | Open fire, prioritize designated |
| 2 | OPEN_FIRE | Fire at designated only |
| 3 | RETURN_FIRE | Return fire only |
| 4 | WEAPON_HOLD | Hold fire |

### Reaction to Threat

| Value | Name | Description |
|-------|------|-------------|
| 0 | NO_REACTION | No evasive action |
| 1 | PASSIVE_DEFENCE | Use countermeasures only |
| 2 | EVADE_FIRE | Evade incoming fire |
| 3 | BYPASS_AND_ESCAPE | Evade and escape |
| 4 | ALLOW_ABORT_MISSION | May abort mission |

### Radar Using

| Value | Name |
|-------|------|
| 0 | NEVER |
| 1 | FOR_ATTACK_ONLY |
| 2 | FOR_SEARCH_IF_REQUIRED |
| 3 | FOR_CONTINUOUS_SEARCH |

## Complete Route Example

### Fighter CAP Mission

```lua
["route"] = {
    ["points"] = {
        [1] = {
            ["alt"] = 18,
            ["type"] = "TakeOffParking",
            ["action"] = "From Parking Area",
            ["alt_type"] = "BARO",
            ["speed"] = 138.89,
            ["speed_locked"] = true,
            ["x"] = -317688,
            ["y"] = 636897,
            ["airdromeId"] = 24,
            ["ETA"] = 0,
            ["ETA_locked"] = true,
            ["task"] = {
                ["id"] = "ComboTask",
                ["params"] = {
                    ["tasks"] = {},
                },
            },
        },
        [2] = {
            ["alt"] = 7000,
            ["type"] = "Turning Point",
            ["action"] = "Turning Point",
            ["alt_type"] = "BARO",
            ["speed"] = 220,
            ["speed_locked"] = true,
            ["x"] = -290000,
            ["y"] = 680000,
            ["ETA"] = 300,
            ["ETA_locked"] = false,
            ["task"] = {
                ["id"] = "ComboTask",
                ["params"] = {
                    ["tasks"] = {
                        [1] = {
                            ["number"] = 1,
                            ["auto"] = false,
                            ["id"] = "EngageTargets",
                            ["enabled"] = true,
                            ["params"] = {
                                ["maxDist"] = 50000,
                                ["targetTypes"] = { [1] = "Air" },
                                ["priority"] = 0,
                            },
                        },
                        [2] = {
                            ["number"] = 2,
                            ["auto"] = false,
                            ["id"] = "Orbit",
                            ["enabled"] = true,
                            ["params"] = {
                                ["altitude"] = 7000,
                                ["pattern"] = "Race-Track",
                                ["speed"] = 180,
                                ["point"] = {
                                    ["x"] = -285000,
                                    ["y"] = 680000,
                                },
                            },
                        },
                    },
                },
            },
        },
        [3] = {
            ["alt"] = 18,
            ["type"] = "Land",
            ["action"] = "Landing",
            ["alt_type"] = "BARO",
            ["speed"] = 138.89,
            ["x"] = -317688,
            ["y"] = 636897,
            ["airdromeId"] = 24,
            ["task"] = {
                ["id"] = "ComboTask",
                ["params"] = { ["tasks"] = {} },
            },
        },
    },
},
```

### Ground Patrol Route

```lua
["route"] = {
    ["points"] = {
        [1] = {
            ["alt"] = 35,
            ["type"] = "Turning Point",
            ["action"] = "On Road",
            ["alt_type"] = "BARO",
            ["speed"] = 8.33,  -- 30 km/h
            ["speed_locked"] = true,
            ["x"] = -286000,
            ["y"] = 678000,
            ["ETA"] = 0,
            ["ETA_locked"] = true,
            ["task"] = {
                ["id"] = "ComboTask",
                ["params"] = { ["tasks"] = {} },
            },
        },
        [2] = {
            ["alt"] = 40,
            ["type"] = "Turning Point",
            ["action"] = "On Road",
            ["alt_type"] = "BARO",
            ["speed"] = 8.33,
            ["x"] = -284000,
            ["y"] = 680000,
            ["task"] = {
                ["id"] = "ComboTask",
                ["params"] = { ["tasks"] = {} },
            },
        },
        [3] = {
            ["alt"] = 35,
            ["type"] = "Turning Point",
            ["action"] = "On Road",
            ["x"] = -286000,
            ["y"] = 678000,
            ["task"] = {
                ["id"] = "ComboTask",
                ["params"] = { ["tasks"] = {} },
            },
        },
    },
},
```
