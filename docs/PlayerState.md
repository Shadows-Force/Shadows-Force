# PlayerState

<p>
  Librería para gestionar el estado y los datos de los jugadores en Roblox.
</p>

<br>

### Inicialización

inicio datos del jugador con:

```lua
PlayerState.Init()
```

<br>

atento cuando carguen:

```lua
PlayerState.ProfileLoaded:Connect(function(plr, data)
   -- código aquí --
end)
```

<br>

atento cuando se vaya:

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
