<h1 align="center">PlayerState</h1>

<p align="center">
  Librería para gestionar el estado y los datos de los jugadores en Roblox.
</p>

## ¿Qué es PlayerState?

<p>La librería <strong>PlayerState</strong> permite gestionar la información de cada jugador, como sus datos, progreso, estadísticas y estados dentro del juego.</p>

## Lado del servidor

Para gestionar la carga y el guardado de datos, utilizaremos un Script dentro de **ServerScriptService (SSS)**.

### Inicialización

Primero, debemos inicializar la librería utilizando la siguiente función:

```lua
PlayerState.Init()
```

Esta función se encarga de iniciar el sistema de PlayerState para permitir la gestión de los datos de los jugadores.
