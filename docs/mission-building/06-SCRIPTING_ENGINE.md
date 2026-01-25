# DCS Scripting Engine

The DCS Scripting Engine allows mission designers to add dynamic behavior using Lua scripts. Scripts can be embedded in missions or loaded from external files.

## Overview

The Simulator Scripting Engine (SSE) provides:
- Access to game objects (units, groups, airbases)
- Control over AI behavior
- Mission trigger functionality
- Custom game logic

## Script Execution Methods

### 1. Initialization Script

Runs when the mission loads (before any units spawn).

```lua
-- In mission file trig.funcStartup
["funcStartup"] = {
    [1] = "local myVar = 'Hello World'",
},
```

### 2. Trigger Actions

Run when trigger conditions are met.

```lua
-- DO SCRIPT action
["actions"] = {
    [1] = "a_do_script(\"trigger.action.outText('Message', 10)\")",
},

-- DO SCRIPT FILE action
["actions"] = {
    [1] = "a_do_script_file('scripts/myscript.lua')",
},
```

### 3. Waypoint Actions

Run when a group reaches a waypoint.

```lua
["task"] = {
    ["id"] = "WrappedAction",
    ["params"] = {
        ["action"] = {
            ["id"] = "Script",
            ["params"] = {
                ["command"] = "trigger.action.outText('Waypoint reached', 5)",
            },
        },
    },
},
```

## Singletons (Global Objects)

### env - Environment

```lua
-- Logging
env.info("Information message")
env.warning("Warning message")
env.error("Error message")

-- Mission path
local path = env.mission.missionPath
```

### timer - Time Functions

```lua
-- Get mission time (seconds since mission start)
local missionTime = timer.getTime()

-- Get absolute time
local absTime = timer.getAbsTime()

-- Schedule a function
local function myFunc(arg, time)
    -- Do something
    return time + 60  -- Reschedule in 60 seconds
end
timer.scheduleFunction(myFunc, arg, timer.getTime() + 10)
```

### world - World Access

```lua
-- Get all players
local players = world.getPlayer()

-- Add event handler
local eventHandler = {}
function eventHandler:onEvent(event)
    if event.id == world.event.S_EVENT_SHOT then
        -- Handle shot event
    end
end
world.addEventHandler(eventHandler)

-- Search objects
world.searchObjects(Object.Category.UNIT, {
    id = world.VolumeType.SPHERE,
    params = {
        point = {x = -285000, y = 0, z = 678000},
        radius = 5000
    }
}, function(foundObject)
    -- Process found object
    return true  -- Continue search
end)
```

### coalition - Coalition Functions

```lua
-- Get all groups for a coalition
local blueGroups = coalition.getGroups(coalition.side.BLUE)

-- Get airbases
local blueAirbases = coalition.getAirbases(coalition.side.BLUE)

-- Add group dynamically
coalition.addGroup(country.id.USA, Group.Category.GROUND, groupData)

-- Add static object
coalition.addStaticObject(country.id.USA, staticData)
```

### trigger - Trigger Functions

```lua
-- Display text
trigger.action.outText("Hello World", 10)  -- 10 seconds display
trigger.action.outTextForCoalition(coalition.side.BLUE, "Blue only", 10)
trigger.action.outTextForGroup(groupId, "Group message", 10)

-- Play sound
trigger.action.outSound("sounds/alert.ogg")
trigger.action.outSoundForGroup(groupId, "sounds/beep.ogg")

-- Create effects
trigger.action.smoke({x = -285000, y = 0, z = 678000}, trigger.smokeColor.Red)
trigger.action.explosion({x = -285000, y = 0, z = 678000}, 100)  -- 100 power
trigger.action.illuminationBomb({x = -285000, y = 1000, z = 678000}, 1000000)

-- Get trigger zone
local zone = trigger.misc.getZone("ZoneName")
-- Returns: {point = {x, y, z}, radius = number}

-- Flags
trigger.action.setUserFlag("flag1", 1)
local value = trigger.misc.getUserFlag("flag1")

-- Markers
trigger.action.markToAll(1, "Marker Text", {x = -285000, y = 0, z = 678000})
trigger.action.removeMark(1)

-- Activate/Deactivate groups
trigger.action.activateGroup(Group.getByName("Late-Group"))
trigger.action.deactivateGroup(Group.getByName("Active-Group"))
```

### missionCommands - Radio Menu

```lua
-- Add command to radio menu
local rootMenu = missionCommands.addSubMenu("My Menu")
missionCommands.addCommand("Do Something", rootMenu, myFunction, arg)

-- Coalition-specific
local blueMenu = missionCommands.addSubMenuForCoalition(
    coalition.side.BLUE, "Blue Menu"
)

-- Group-specific
local groupMenu = missionCommands.addSubMenuForGroup(
    groupId, "Group Menu"
)

-- Remove command
missionCommands.removeItem(menuPath)
```

## Classes

### Group

```lua
-- Get group by name
local group = Group.getByName("Fighter-1")

-- Group methods
local name = group:getName()
local id = group:getID()
local size = group:getSize()
local category = group:getCategory()
local coalition = group:getCoalition()
local units = group:getUnits()
local controller = group:getController()

-- Check if exists
if group:isExist() then
    -- Group is alive
end

-- Destroy group
group:destroy()

-- Activate late-activation group
group:activate()
```

### Unit

```lua
-- Get unit by name
local unit = Unit.getByName("Fighter-1-1")

-- Get from group
local unit = group:getUnit(1)  -- First unit

-- Unit methods
local name = unit:getName()
local type = unit:getTypeName()
local position = unit:getPosition()  -- Returns position3
local point = unit:getPoint()  -- Returns vec3
local velocity = unit:getVelocity()
local life = unit:getLife()
local life0 = unit:getLife0()  -- Initial life
local fuel = unit:getFuel()  -- 0-1
local ammo = unit:getAmmo()
local group = unit:getGroup()
local coalition = unit:getCoalition()
local country = unit:getCountry()

-- Is unit alive
if unit:isActive() then
    -- Unit is active
end

-- Is player
if unit:getPlayerName() then
    -- Is player-controlled
end

-- Destroy
unit:destroy()
```

### Controller

```lua
local controller = group:getController()

-- Set task
controller:setTask({
    id = "Orbit",
    params = {
        pattern = "Circle",
        point = {x = -285000, y = 678000},
        altitude = 5000,
        speed = 150,
    }
})

-- Push task (add to queue)
controller:pushTask(task)

-- Reset task
controller:resetTask()

-- Pop current task
controller:popTask()

-- Check if has task
local hasTask = controller:hasTask()

-- Set options
controller:setOption(AI.Option.Air.id.ROE, AI.Option.Air.val.ROE.WEAPON_FREE)

-- Set command
controller:setCommand({
    id = "Script",
    params = {
        command = "env.info('Command executed')"
    }
})

-- Set on/off
controller:setOnOff(true)
```

### Airbase

```lua
-- Get by name
local airbase = Airbase.getByName("Kobuleti")

-- Get all for coalition
local airbases = coalition.getAirbases(coalition.side.BLUE)

-- Airbase methods
local name = airbase:getName()
local id = airbase:getID()
local callsign = airbase:getCallsign()
local point = airbase:getPoint()
local coalition = airbase:getCoalition()

-- Get parking spots
local parking = airbase:getParking()
-- Returns array of: {Term_Index, Term_Type, TO_AC, Term_Index_0, vTerminalPos, fDistToRW}

-- Get runways
local runways = airbase:getRunways()

-- Set coalition (capture)
airbase:setCoalition(coalition.side.RED)
```

### Spot (Laser/IR)

```lua
-- Create laser spot
local spot = Spot.createLaser(
    sourceUnit,
    {x = 0, y = 2, z = 0},  -- Offset from source
    targetPoint,            -- Target position
    1688                    -- Laser code
)

-- Create IR pointer
local ir = Spot.createInfraRed(sourceUnit, offset, targetPoint)

-- Spot methods
spot:setPoint(newPoint)
local code = spot:getCode()
spot:setCode(1687)
spot:destroy()
```

## Events

Subscribe to game events:

```lua
local eventHandler = {}

function eventHandler:onEvent(event)
    if event.id == world.event.S_EVENT_SHOT then
        local shooter = event.initiator
        local weapon = event.weapon
        env.info("Shot fired by: " .. shooter:getName())
        
    elseif event.id == world.event.S_EVENT_HIT then
        local target = event.target
        env.info("Target hit: " .. target:getName())
        
    elseif event.id == world.event.S_EVENT_DEAD then
        local deadUnit = event.initiator
        env.info("Unit died: " .. deadUnit:getName())
        
    elseif event.id == world.event.S_EVENT_BIRTH then
        local unit = event.initiator
        env.info("Unit spawned: " .. unit:getName())
        
    elseif event.id == world.event.S_EVENT_TAKEOFF then
        local unit = event.initiator
        local airbase = event.place
        
    elseif event.id == world.event.S_EVENT_LAND then
        local unit = event.initiator
        local airbase = event.place
    end
end

world.addEventHandler(eventHandler)
```

### Common Events

| Event | Description |
|-------|-------------|
| `S_EVENT_SHOT` | Weapon fired |
| `S_EVENT_HIT` | Target hit |
| `S_EVENT_DEAD` | Unit destroyed |
| `S_EVENT_BIRTH` | Unit spawned |
| `S_EVENT_TAKEOFF` | Aircraft takeoff |
| `S_EVENT_LAND` | Aircraft landed |
| `S_EVENT_CRASH` | Aircraft crashed |
| `S_EVENT_EJECTION` | Pilot ejected |
| `S_EVENT_PLAYER_ENTER_UNIT` | Player entered aircraft |
| `S_EVENT_PLAYER_LEAVE_UNIT` | Player left aircraft |
| `S_EVENT_MARK_ADDED` | Map marker added |
| `S_EVENT_MARK_REMOVED` | Map marker removed |
| `S_EVENT_MARK_CHANGE` | Map marker changed |

## Dynamic Spawning

### Spawn Ground Group

```lua
local groundGroupData = {
    name = "Dynamic-Ground-1",
    task = "Ground Nothing",
    x = -286000,
    y = 678000,
    hidden = false,
    units = {
        [1] = {
            name = "Dynamic-Ground-1-1",
            type = "M1A2",
            x = -286000,
            y = 678000,
            heading = 0,
            skill = "Average",
        },
    },
    route = {
        points = {
            [1] = {
                x = -286000,
                y = 678000,
                type = "Turning Point",
                action = "Off Road",
                speed = 10,
            },
        },
    },
}

coalition.addGroup(country.id.USA, Group.Category.GROUND, groundGroupData)
```

### Spawn Aircraft

```lua
local planeGroupData = {
    name = "Dynamic-Plane-1",
    task = "CAP",
    x = -290000,
    y = 680000,
    communication = true,
    frequency = 251,
    modulation = 0,
    units = {
        [1] = {
            name = "Dynamic-Plane-1-1",
            type = "F-16C_50",
            x = -290000,
            y = 680000,
            alt = 5000,
            alt_type = "BARO",
            speed = 200,
            heading = 0,
            skill = "High",
            payload = {
                pylons = {},
                fuel = 3000,
                flare = 60,
                chaff = 60,
                gun = 100,
            },
            callsign = {
                [1] = 1,
                [2] = 1,
                [3] = 1,
                name = "Enfield11",
            },
        },
    },
    route = {
        points = {
            [1] = {
                x = -290000,
                y = 680000,
                alt = 5000,
                alt_type = "BARO",
                type = "Turning Point",
                action = "Turning Point",
                speed = 200,
            },
        },
    },
}

coalition.addGroup(country.id.USA, Group.Category.AIRPLANE, planeGroupData)
```

## Third-Party Libraries

### MIST (Mission Scripting Tools)

Popular scripting library with many helper functions.

```lua
-- Load via DO SCRIPT FILE trigger
-- Functions include:
mist.respawnGroup("GroupName")
mist.cloneGroup("GroupName", true)
mist.getUnitsInZones(unitTable, zoneTable)
mist.getRandPointInCircle(point, radius)
```

### MOOSE (Mission Object Oriented Scripting Environment)

Comprehensive framework for mission design.

```lua
-- Object-oriented approach
local CAPZone = ZONE:New("CAP Zone")
local CAPGroup = SPAWN:New("CAP Template")
    :InitLimit(4, 2)
    :SpawnInZone(CAPZone, true)
```

## Best Practices

1. **Delay after spawn**: Always wait before accessing newly spawned groups
```lua
timer.scheduleFunction(function()
    local group = Group.getByName("Spawned-Group")
    local controller = group:getController()
    -- Now safe to issue tasks
end, nil, timer.getTime() + 1)
```

2. **Check existence**: Always verify objects exist before using
```lua
local group = Group.getByName("Maybe-Dead")
if group and group:isExist() then
    -- Safe to use
end
```

3. **Use pcall for error handling**:
```lua
local success, result = pcall(function()
    -- Potentially dangerous code
end)
if not success then
    env.error("Error: " .. tostring(result))
end
```

4. **Clean up event handlers**:
```lua
-- Store reference
local handler = {}
function handler:onEvent(event) end
world.addEventHandler(handler)

-- Remove when done
world.removeEventHandler(handler)
```
