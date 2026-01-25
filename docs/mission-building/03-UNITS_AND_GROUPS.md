# Units and Groups

Units in DCS missions are organized into groups. Each group can contain one or more units of the same general category (aircraft, vehicles, ships, etc.).

## Group Categories

| Category | Group.Category | Description |
|----------|----------------|-------------|
| Airplane | 0 | Fixed-wing aircraft |
| Helicopter | 1 | Rotorcraft |
| Ground | 2 | Vehicles, infantry, fortifications |
| Ship | 3 | Naval vessels |
| Train | 4 | Railway vehicles |

## Country Structure

Groups are organized by country within coalitions:

```lua
["country"] = {
    [1] = {
        ["id"] = 2,          -- Country ID (USA = 2)
        ["name"] = "USA",
        ["plane"] = {
            ["group"] = { ... }
        },
        ["helicopter"] = {
            ["group"] = { ... }
        },
        ["vehicle"] = {
            ["group"] = { ... }
        },
        ["ship"] = {
            ["group"] = { ... }
        },
        ["static"] = {
            ["group"] = { ... }
        },
    },
}
```

## Common Group Properties

All group types share these properties:

```lua
{
    -- Required
    ["name"] = "Group-1",           -- Unique group name
    ["groupId"] = 1,                -- Unique numeric ID
    ["task"] = "CAP",               -- Master task (aircraft) or "Ground Nothing" (ground)
    ["x"] = -285000,                -- Initial X position
    ["y"] = 678000,                 -- Initial Y position
    ["units"] = { ... },            -- Array of units
    
    -- Optional
    ["start_time"] = 0,             -- Spawn delay in seconds
    ["hidden"] = false,             -- Hide on F10 map
    ["route"] = { ["points"] = {} },-- Waypoints
    ["tasks"] = {},                 -- Additional tasks
    
    -- Category-specific
    ["visible"] = false,            -- Ground/ships: visible before start
    ["uncontrollable"] = false,     -- Ground/ships: Game Master only
    ["lateActivation"] = false,     -- Spawn via trigger
}
```

## Aircraft Group (Fixed-Wing)

```lua
{
    ["name"] = "Fighter-1",
    ["groupId"] = 1,
    ["task"] = "CAP",               -- Master task
    ["uncontrolled"] = false,       -- Engine off on ground
    ["communication"] = true,       -- Radio communication enabled
    ["frequency"] = 251,            -- MHz
    ["modulation"] = 0,             -- 0 = AM, 1 = FM
    ["radioSet"] = false,
    ["hidden"] = false,
    ["x"] = -317688,
    ["y"] = 636897,
    ["start_time"] = 0,
    ["route"] = { ... },
    ["units"] = {
        [1] = { ... },  -- Unit definitions
    },
}
```

### Aircraft Master Tasks

| Task | Description |
|------|-------------|
| `CAP` | Combat Air Patrol |
| `CAS` | Close Air Support |
| `SEAD` | Suppression of Enemy Air Defenses |
| `Intercept` | Interceptor |
| `Ground Attack` | Ground attack |
| `Runway Attack` | Attack runways |
| `Antiship Strike` | Anti-ship |
| `AWACS` | Airborne Warning and Control |
| `Refueling` | Tanker |
| `Reconnaissance` | Reconnaissance |
| `Fighter Sweep` | Fighter sweep |
| `Escort` | Escort mission |
| `Transport` | Transport |
| `AFAC` | Airborne Forward Air Controller |
| `Pinpoint Strike` | Precision strike |
| `Nothing` | No assigned task |

## Aircraft Unit Definition

```lua
{
    -- Required
    ["name"] = "Fighter-1-1",       -- Unique unit name
    ["unitId"] = 1,                 -- Unique numeric ID
    ["type"] = "F-16C_50",          -- Aircraft type string
    ["x"] = -317688,
    ["y"] = 636897,
    ["alt"] = 18,                   -- Altitude in meters
    ["alt_type"] = "BARO",          -- "BARO" (MSL) or "RADIO" (AGL)
    ["speed"] = 138.89,             -- m/s
    ["heading"] = 1.57,             -- Radians
    ["skill"] = "High",             -- AI skill level
    ["payload"] = { ... },          -- Weapons/fuel loadout
    ["callsign"] = { ... },         -- Callsign definition
    
    -- Optional
    ["psi"] = 0,                    -- Yaw angle
    ["onboard_num"] = "010",        -- Tail number
    ["livery_id"] = "default",      -- Skin/livery
    ["parking"] = "15",             -- Parking spot index
    ["parking_id"] = "30",          -- Parking spot display ID
    ["AddPropAircraft"] = { ... },  -- Additional properties
    ["Radio"] = { ... },            -- Radio presets
    ["datalinks"] = { ... },        -- Datalink configuration
    ["hardpoint_racks"] = true,     -- Show pylons
}
```

### Skill Levels

| Skill | Description |
|-------|-------------|
| `Average` | Basic AI |
| `Good` | Competent AI |
| `High` | Skilled AI |
| `Excellent` | Expert AI |
| `Random` | Random skill |
| `Player` | Single-player controllable |
| `Client` | Multiplayer slot |

### Payload Structure

```lua
["payload"] = {
    ["pylons"] = {
        [1] = {
            ["CLSID"] = "{AIM-120C}",  -- Weapon class ID
        },
        [2] = {
            ["CLSID"] = "{LAU-131 - 7 AGR-20 M282}",
            ["settings"] = {
                ["laser_code"] = 1688,
            },
        },
    },
    ["fuel"] = 3249,      -- Internal fuel (kg)
    ["flare"] = 60,       -- Flare count
    ["chaff"] = 60,       -- Chaff count
    ["gun"] = 100,        -- Gun ammo percentage
    ["ammo_type"] = 1,    -- Ammo type index
},
```

### Callsign Structure

**NATO Style:**
```lua
["callsign"] = {
    [1] = 1,              -- Callsign index (1=Enfield, 2=Springfield, etc.)
    [2] = 1,              -- Flight number
    [3] = 1,              -- Position in flight
    ["name"] = "Enfield11",
},
```

**Russian Style:**
```lua
["callsign"] = 123,       -- Numeric callsign
```

### Airfield Spawn

For parking spawns:
```lua
["parking"] = "15",           -- Term_Index from getParking
["parking_id"] = "30",        -- Display ID
```

For takeoff waypoints, include `airdromeId` in route point.

## Helicopter Group

Similar to aircraft with additional properties:

```lua
{
    ["name"] = "Helo-1",
    ["task"] = "CAS",
    ["ropeLength"] = 15,  -- Sling load rope length
    -- ... other aircraft properties
}
```

### Helicopter Unit

```lua
{
    ["type"] = "AH-64D_BLK_II",
    ["ropeLength"] = 15,
    -- ... other aircraft unit properties
}
```

## Ground Vehicle Group

```lua
{
    ["name"] = "Armor-1",
    ["groupId"] = 1,
    ["task"] = "Ground Nothing",
    ["visible"] = false,
    ["uncontrollable"] = false,
    ["hidden"] = false,
    ["x"] = -286189,
    ["y"] = 678515,
    ["start_time"] = 0,
    ["taskSelected"] = true,
    ["manualHeading"] = false,  -- Respect unit heading vs auto-orient to route
    ["route"] = { ... },
    ["units"] = { ... },
}
```

### Ground Vehicle Unit

```lua
{
    ["name"] = "Armor-1-1",
    ["unitId"] = 1,
    ["type"] = "M1A2",            -- Vehicle type
    ["x"] = -286189,
    ["y"] = 678515,
    ["heading"] = 0,              -- Radians
    ["skill"] = "Average",
    ["playerCanDrive"] = true,    -- Combined Arms controllable
    ["coldAtStart"] = false,      -- Engine cold (FLIR signature)
    ["transportable"] = {
        ["randomTransportable"] = false,
    },
}
```

### Ground Vehicle Types (Examples)

| Type String | Description |
|-------------|-------------|
| `M1A2` | M1A2 Abrams MBT |
| `T-80UD` | T-80UD MBT |
| `BTR-80` | BTR-80 APC |
| `M-109` | M-109 SP Artillery |
| `SA-11 Buk SR 9S18M1` | SA-11 Buk search radar |
| `SA-11 Buk LN 9A310M1` | SA-11 Buk launcher |
| `Soldier M4` | US Infantry with M4 |
| `2B11 mortar` | Mortar |

### Ground Tasks

| Task | Description |
|------|-------------|
| `Ground Nothing` | No task |
| `Ground Attack` | Attack ground targets |

## Ship Group

```lua
{
    ["name"] = "Navy-1",
    ["groupId"] = 1,
    ["task"] = "Ground Nothing",
    ["visible"] = false,
    ["uncontrollable"] = false,
    ["x"] = -10000,
    ["y"] = 690000,
    ["route"] = { ... },
    ["units"] = { ... },
}
```

### Ship Unit

```lua
{
    ["name"] = "Navy-1-1",
    ["unitId"] = 1,
    ["type"] = "CVN_74",          -- Aircraft carrier
    ["x"] = -10000,
    ["y"] = 690000,
    ["heading"] = 0,
    ["skill"] = "Average",
}
```

### Ship Types (Examples)

| Type String | Description |
|-------------|-------------|
| `CVN_74` | USS John C. Stennis |
| `CVN_71` | USS Theodore Roosevelt |
| `LHA_Tarawa` | LHA Tarawa |
| `CG_Ticonderoga` | Ticonderoga-class cruiser |
| `FFG-7CL` | Oliver Hazard Perry frigate |
| `KUZNECOW` | Admiral Kuznetsov |

## Static Objects

Static objects are non-moving objects like buildings, cargo, and parked aircraft.

```lua
["static"] = {
    ["group"] = {
        [1] = {
            ["name"] = "Static-1",
            ["groupId"] = 100,
            ["x"] = -285000,
            ["y"] = 678000,
            ["heading"] = 0,
            ["dead"] = false,
            ["units"] = {
                [1] = {
                    ["name"] = "Static-1-1",
                    ["unitId"] = 100,
                    ["type"] = "Cafe",
                    ["shape_name"] = "stolovaya",
                    ["category"] = "Fortifications",
                    ["x"] = -285000,
                    ["y"] = 678000,
                    ["heading"] = 0,
                    ["rate"] = 100,  -- Score value
                },
            },
        },
    },
},
```

### Static Object Categories

| Category | Description |
|----------|-------------|
| `Fortifications` | Buildings, bunkers |
| `Cargos` | Cargo containers (can be sling-loaded) |
| `Heliports` | FARP |
| `Warehouses` | Warehouse structures |
| `Ground Units` | Static vehicle models |
| `Air Defence` | Static air defense |
| `ShipWrecks` | Ship wrecks |

### Cargo Objects

```lua
{
    ["type"] = "ammo_cargo",
    ["category"] = "Cargos",
    ["mass"] = 1000,      -- Weight in kg
    ["canCargo"] = true,  -- Can be lifted
}
```

### Static Aircraft

```lua
{
    ["type"] = "F-16C_50",
    ["category"] = "Planes",
    ["livery_id"] = "default",
}
```

## Generating Unique IDs

When creating missions programmatically, ensure unique IDs:

```python
class MissionBuilder:
    def __init__(self):
        self.group_id_counter = 1
        self.unit_id_counter = 1
    
    def next_group_id(self):
        gid = self.group_id_counter
        self.group_id_counter += 1
        return gid
    
    def next_unit_id(self):
        uid = self.unit_id_counter
        self.unit_id_counter += 1
        return uid
```

## Coordinate Reference

Different maps have different coordinate ranges. Example for Caucasus:

| Location | X (approx) | Y (approx) |
|----------|------------|------------|
| Batumi Airport | -355,700 | 618,000 |
| Tbilisi Airport | -314,000 | 895,000 |
| Anapa Airport | -5,400 | 243,000 |
| Kobuleti Airport | -317,700 | 636,900 |

**Note:** X values are typically negative (west), Y values are typically positive (north) for the Caucasus map.
