# Mission Examples

Complete examples demonstrating how to build DCS missions programmatically.

## Example 1: Basic Air-to-Air Mission

A simple CAP mission with blue fighters defending against red attackers.

### Mission File Structure

```lua
mission = {
    ["date"] = {
        ["Year"] = 2024,
        ["Day"] = 15,
        ["Month"] = 6,
    },
    ["start_time"] = 36000,  -- 10:00 AM
    ["theatre"] = "Caucasus",
    ["version"] = 23,
    ["currentKey"] = 100,
    ["maxDictId"] = 5,
    
    -- Briefing references
    ["sortie"] = "DictKey_sortie_5",
    ["descriptionText"] = "DictKey_descriptionText_1",
    ["descriptionBlueTask"] = "DictKey_descriptionBlueTask_3",
    ["descriptionRedTask"] = "DictKey_descriptionRedTask_2",
    ["descriptionNeutralsTask"] = "DictKey_descriptionNeutralsTask_4",
    ["pictureFileNameB"] = {},
    ["pictureFileNameR"] = {},
    ["pictureFileNameN"] = {},
    ["pictureFileNameServer"] = {},
    
    -- Ground control
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
    
    -- Required modules
    ["requiredModules"] = {},
    
    -- Weather - clear day
    ["weather"] = {
        ["atmosphere_type"] = 0,
        ["type_weather"] = 0,
        ["name"] = "Clear",
        ["modifiedTime"] = false,
        ["season"] = { ["temperature"] = 22 },
        ["qnh"] = 760,
        ["groundTurbulence"] = 0,
        ["wind"] = {
            ["atGround"] = { ["speed"] = 3, ["dir"] = 270 },
            ["at2000"] = { ["speed"] = 5, ["dir"] = 280 },
            ["at8000"] = { ["speed"] = 10, ["dir"] = 290 },
        },
        ["visibility"] = { ["distance"] = 80000 },
        ["clouds"] = {
            ["preset"] = "Preset1",
            ["base"] = 3000,
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
    
    -- Coalition assignments
    ["coalitions"] = {
        ["blue"] = { [1] = 2 },   -- USA
        ["red"] = { [1] = 0 },    -- Russia
        ["neutrals"] = {},
    },
    
    -- Coalition data with units
    ["coalition"] = {
        ["blue"] = {
            ["bullseye"] = { ["x"] = -291014, ["y"] = 617414 },
            ["nav_points"] = {},
            ["name"] = "blue",
            ["country"] = {
                [1] = {
                    ["id"] = 2,
                    ["name"] = "USA",
                    ["plane"] = {
                        ["group"] = {
                            -- Blue CAP Flight
                            [1] = {
                                ["name"] = "Blue-CAP-1",
                                ["groupId"] = 1,
                                ["task"] = "CAP",
                                ["uncontrolled"] = false,
                                ["communication"] = true,
                                ["frequency"] = 251,
                                ["modulation"] = 0,
                                ["radioSet"] = false,
                                ["hidden"] = false,
                                ["x"] = -317688,
                                ["y"] = 636897,
                                ["start_time"] = 0,
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
                                            ["formation_template"] = "",
                                            ["task"] = {
                                                ["id"] = "ComboTask",
                                                ["params"] = { ["tasks"] = {} },
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
                                            ["ETA"] = 600,
                                            ["ETA_locked"] = false,
                                            ["formation_template"] = "",
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
                                                                ["maxDist"] = 80000,
                                                                ["maxDistEnabled"] = true,
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
                                    },
                                },
                                ["units"] = {
                                    [1] = {
                                        ["name"] = "Blue-CAP-1-1",
                                        ["unitId"] = 1,
                                        ["type"] = "F-16C_50",
                                        ["x"] = -317688,
                                        ["y"] = 636897,
                                        ["alt"] = 18,
                                        ["alt_type"] = "BARO",
                                        ["speed"] = 138.89,
                                        ["heading"] = 1.57,
                                        ["skill"] = "High",
                                        ["livery_id"] = "default",
                                        ["psi"] = 0,
                                        ["onboard_num"] = "001",
                                        ["parking"] = "15",
                                        ["parking_id"] = "30",
                                        ["payload"] = {
                                            ["pylons"] = {
                                                [1] = { ["CLSID"] = "{40EF17B7-F508-45de-8566-6FFECC0C1AB8}" },
                                                [9] = { ["CLSID"] = "{40EF17B7-F508-45de-8566-6FFECC0C1AB8}" },
                                                [4] = { ["CLSID"] = "{C8E06185-7CD6-4C90-959F-044679E90751}" },
                                                [6] = { ["CLSID"] = "{C8E06185-7CD6-4C90-959F-044679E90751}" },
                                            },
                                            ["fuel"] = 3249,
                                            ["flare"] = 60,
                                            ["chaff"] = 60,
                                            ["gun"] = 100,
                                        },
                                        ["callsign"] = {
                                            [1] = 1,
                                            [2] = 1,
                                            [3] = 1,
                                            ["name"] = "Enfield11",
                                        },
                                    },
                                    [2] = {
                                        ["name"] = "Blue-CAP-1-2",
                                        ["unitId"] = 2,
                                        ["type"] = "F-16C_50",
                                        ["x"] = -317700,
                                        ["y"] = 636850,
                                        ["alt"] = 18,
                                        ["alt_type"] = "BARO",
                                        ["speed"] = 138.89,
                                        ["heading"] = 1.57,
                                        ["skill"] = "High",
                                        ["livery_id"] = "default",
                                        ["psi"] = 0,
                                        ["onboard_num"] = "002",
                                        ["parking"] = "14",
                                        ["parking_id"] = "29",
                                        ["payload"] = {
                                            ["pylons"] = {
                                                [1] = { ["CLSID"] = "{40EF17B7-F508-45de-8566-6FFECC0C1AB8}" },
                                                [9] = { ["CLSID"] = "{40EF17B7-F508-45de-8566-6FFECC0C1AB8}" },
                                                [4] = { ["CLSID"] = "{C8E06185-7CD6-4C90-959F-044679E90751}" },
                                                [6] = { ["CLSID"] = "{C8E06185-7CD6-4C90-959F-044679E90751}" },
                                            },
                                            ["fuel"] = 3249,
                                            ["flare"] = 60,
                                            ["chaff"] = 60,
                                            ["gun"] = 100,
                                        },
                                        ["callsign"] = {
                                            [1] = 1,
                                            [2] = 1,
                                            [3] = 2,
                                            ["name"] = "Enfield12",
                                        },
                                    },
                                },
                            },
                        },
                    },
                },
            },
        },
        ["red"] = {
            ["bullseye"] = { ["x"] = 11557, ["y"] = 371700 },
            ["nav_points"] = {},
            ["name"] = "red",
            ["country"] = {
                [1] = {
                    ["id"] = 0,
                    ["name"] = "Russia",
                    ["plane"] = {
                        ["group"] = {
                            -- Red Striker Flight
                            [1] = {
                                ["name"] = "Red-Strike-1",
                                ["groupId"] = 2,
                                ["task"] = "Ground Attack",
                                ["uncontrolled"] = false,
                                ["communication"] = true,
                                ["frequency"] = 124,
                                ["modulation"] = 0,
                                ["radioSet"] = false,
                                ["hidden"] = false,
                                ["x"] = -50000,
                                ["y"] = 750000,
                                ["start_time"] = 600,  -- Spawn after 10 minutes
                                ["route"] = {
                                    ["points"] = {
                                        [1] = {
                                            ["alt"] = 5000,
                                            ["type"] = "Turning Point",
                                            ["action"] = "Turning Point",
                                            ["alt_type"] = "BARO",
                                            ["speed"] = 200,
                                            ["x"] = -50000,
                                            ["y"] = 750000,
                                            ["ETA"] = 0,
                                            ["ETA_locked"] = true,
                                            ["task"] = {
                                                ["id"] = "ComboTask",
                                                ["params"] = { ["tasks"] = {} },
                                            },
                                        },
                                        [2] = {
                                            ["alt"] = 3000,
                                            ["type"] = "Turning Point",
                                            ["action"] = "Turning Point",
                                            ["alt_type"] = "BARO",
                                            ["speed"] = 250,
                                            ["x"] = -290000,
                                            ["y"] = 680000,
                                            ["task"] = {
                                                ["id"] = "ComboTask",
                                                ["params"] = { ["tasks"] = {} },
                                            },
                                        },
                                    },
                                },
                                ["units"] = {
                                    [1] = {
                                        ["name"] = "Red-Strike-1-1",
                                        ["unitId"] = 3,
                                        ["type"] = "MiG-29A",
                                        ["x"] = -50000,
                                        ["y"] = 750000,
                                        ["alt"] = 5000,
                                        ["alt_type"] = "BARO",
                                        ["speed"] = 200,
                                        ["heading"] = 3.14,
                                        ["skill"] = "Good",
                                        ["payload"] = {
                                            ["pylons"] = {},
                                            ["fuel"] = 3500,
                                            ["flare"] = 30,
                                            ["chaff"] = 30,
                                            ["gun"] = 100,
                                        },
                                        ["callsign"] = 101,
                                    },
                                    [2] = {
                                        ["name"] = "Red-Strike-1-2",
                                        ["unitId"] = 4,
                                        ["type"] = "MiG-29A",
                                        ["x"] = -50050,
                                        ["y"] = 750050,
                                        ["alt"] = 5000,
                                        ["alt_type"] = "BARO",
                                        ["speed"] = 200,
                                        ["heading"] = 3.14,
                                        ["skill"] = "Good",
                                        ["payload"] = {
                                            ["pylons"] = {},
                                            ["fuel"] = 3500,
                                            ["flare"] = 30,
                                            ["chaff"] = 30,
                                            ["gun"] = 100,
                                        },
                                        ["callsign"] = 102,
                                    },
                                },
                            },
                        },
                    },
                },
            },
        },
        ["neutrals"] = {
            ["bullseye"] = { ["x"] = 0, ["y"] = 0 },
            ["nav_points"] = {},
            ["name"] = "neutrals",
            ["country"] = {},
        },
    },
    
    -- Triggers
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
    
    -- Results
    ["result"] = {
        ["total"] = 0,
        ["offline"] = { ["conditions"] = {}, ["actions"] = {}, ["func"] = {} },
        ["blue"] = { ["conditions"] = {}, ["actions"] = {}, ["func"] = {} },
        ["red"] = { ["conditions"] = {}, ["actions"] = {}, ["func"] = {} },
    },
    ["goals"] = {},
    
    -- Map display
    ["map"] = {
        ["centerX"] = -285000,
        ["centerY"] = 680000,
        ["zoom"] = 150000,
    },
    
    ["failures"] = {},
    ["forcedOptions"] = {},
}
```

## Example 2: Ground Attack Training

A simple CAS training scenario with player helicopter and ground targets.

### Dictionary File

```lua
dictionary = {
    ["DictKey_descriptionText_1"] = "Close Air Support Training Mission\n\nObjective: Destroy enemy armor convoy",
    ["DictKey_descriptionBlueTask_3"] = "Locate and destroy the enemy armor convoy moving through the valley.",
    ["DictKey_descriptionRedTask_2"] = "Defend against air attack.",
    ["DictKey_descriptionNeutralsTask_4"] = "",
    ["DictKey_sortie_5"] = "CAS Training",
}
```

### Ground Target Group Example

```lua
-- Within red coalition country vehicle group
{
    ["name"] = "Enemy-Convoy-1",
    ["groupId"] = 10,
    ["task"] = "Ground Nothing",
    ["visible"] = false,
    ["uncontrollable"] = false,
    ["hidden"] = false,
    ["x"] = -286000,
    ["y"] = 678000,
    ["start_time"] = 0,
    ["route"] = {
        ["points"] = {
            [1] = {
                ["x"] = -286000,
                ["y"] = 678000,
                ["alt"] = 35,
                ["alt_type"] = "BARO",
                ["type"] = "Turning Point",
                ["action"] = "On Road",
                ["speed"] = 8.33,
                ["speed_locked"] = true,
                ["ETA"] = 0,
                ["ETA_locked"] = true,
                ["task"] = {
                    ["id"] = "ComboTask",
                    ["params"] = { ["tasks"] = {} },
                },
            },
            [2] = {
                ["x"] = -280000,
                ["y"] = 682000,
                ["alt"] = 40,
                ["type"] = "Turning Point",
                ["action"] = "On Road",
                ["speed"] = 8.33,
                ["task"] = {
                    ["id"] = "ComboTask",
                    ["params"] = { ["tasks"] = {} },
                },
            },
        },
    },
    ["units"] = {
        [1] = {
            ["name"] = "Enemy-Convoy-1-1",
            ["unitId"] = 11,
            ["type"] = "T-72B",
            ["x"] = -286000,
            ["y"] = 678000,
            ["heading"] = 0.5,
            ["skill"] = "Average",
            ["playerCanDrive"] = false,
        },
        [2] = {
            ["name"] = "Enemy-Convoy-1-2",
            ["unitId"] = 12,
            ["type"] = "T-72B",
            ["x"] = -286030,
            ["y"] = 677970,
            ["heading"] = 0.5,
            ["skill"] = "Average",
            ["playerCanDrive"] = false,
        },
        [3] = {
            ["name"] = "Enemy-Convoy-1-3",
            ["unitId"] = 13,
            ["type"] = "BTR-80",
            ["x"] = -286060,
            ["y"] = 677940,
            ["heading"] = 0.5,
            ["skill"] = "Average",
            ["playerCanDrive"] = false,
        },
        [4] = {
            ["name"] = "Enemy-Convoy-1-4",
            ["unitId"] = 14,
            ["type"] = "BTR-80",
            ["x"] = -286090,
            ["y"] = 677910,
            ["heading"] = 0.5,
            ["skill"] = "Average",
            ["playerCanDrive"] = false,
        },
    },
}
```

## Python Mission Generator Template

```python
import json
import zipfile
from datetime import datetime

class DCSMissionBuilder:
    """Simple DCS mission generator."""
    
    def __init__(self, theatre="Caucasus"):
        self.theatre = theatre
        self.group_id = 1
        self.unit_id = 1
        self.blue_groups = []
        self.red_groups = []
        
    def next_group_id(self):
        gid = self.group_id
        self.group_id += 1
        return gid
    
    def next_unit_id(self):
        uid = self.unit_id
        self.unit_id += 1
        return uid
    
    def add_aircraft_group(self, coalition, country_id, name, aircraft_type, 
                           x, y, altitude, task="CAP", skill="High"):
        """Add a simple aircraft group."""
        group = {
            "name": name,
            "groupId": self.next_group_id(),
            "task": task,
            "communication": True,
            "frequency": 251,
            "modulation": 0,
            "x": x,
            "y": y,
            "start_time": 0,
            "route": {
                "points": [{
                    "alt": altitude,
                    "type": "Turning Point",
                    "action": "Turning Point",
                    "alt_type": "BARO",
                    "speed": 200,
                    "x": x,
                    "y": y,
                    "task": {"id": "ComboTask", "params": {"tasks": []}},
                }]
            },
            "units": [{
                "name": f"{name}-1",
                "unitId": self.next_unit_id(),
                "type": aircraft_type,
                "x": x,
                "y": y,
                "alt": altitude,
                "alt_type": "BARO",
                "speed": 200,
                "heading": 0,
                "skill": skill,
                "payload": {
                    "pylons": {},
                    "fuel": 3000,
                    "flare": 60,
                    "chaff": 60,
                    "gun": 100,
                },
                "callsign": {"1": 1, "2": 1, "3": 1, "name": "Enfield11"},
            }],
        }
        
        if coalition == "blue":
            self.blue_groups.append((country_id, "plane", group))
        else:
            self.red_groups.append((country_id, "plane", group))
    
    def add_ground_group(self, coalition, country_id, name, vehicle_type, 
                         x, y, count=4, skill="Average"):
        """Add a ground vehicle group."""
        units = []
        for i in range(count):
            units.append({
                "name": f"{name}-{i+1}",
                "unitId": self.next_unit_id(),
                "type": vehicle_type,
                "x": x - (i * 30),
                "y": y,
                "heading": 0,
                "skill": skill,
                "playerCanDrive": True,
            })
        
        group = {
            "name": name,
            "groupId": self.next_group_id(),
            "task": "Ground Nothing",
            "visible": False,
            "x": x,
            "y": y,
            "start_time": 0,
            "route": {
                "points": [{
                    "x": x,
                    "y": y,
                    "alt": 0,
                    "type": "Turning Point",
                    "action": "Off Road",
                    "speed": 0,
                    "task": {"id": "ComboTask", "params": {"tasks": []}},
                }]
            },
            "units": units,
        }
        
        if coalition == "blue":
            self.blue_groups.append((country_id, "vehicle", group))
        else:
            self.red_groups.append((country_id, "vehicle", group))
    
    def _build_country_data(self, groups):
        """Build country structure from groups."""
        countries = {}
        for country_id, category, group in groups:
            if country_id not in countries:
                countries[country_id] = {"id": country_id, "name": str(country_id)}
            if category not in countries[country_id]:
                countries[country_id][category] = {"group": []}
            countries[country_id][category]["group"].append(group)
        return list(countries.values())
    
    def generate_mission(self):
        """Generate complete mission data."""
        return f'''mission = {{
    ["date"] = {{ ["Year"] = 2024, ["Day"] = 15, ["Month"] = 6 }},
    ["start_time"] = 36000,
    ["theatre"] = "{self.theatre}",
    ["version"] = 23,
    ["currentKey"] = 100,
    ["maxDictId"] = 5,
    ["sortie"] = "DictKey_sortie_5",
    ["descriptionText"] = "DictKey_descriptionText_1",
    ["descriptionBlueTask"] = "DictKey_descriptionBlueTask_3",
    ["descriptionRedTask"] = "DictKey_descriptionRedTask_2",
    ["descriptionNeutralsTask"] = "DictKey_descriptionNeutralsTask_4",
    ["pictureFileNameB"] = {{}},
    ["pictureFileNameR"] = {{}},
    ["pictureFileNameN"] = {{}},
    ["pictureFileNameServer"] = {{}},
    ["groundControl"] = {{
        ["isPilotControlVehicles"] = false,
        ["passwords"] = {{
            ["artillery_commander"] = {{}},
            ["instructor"] = {{}},
            ["observer"] = {{}},
            ["forward_observer"] = {{}},
        }},
        ["roles"] = {{
            ["artillery_commander"] = {{ ["neutrals"] = 0, ["blue"] = 0, ["red"] = 0 }},
            ["instructor"] = {{ ["neutrals"] = 0, ["blue"] = 0, ["red"] = 0 }},
            ["observer"] = {{ ["neutrals"] = 0, ["blue"] = 0, ["red"] = 0 }},
            ["forward_observer"] = {{ ["neutrals"] = 0, ["blue"] = 0, ["red"] = 0 }},
        }},
    }},
    ["requiredModules"] = {{}},
    ["weather"] = {{
        ["atmosphere_type"] = 0,
        ["type_weather"] = 0,
        ["name"] = "Clear",
        ["modifiedTime"] = false,
        ["season"] = {{ ["temperature"] = 20 }},
        ["qnh"] = 760,
        ["groundTurbulence"] = 0,
        ["wind"] = {{
            ["atGround"] = {{ ["speed"] = 0, ["dir"] = 0 }},
            ["at2000"] = {{ ["speed"] = 0, ["dir"] = 0 }},
            ["at8000"] = {{ ["speed"] = 0, ["dir"] = 0 }},
        }},
        ["visibility"] = {{ ["distance"] = 80000 }},
        ["clouds"] = {{
            ["preset"] = "Preset1",
            ["base"] = 3000,
            ["density"] = 0,
            ["thickness"] = 200,
            ["iprecptns"] = 0,
        }},
        ["enable_fog"] = false,
        ["fog"] = {{ ["visibility"] = 0, ["thickness"] = 0 }},
        ["enable_dust"] = false,
        ["dust_density"] = 0,
        ["cyclones"] = {{}},
        ["halo"] = {{ ["preset"] = "auto" }},
    }},
    ["coalitions"] = {{
        ["blue"] = {{ [1] = 2 }},
        ["red"] = {{ [1] = 0 }},
        ["neutrals"] = {{}},
    }},
    ["coalition"] = {{
        ["blue"] = {{
            ["bullseye"] = {{ ["x"] = -291014, ["y"] = 617414 }},
            ["nav_points"] = {{}},
            ["name"] = "blue",
            ["country"] = {{}},
        }},
        ["red"] = {{
            ["bullseye"] = {{ ["x"] = 11557, ["y"] = 371700 }},
            ["nav_points"] = {{}},
            ["name"] = "red",
            ["country"] = {{}},
        }},
        ["neutrals"] = {{
            ["bullseye"] = {{ ["x"] = 0, ["y"] = 0 }},
            ["nav_points"] = {{}},
            ["name"] = "neutrals",
            ["country"] = {{}},
        }},
    }},
    ["trig"] = {{
        ["actions"] = {{}},
        ["events"] = {{}},
        ["custom"] = {{}},
        ["func"] = {{}},
        ["flag"] = {{}},
        ["conditions"] = {{}},
        ["customStartup"] = {{}},
        ["funcStartup"] = {{}},
    }},
    ["triggers"] = {{ ["zones"] = {{}} }},
    ["trigrules"] = {{}},
    ["result"] = {{
        ["total"] = 0,
        ["offline"] = {{ ["conditions"] = {{}}, ["actions"] = {{}}, ["func"] = {{}} }},
        ["blue"] = {{ ["conditions"] = {{}}, ["actions"] = {{}}, ["func"] = {{}} }},
        ["red"] = {{ ["conditions"] = {{}}, ["actions"] = {{}}, ["func"] = {{}} }},
    }},
    ["goals"] = {{}},
    ["map"] = {{
        ["centerX"] = -285000,
        ["centerY"] = 680000,
        ["zoom"] = 100000,
    }},
    ["failures"] = {{}},
    ["forcedOptions"] = {{}},
}}
'''

# Usage example
if __name__ == "__main__":
    builder = DCSMissionBuilder("Caucasus")
    builder.add_aircraft_group("blue", 2, "Blue-CAP", "F-16C_50", 
                               -290000, 680000, 7000)
    builder.add_ground_group("red", 0, "Red-Armor", "T-72B", 
                             -286000, 678000, count=4)
    
    mission_data = builder.generate_mission()
    print(mission_data)
```

## Validating Generated Missions

1. **Open in DCS Mission Editor** - Best validation method
2. **Check Lua syntax** - Use a Lua parser
3. **Verify coordinates** - Ensure they're within map bounds
4. **Check unit types** - Must match DCS database exactly
5. **Verify IDs are unique** - No duplicate groupId or unitId values
