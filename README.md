 [![discord](https://img.shields.io/badge/Join-Discord-blue?logo=discord&logoColor=white)](https://discord.gg/Vk7eY8xYV2)
 ![Discord](https://img.shields.io/discord/1048630711881568267?style=flat&label=Online%20Users)
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FMono-94%2FmGarage&count_bg=%23E9A711&title_bg=%23232323&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)
![License](https://img.shields.io/github/license/Mono-94/mGarage)
![Open Issues](https://img.shields.io/github/issues-raw/Mono-94/mGarage?label=open%20issues)
![Closed Issues](https://img.shields.io/github/issues-closed-raw/Mono-94/mGarage?color=success&amp;label=closed%20issues)
![Open PRs](https://img.shields.io/github/issues-pr-raw/Mono-94/mGarage?label=open%20PRs)
![Closed PRs](https://img.shields.io/github/issues-pr-closed-raw/Mono-94/mGarage?color=success&amp;label=closed%20PRs)
![Stars](https://img.shields.io/github/stars/Mono-94/mGarage?style=social)
![Forks](https://img.shields.io/github/forks/Mono-94/mGarage?style=social)
![Repo Size](https://img.shields.io/github/repo-size/Mono-94/mGarage)


# mGarage

* Create garages/impounds in-game or in the Config file
* Garage action: Target/TextUI
* Multilanguage
* Garages for jobs
* Vehicle search in the garage interface
* Custom vehicle garages
* Obtain an item key if necessary
* Mark vehicles outside the garage
* Share vehicles with companions
* Save vehicles with fake license plates (using the 'fakeplate' item from mVehicle)
* Impound with societies
* Functions to integrate the garage into any housing system
* Function to impound vehicles
* * The impound can establish a society account
* * Set a recovery date
* * Function to remove time from a plate vehicle

## Functions 

### OpenGarage
* **exports.mGarage:OpenGarage()**

```lua

exports.mGarage:OpenGarage({
    name = 'GARAGE ID/NAME',
    garagetype = 'garage',              
    intocar = true,                     
    carType = { 'automobile', 'bike' }, 
    spawnpos = {  vec4(0, 0, 0, 0) }
})
```
 
### SaveCar 
* **exports.mGarage:SaveCar()**
```lua
    exports.mGarage:SaveCar({
        name = 'GARAGE ID/NAME',
        garagetype = 'garage',              
        entity = vehicleEntity or false to getVehiclePedIsIn,            
        carType = { 'automobile', 'bike' }, 
    })
```

### impound Vehicle
```lua
    exports.mGarage:ImpoundVehicle({ 
        vehicle = Vehicle entity, 
        impoundName = 'Impound Name' 
    })
```

### Remove time for recovery vehicle
```lua
  -- open input to set plate 
    exports.mGarage:UnpoundVehicle()
  -- or direct plate
     exports.mGarage:UnpoundVehicle(plate)
```
### Example 

```lua
RegisterCommand('mGarage:opengarage', function(source, args, raw)
    local ped = PlayerPedId()
    local coords, heading = GetEntityCoords(ped), GetEntityHeading(ped)
    exports.mGarage:OpenGarage({
        name = 'Pillbox Hill',
        garagetype = 'garage',              
        intocar = true,                     
        carType = { 'automobile', 'bike' }, 
        spawnpos = {
            vec4(coords.x, coords.y, coords.z, heading),
        }
    })
end)

RegisterCommand('mGarage:savecar', function(source, args, raw)
    local ped = PlayerPedId()
    local vehicleEntity = GetVehiclePedIsIn(ped, false)
    if DoesEntityExist(vehicleEntity) then
        exports.mGarage:SaveCar({
            name = 'Pillbox Hill',
            garagetype = 'garage',             
            entity = vehicleEntity,             
            carType = { 'automobile', 'bike' }, 
        })
    else
        print('No Vehicle')
    end
end)

RegisterCommand('mGarage:impound', function(source, args, raw)
    local ped = PlayerPedId()
    local vehicleEntity = GetVehiclePedIsIn(ped, false)
    if DoesEntityExist(vehicleEntity) then
     ImpoundVehicle({
        vehicle = vehicleEntity,
        impoundName = 'Impound'
    })
    else
        print('No Vehicle')
    end
end)

RegisterCommand('mGarage:unpound', function(source, args, raw)
    UnpoundVehicle()
    -- or 
    --  UnpoundVehicle('MONO 420')
end)
```

![image](https://cdn.discordapp.com/attachments/1234840062181769378/1238255435358666884/307592b7-b7d1-40b4-b615-a1ac0d26c385.jpg?ex=663e9ebd&is=663d4d3d&hm=133b443e1a18490a0ef8669650068d0c546149d9bda930140539665202112e27&)
