# PlayerState

<p>
  Librería para gestionar el estado y los datos de los jugadores en Roblox.
</p>

<br>

### Inicialización

Primero, inicializamos los datos del jugador utilizando la siguiente función:

```lua
PlayerState.Init()
```

<br>

Luego, esperamos a que los datos del jugador se carguen completamente:

```lua
PlayerState.ProfileLoaded:Connect(function(plr, data)
   -- código aquí --
end)
```

<br>

Finalmente, detectamos cuándo el jugador abandona el juego para realizar las últimas modificaciones antes de guardar sus datos:

```lua
PlayerState.BeforeRelease:Connect(function(plr, data)
   -- últimas modificaciones antes de guardar --
end)
```

<br>

## Capturas de pantalla

<p align="center">
  <img src="../screenshots/DataSystem/DataManagerServer.png" width="80%">
</p>

<br>

<a href="../README.md#proyectos">← Regresar</a>
