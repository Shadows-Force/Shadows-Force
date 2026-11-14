<h1 align="center">PlayerState</h1>

<p align="center">
  Librería para gestionar el estado y los datos de los jugadores en Roblox.
</p>

## Lado del servidor

Para gestionar la carga y el guardado de datos, utilizaremos un Script dentro de **ServerScriptService (SSS)**.

### Inicialización

Primero, Inicializo los datos del jugador utilizando la siguiente función:

```lua
PlayerState.Init()
```

Luego espero a que los datos del jugador se carguen completamente

```lua
PlayerState.ProfileLoaded:Connect(function(plr, data)
   -- codigo aqui --
)
```

Al final solo detecto cuando el jugador se va del juego para hacer las ultimas modificaciones antes de guardar

```lua
PlayerState.BeforeRelease:Connect(function(plr, data)
   -- ultimas modificaciones antes de guardar --
)
```

## Image

<p align="center">
  <img src="main/screenshots/DataSystem/DataManagerServer.png" width="48%">
</p>
