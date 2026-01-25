# Enumerators Reference

This document lists all constant values used in DCS mission files.

## Country IDs

Countries are identified by numeric IDs. The coalition (red/blue/neutral) is assigned in the mission.

| ID | Country Name | Constant |
|----|--------------|----------|
| 0 | Russia | `RUSSIA` |
| 1 | Ukraine | `UKRAINE` |
| 2 | USA | `USA` |
| 3 | Turkey | `TURKEY` |
| 4 | UK | `UK` |
| 5 | France | `FRANCE` |
| 6 | Germany | `GERMANY` |
| 7 | Aggressors | `AGGRESSORS` |
| 8 | Canada | `CANADA` |
| 9 | Spain | `SPAIN` |
| 10 | The Netherlands | `THE_NETHERLANDS` |
| 11 | Belgium | `BELGIUM` |
| 12 | Norway | `NORWAY` |
| 13 | Denmark | `DENMARK` |
| 15 | Israel | `ISRAEL` |
| 16 | Georgia | `GEORGIA` |
| 17 | Insurgents | `INSURGENTS` |
| 18 | Abkhazia | `ABKHAZIA` |
| 19 | South Ossetia | `SOUTH_OSETIA` |
| 20 | Italy | `ITALY` |
| 21 | Australia | `AUSTRALIA` |
| 22 | Switzerland | `SWITZERLAND` |
| 23 | Austria | `AUSTRIA` |
| 24 | Belarus | `BELARUS` |
| 25 | Bulgaria | `BULGARIA` |
| 26 | Czech Republic | `CHEZH_REPUBLIC` |
| 27 | China | `CHINA` |
| 28 | Croatia | `CROATIA` |
| 29 | Egypt | `EGYPT` |
| 30 | Finland | `FINLAND` |
| 31 | Greece | `GREECE` |
| 32 | Hungary | `HUNGARY` |
| 33 | India | `INDIA` |
| 34 | Iran | `IRAN` |
| 35 | Iraq | `IRAQ` |
| 36 | Japan | `JAPAN` |
| 37 | Kazakhstan | `KAZAKHSTAN` |
| 38 | North Korea | `NORTH_KOREA` |
| 39 | Pakistan | `PAKISTAN` |
| 40 | Poland | `POLAND` |
| 41 | Romania | `ROMANIA` |
| 42 | Saudi Arabia | `SAUDI_ARABIA` |
| 43 | Serbia | `SERBIA` |
| 44 | Slovakia | `SLOVAKIA` |
| 45 | South Korea | `SOUTH_KOREA` |
| 46 | Sweden | `SWEDEN` |
| 47 | Syria | `SYRIA` |
| 48 | Yemen | `YEMEN` |
| 49 | Vietnam | `VIETNAM` |
| 50 | Venezuela | `VENEZUELA` |
| 51 | Tunisia | `TUNISIA` |
| 52 | Thailand | `THAILAND` |
| 53 | Sudan | `SUDAN` |
| 54 | Philippines | `PHILIPPINES` |
| 55 | Morocco | `MOROCCO` |
| 56 | Mexico | `MEXICO` |
| 57 | Malaysia | `MALAYSIA` |
| 58 | Libya | `LIBYA` |
| 59 | Jordan | `JORDAN` |
| 60 | Indonesia | `INDONESIA` |
| 61 | Honduras | `HONDURAS` |
| 62 | Ethiopia | `ETHIOPIA` |
| 63 | Chile | `CHILE` |
| 64 | Brazil | `BRAZIL` |
| 65 | Bahrain | `BAHRAIN` |
| 66 | Third Reich | `THIRDREICH` |
| 67 | Yugoslavia | `YUGOSLAVIA` |
| 68 | USSR | `USSR` |
| 69 | Italian Social Republic | `ITALIAN_SOCIAL_REPUBLIC` |
| 70 | Algeria | `ALGERIA` |
| 71 | Kuwait | `KUWAIT` |
| 72 | Qatar | `QATAR` |
| 73 | Oman | `OMAN` |
| 74 | UAE | `UNITED_ARAB_EMIRATES` |
| 75 | South Africa | `SOUTH_AFRICA` |
| 76 | Cuba | `CUBA` |
| 77 | Portugal | `PORTUGAL` |
| 78 | GDR | `GDR` |
| 79 | Lebanon | `LEBANON` |
| 80 | CJTF Blue | `CJTF_BLUE` |
| 81 | CJTF Red | `CJTF_RED` |
| 82 | UN Peacekeepers | `UN_PEACEKEEPERS` |
| 83 | Argentina | `Argentina` |
| 84 | Cyprus | `Cyprus` |
| 85 | Slovenia | `Slovenia` |
| 86 | Bolivia | `BOLIVIA` |
| 87 | Ghana | `GHANA` |
| 88 | Nigeria | `NIGERIA` |
| 89 | Peru | `PERU` |
| 90 | Ecuador | `ECUADOR` |

**Note:** Index 14 does not exist.

## Coalition Side

```lua
coalition.side = {
    NEUTRAL = 0,
    RED = 1,
    BLUE = 2,
}
```

## Group Categories

```lua
Group.Category = {
    AIRPLANE = 0,
    HELICOPTER = 1,
    GROUND = 2,
    SHIP = 3,
    TRAIN = 4,
}
```

## Airbase Categories

```lua
Airbase.Category = {
    AIRDROME = 0,
    HELIPAD = 1,
    SHIP = 2,
}
```

## Skill Levels

| Value | Description |
|-------|-------------|
| `Average` | Basic AI proficiency |
| `Good` | Competent AI |
| `High` | Skilled AI |
| `Excellent` | Expert AI |
| `Random` | Randomly assigned |
| `Player` | Single-player controllable |
| `Client` | Multiplayer slot |

## Waypoint Types

```lua
AI.Task.WaypointType = {
    TAKEOFF = "TakeOff",
    TAKEOFF_PARKING = "TakeOffParking",
    TAKEOFF_PARKING_HOT = "TakeOffParkingHot",
    TURNING_POINT = "Turning Point",
    LAND = "Land",
}
```

## Altitude Types

```lua
AI.Task.AltitudeType = {
    RADIO = "RADIO",  -- Above Ground Level
    BARO = "BARO",    -- Mean Sea Level
}
```

## Turn Method

```lua
AI.Task.TurnMethod = {
    FLY_OVER_POINT = "Fly Over Point",
    FIN_POINT = "Fin Point",
}
```

## Vehicle Formation

```lua
AI.Task.VehicleFormation = {
    VEE = "Vee",
    ECHELON_RIGHT = "EchelonR",
    OFF_ROAD = "Off Road",
    RANK = "Rank",
    ECHELON_LEFT = "EchelonL",
    ON_ROAD = "On Road",
    CONE = "Cone",
    DIAMOND = "Diamond",
}
```

## Orbit Patterns

```lua
AI.Task.OrbitPattern = {
    RACE_TRACK = "Race-Track",
    CIRCLE = "Circle",
}
```

## Weapon Expenditure

```lua
AI.Task.WeaponExpend = {
    QUARTER = "Quarter",
    TWO = "Two",
    ONE = "One",
    FOUR = "Four",
    HALF = "Half",
    ALL = "All",
}
```

## Designation Types

```lua
AI.Task.Designation = {
    NO = "No",
    WP = "WP",
    IR_POINTER = "IR-Pointer",
    LASER = "Laser",
    AUTO = "Auto",
}
```

## Air Options

### ROE (Rules of Engagement)

| ID | Value | Name |
|----|-------|------|
| 0 | 0 | WEAPON_FREE |
| 0 | 1 | OPEN_FIRE_WEAPON_FREE |
| 0 | 2 | OPEN_FIRE |
| 0 | 3 | RETURN_FIRE |
| 0 | 4 | WEAPON_HOLD |

### Reaction to Threat

| ID | Value | Name |
|----|-------|------|
| 1 | 0 | NO_REACTION |
| 1 | 1 | PASSIVE_DEFENCE |
| 1 | 2 | EVADE_FIRE |
| 1 | 3 | BYPASS_AND_ESCAPE |
| 1 | 4 | ALLOW_ABORT_MISSION |

### Radar Using

| ID | Value | Name |
|----|-------|------|
| 3 | 0 | NEVER |
| 3 | 1 | FOR_ATTACK_ONLY |
| 3 | 2 | FOR_SEARCH_IF_REQUIRED |
| 3 | 3 | FOR_CONTINUOUS_SEARCH |

### Flare Using

| ID | Value | Name |
|----|-------|------|
| 4 | 0 | NEVER |
| 4 | 1 | AGAINST_FIRED_MISSILE |
| 4 | 2 | WHEN_FLYING_IN_SAM_WEZ |
| 4 | 3 | WHEN_FLYING_NEAR_ENEMIES |

### ECM Using

| ID | Value | Name |
|----|-------|------|
| 13 | 0 | NEVER_USE |
| 13 | 1 | USE_IF_ONLY_LOCK_BY_RADAR |
| 13 | 2 | USE_IF_DETECTED_LOCK_BY_RADAR |
| 13 | 3 | ALWAYS_USE |

### Missile Attack Range

| ID | Value | Name |
|----|-------|------|
| 18 | 0 | MAX_RANGE |
| 18 | 1 | NEZ_RANGE |
| 18 | 2 | HALF_WAY_RMAX_NEZ |
| 18 | 3 | TARGET_THREAT_EST |
| 18 | 4 | RANDOM_RANGE |

## Ground Options

### Alarm State

| ID | Value | Name |
|----|-------|------|
| 9 | 0 | AUTO |
| 9 | 1 | GREEN |
| 9 | 2 | RED |

## Smoke Colors

```lua
trigger.smokeColor = {
    Green = 0,
    Red = 1,
    White = 2,
    Orange = 3,
    Blue = 4,
}
```

## Flare Colors

```lua
trigger.flareColor = {
    Green = 0,
    Red = 1,
    White = 2,
    Yellow = 3,
}
```

## Radio Modulation

| Value | Type |
|-------|------|
| 0 | AM |
| 1 | FM |

## Unit Attributes

Attributes are tags that describe unit capabilities:

### Air Attributes
- `Planes`
- `Helicopters`
- `Air`
- `Fighters`
- `Interceptors`
- `Multirole fighters`
- `Bombers`
- `Battleplanes`
- `AWACS`
- `Tankers`
- `Transports`
- `UAVs`
- `Attack helicopters`
- `Transport helicopters`

### Ground Attributes
- `Ground Units`
- `Ground vehicles`
- `Vehicles`
- `Armed vehicles`
- `Unarmed vehicles`
- `Armored vehicles`
- `Tanks`
- `Modern Tanks`
- `Old Tanks`
- `IFV`
- `APC`
- `Artillery`
- `MLRS`
- `Infantry`
- `Infantry carriers`

### Air Defense Attributes
- `Air Defence`
- `Armed Air Defence`
- `SAM`
- `SAM related`
- `SAM elements`
- `SAM SR` (Search Radar)
- `SAM TR` (Track Radar)
- `SAM LL` (Launcher)
- `SAM CC` (Command Center)
- `SR SAM` (Short Range)
- `MR SAM` (Medium Range)
- `LR SAM` (Long Range)
- `AAA`
- `Static AAA`
- `Mobile AAA`
- `MANPADS`
- `EWR`

### Naval Attributes
- `Ships`
- `Armed ships`
- `Unarmed ships`
- `Heavy armed ships`
- `Light armed ships`
- `Aircraft Carriers`
- `Cruisers`
- `Destroyers`
- `Frigates`
- `Corvettes`

## Callsign Names (NATO)

| Index | Callsign |
|-------|----------|
| 1 | Enfield |
| 2 | Springfield |
| 3 | Uzi |
| 4 | Colt |
| 5 | Dodge |
| 6 | Ford |
| 7 | Chevy |
| 8 | Pontiac |
| 9 | Hawg |
| 10 | Boar |
| 11 | Pig |
| 12 | Tusk |

## Caucasus Map Airbases

| ID | Name |
|----|------|
| 12 | Anapa-Vityazevo |
| 13 | Krasnodar-Center |
| 14 | Novorossiysk |
| 15 | Krymsk |
| 16 | Maykop-Khanskaya |
| 17 | Gelendzhik |
| 18 | Sochi-Adler |
| 19 | Krasnodar-Pashkovsky |
| 20 | Sukhumi-Babushara |
| 21 | Gudauta |
| 22 | Batumi |
| 23 | Senaki-Kolkhi |
| 24 | Kobuleti |
| 25 | Kutaisi |
| 26 | Mineralnye Vody |
| 27 | Nalchik |
| 28 | Mozdok |
| 29 | Tbilisi-Lochini |
| 30 | Soganlug |
| 31 | Vaziani |
| 32 | Beslan |
