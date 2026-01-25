# DCS Mission Generation Prompt Guide

This guide helps you write effective prompts to generate complete, working DCS World missions. Use this as a reference when asking an AI to create missions for you.

## Quick Start Template

Copy and fill in this template for basic missions:

```
Generate a DCS World mission with the following specifications:

**Map:** [Caucasus/Syria/Persian Gulf/etc.]
**Date/Time:** [YYYY-MM-DD, HH:MM local]
**Weather:** [Clear/Cloudy/Overcast/Rain]

**Blue Forces (Player Side):**
- [Number] x [Aircraft Type] at [Location/Airbase], task: [CAP/CAS/Strike/etc.]
- Player slot: [Yes/No]

**Red Forces (Enemy):**
- [Number] x [Aircraft/Vehicle Type] at [Location], task: [Description]

**Mission Objective:**
[Brief description of what the player should accomplish]

**Output Format:** Complete .miz file contents (mission, options, warehouses, theatre, dictionary files)
```

---

## Essential Information Checklist

For any mission generation prompt, include:

### Required Elements

| Element | Description | Example |
|---------|-------------|---------|
| **Theatre/Map** | Which DCS map to use | Caucasus, Syria, Persian Gulf |
| **Date** | Mission date | 2024-06-15 |
| **Start Time** | Local time | 08:00, 14:30 |
| **Coalition Setup** | Which countries on each side | Blue: USA, UK / Red: Russia |
| **At least one unit** | Player or AI unit | F-16C at Kobuleti |

### Recommended Elements

| Element | Description | Example |
|---------|-------------|---------|
| **Weather** | Conditions | Clear, scattered clouds, 20°C |
| **Wind** | Speed and direction | 5 kts from 270° |
| **Mission objective** | What to accomplish | Destroy convoy |
| **Briefing text** | Mission description | "Intercept incoming bombers" |

---

## Prompt Templates by Mission Type

### 1. Air-to-Air Combat (CAP/Intercept)

```
Generate a DCS World air-to-air mission:

**Theatre:** Caucasus
**Date:** 2024-06-15
**Time:** 10:00 local
**Weather:** Clear skies, visibility 80km, temp 22°C

**Blue Coalition (USA):**
- 2x F-16C_50 "Viper" at Kobuleti (parking, cold start)
  - Callsign: Enfield 1
  - Task: CAP
  - Loadout: 4x AIM-120C, 2x AIM-9X, fuel tank
  - Skill: Client (multiplayer slot)
- 1x E-3A AWACS orbiting at waypoint BULLSEYE, angels 30
  - Callsign: Overlord
  - Frequency: 251.0 AM

**Red Coalition (Russia):**
- 4x MiG-29A spawning from the north at mission time +15 minutes
  - Altitude: 20,000 ft
  - Heading: South toward Batumi
  - Task: Fighter sweep
  - Skill: Good

**Trigger Zones:**
- "CAP Station" - Circle, 30nm radius, centered on N41°45' E042°10'

**Mission Objective:** 
Defend Georgian airspace. Intercept and destroy hostile aircraft approaching from the north.

**Briefing:**
"Intelligence reports indicate hostile fighter activity north of the border. 
Launch immediately and establish a CAP station. AWACS Overlord will provide radar coverage."

Generate complete mission files: mission, options, warehouses, theatre, dictionary
```

### 2. Close Air Support (CAS)

```
Generate a DCS World CAS training mission:

**Theatre:** Caucasus  
**Date:** 2024-07-20
**Time:** 14:00 local
**Weather:** Few clouds at 8000ft, visibility 50km, temp 28°C

**Blue Coalition (USA):**
- 1x AH-64D Apache at FARP London (hot start)
  - Callsign: Ugly 1-1
  - Task: CAS
  - Loadout: 8x Hellfire, 38x rockets, 300x 30mm
  - Skill: Client
- 1x MQ-9 Reaper orbiting overhead as JTAC
  - Callsign: Axeman
  - Laser code: 1688
  - Frequency: 135.0 AM

**Red Coalition (Russia):**
- Convoy "Target Alpha" - 4x T-72B3, 2x BMP-2, 2x Ural trucks
  - Location: Road between N42°15' E042°30' and N42°18' E042°35'
  - Moving at 30 km/h on road
  - No air defense
  
- Static defense "Target Bravo" - 2x ZSU-23-4 Shilka, infantry
  - Location: Crossroads at N42°20' E042°32'
  - Stationary, high alert

**Trigger Zones:**
- "Engagement Zone" - covers both target areas

**Mission Objective:**
Destroy enemy armor convoy and static defense position.
JTAC will provide laser designation.

Generate all mission files with realistic Caucasus coordinates.
```

### 3. SEAD/DEAD Mission

```
Generate a DCS World SEAD mission:

**Theatre:** Syria
**Date:** 2024-03-15
**Time:** 06:30 local (dawn)
**Weather:** Haze, visibility 20km, scattered clouds at 12000ft

**Blue Coalition (USA, Israel):**
- 2x F-16C_50 (SEAD package) at Ramat David
  - Loadout: 2x AGM-88C HARM, 2x AIM-120, targeting pod
  - Task: SEAD
  - Skill: Client (lead), High (wingman)
  
- 2x F-15E Strike Eagle (strike package) at Ramat David
  - Loadout: 4x GBU-12, 2x AIM-120
  - Task: Ground Attack
  - Start time: +10 minutes after SEAD
  - Skill: Excellent

**Red Coalition (Syria):**
- SA-6 Gainful battery at N33°45' E036°20'
  - 1x Straight Flush radar
  - 3x TEL launchers
  - Skill: High
  
- SA-11 Buk battery at N33°50' E036°25'
  - Full battery (SR, TR, TELs)
  - Skill: Excellent
  
- EWR site at N33°55' E036°30'
  - 1x 55G6 EWR

**Mission Objective:**
Suppress enemy air defenses to enable follow-on strike package.
Primary: SA-11 site. Secondary: SA-6 site.

Generate with proper SAM threat rings visible on F10 map.
```

### 4. Helicopter Operations

```
Generate a DCS World helicopter transport/assault mission:

**Theatre:** Caucasus
**Date:** 2024-08-10
**Time:** 05:45 local (pre-dawn)
**Weather:** Fog in valleys (visibility 2km below 500m AGL), clear above

**Blue Coalition (USA):**
- 2x UH-60L Blackhawk at Kobuleti
  - Callsign: Dustoff 1
  - Task: Transport
  - Carrying: Infantry squad (8 troops each)
  - Skill: Client, High
  
- 2x AH-64D Apache as escort
  - Callsign: Ugly 1
  - Loadout: 16x Hellfire, rockets
  - Task: Escort/CAS
  - Skill: Excellent

**Landing Zone:**
- LZ "Falcon" at N42°05' E043°15' (valley clearing)
- Mark with green smoke trigger

**Red Coalition (Russia):**
- Infantry platoon defending hilltop near LZ
  - 12x Soldiers with small arms
  - 2x DShK heavy MG positions
  
- QRF 5km away
  - 2x BTR-80
  - Triggered to move toward LZ when blue crosses trigger zone

**Mission Objective:**
Insert special forces team at LZ Falcon.
Apaches provide cover, neutralize threats before landing.

Include waypoints: Kobuleti -> IP -> LZ -> RTB
```

### 5. Naval Strike

```
Generate a DCS World anti-ship mission:

**Theatre:** Persian Gulf
**Date:** 2024-05-20
**Time:** 11:00 local
**Weather:** Clear, sea state calm

**Blue Coalition (USA):**
- 4x F/A-18C Hornet from CVN-74 Stennis
  - Position: N26°30' E052°00'
  - Loadout: 2x AGM-84D Harpoon, 2x AIM-120, 2x AIM-9X
  - Task: Antiship Strike
  - Skill: Client (1), Excellent (3)
  
- 1x E-2D Hawkeye for AEW
  - Orbiting over carrier

**Carrier Group:**
- CVN-74 Stennis
- 2x CG Ticonderoga escorts
- Heading: 270° at 15 kts

**Red Coalition (Iran):**
- Surface Action Group at N27°00' E054°30'
  - 1x Alvand-class frigate
  - 2x Kaman-class missile boats
  - Heading: 180° at 20 kts
  - ROE: Weapons free

**Mission Objective:**
Locate and destroy hostile surface group threatening shipping lanes.
Expect return fire from ship-based SAMs.

Generate with carrier operations (Case I recovery).
```

### 6. Simple Training Mission

```
Generate a simple DCS World training mission:

**Theatre:** Caucasus
**Date:** 2024-01-15
**Time:** 12:00 noon
**Weather:** Perfect VFR - clear, no wind, 15°C

**Blue Coalition (USA):**
- 1x [AIRCRAFT TYPE] at Batumi
  - Hot start on runway
  - Full fuel, training loadout
  - Skill: Player (single player)

**No enemies - free flight training**

**Waypoints:**
1. Batumi (takeoff)
2. Coast - N41°40' E041°45' - 5000ft
3. Mountains - N41°50' E042°30' - 15000ft  
4. Batumi (landing)

**Mission Objective:**
Practice takeoff, navigation, and landing.

Generate minimal mission with no threats.
```

---

## Specifying Coordinates

### Option 1: Named Locations
```
Location: Kobuleti Airbase
Location: 10nm north of Batumi
Location: Over the Black Sea, 50nm west of Poti
```

### Option 2: Lat/Long (Preferred for precision)
```
Position: N41°55'30" E041°52'15"
Position: 41.925, 41.8708 (decimal degrees)
```

### Option 3: DCS Internal Coordinates
```
Position: x=-317688, y=636897 (Kobuleti reference)
```

### Option 4: Relative to Bullseye
```
Position: Bullseye 045/50 (45° bearing, 50nm from bullseye)
```

---

## Specifying Aircraft Loadouts

### Simple Method
```
Loadout: Air-to-air configuration
Loadout: SEAD loadout
Loadout: Full CAS loadout
Loadout: Clean (no weapons)
```

### Detailed Method
```
Loadout:
- Pylon 1: AIM-9X
- Pylon 2: Empty
- Pylon 3: AIM-120C
- Pylon 4: Fuel tank 370gal
- Pylon 5: LANTIRN TGP
- Pylon 6: Fuel tank 370gal
- Pylon 7: AIM-120C
- Pylon 8: Empty
- Pylon 9: AIM-9X
- Gun: 100%
- Chaff: 60
- Flare: 60
```

---

## Specifying Weather

### Simple
```
Weather: Clear and calm
Weather: Overcast with rain
Weather: Winter conditions
```

### Detailed
```
Weather:
- Temperature: 22°C at sea level
- Pressure: 760 mmHg
- Clouds: Scattered at 8000ft, broken at 15000ft
- Visibility: 50km
- Wind at ground: 270° at 5 kts
- Wind at 2000m: 280° at 15 kts
- Wind at 8000m: 290° at 30 kts
- Precipitation: None
- Turbulence: Light
```

---

## Specifying Triggers and Events

```
**Triggers:**

1. "Mission Start Message"
   - Condition: Time > 5 seconds
   - Action: Display message "Welcome to the mission" for 15 seconds

2. "Spawn Enemy Wave 2"
   - Condition: Group "Enemy Wave 1" has fewer than 2 units alive
   - Action: Activate group "Enemy Wave 2"

3. "Victory Condition"
   - Condition: All units in group "Target Convoy" destroyed
   - Action: Display message "Mission Complete!" and set flag 1 to true

4. "Mission Failed"
   - Condition: Player aircraft destroyed
   - Action: Display message "Mission Failed" and end mission
```

---

## Output Format Specification

Always specify what output you need:

### Full Mission Package
```
Generate complete mission files:
- mission (main mission lua)
- options (difficulty settings)
- warehouses (airbase supplies)
- theatre (map name)
- l10n/DEFAULT/dictionary (briefing text)
- l10n/DEFAULT/mapResource (empty)

Provide as separate code blocks that can be saved and zipped into a .miz file.
```

### Mission File Only
```
Generate only the mission lua file. I will use default options and warehouses.
```

### Specific Sections
```
Generate only the coalition/country/units section for the following forces:
[specifications]
```

---

## Common Aircraft Type Strings

Reference these exact strings in your prompts:

| Aircraft | Type String |
|----------|-------------|
| F-16C Viper | `F-16C_50` |
| F/A-18C Hornet | `FA-18C_hornet` |
| F-15C Eagle | `F-15C` |
| F-15E Strike Eagle | `F-15ESE` |
| A-10C Warthog | `A-10C_2` |
| AH-64D Apache | `AH-64D_BLK_II` |
| UH-60L Blackhawk | `UH-60L` |
| MiG-29A | `MiG-29A` |
| MiG-29S | `MiG-29S` |
| Su-27 | `Su-27` |
| Su-33 | `Su-33` |
| Mi-24P Hind | `Mi-24P` |
| Ka-50 | `Ka-50` |
| E-3A AWACS | `E-3A` |
| KC-135 Tanker | `KC135MPRS` |

---

## Common Vehicle Type Strings

| Vehicle | Type String |
|---------|-------------|
| M1A2 Abrams | `M1A2` |
| T-72B3 | `T-72B3` |
| T-80U | `T-80UD` |
| BTR-80 | `BTR-80` |
| BMP-2 | `BMP-2` |
| M-109 Paladin | `M-109` |
| SA-11 Buk (launcher) | `SA-11 Buk LN 9A310M1` |
| SA-11 Buk (radar) | `SA-11 Buk SR 9S18M1` |
| ZSU-23-4 Shilka | `ZSU-23-4 Shilka` |
| Patriot (launcher) | `Patriot ln` |

---

## Example Prompt → Result

### Input Prompt
```
Generate a simple DCS dogfight training mission:

Map: Caucasus
Time: Noon, clear weather
Blue: 1x F-16C player at Kobuleti, air-to-air loadout, hot start on runway
Red: 1x MiG-29A 30nm north, same altitude, heading south
No other units. Just a 1v1 practice.
```

### Expected Output Structure
The AI should generate:

1. **mission** file containing:
   - Date set to current year, clear weather
   - Blue coalition with USA, one F-16C group
   - Red coalition with Russia, one MiG-29A group
   - Proper coordinates for Kobuleti
   - Spawn timing for red aircraft

2. **options** file with default settings

3. **warehouses** file for Caucasus airports

4. **theatre** file containing just `Caucasus`

5. **dictionary** file with briefing text

---

## Troubleshooting Prompts

If generated missions don't work, add these specifications:

```
Additional requirements:
- Ensure all groupId and unitId values are unique
- Use exact DCS type strings for all units
- Include all required fields for each unit type
- Coordinates must be valid for the specified map
- Include proper route/waypoint structure even for stationary units
- Set start_time=0 for immediate spawn, or specify delay in seconds
```

---

## Advanced: Scripted Missions

For missions with Lua scripting:

```
**Scripting Requirements:**

Include initialization script that:
1. Displays welcome message at mission start
2. Creates F10 menu option "Request JTAC Support"
3. Tracks kills and displays score

Include trigger that:
- When all targets destroyed, display "RTB - Mission Complete"
- After 60 minutes, display "Bingo Fuel - RTB Now"

Use MIST library functions if complex spawning needed.
```

---

## Quick Reference Card

Copy this for quick mission requests:

```
DCS Mission Request:
━━━━━━━━━━━━━━━━━━━
Map:        
Date/Time:  
Weather:    

BLUE FORCES:
• Aircraft: 
• Location: 
• Task:     
• Player:   Yes/No

RED FORCES:
• Units:    
• Location: 
• Behavior: 

OBJECTIVE:


OUTPUT: Full .miz file contents
```
