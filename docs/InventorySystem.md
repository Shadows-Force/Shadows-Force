# Inventory System

<br>

## Añadir al Inventario

obtengo la ruta y valido si el Item existe

```luau
local path = string.format("inventory.index.%s", itemData.key)
	local data = PlayerState.GetPath(plr, path)
	if data then
		warn("Item already exists")
		return
	end
```

<br>

### Actualizar Inventario

Actualizo el inventario del jugador para todas las rutas necesarias y devuelvo el resultado de la operacion

```luau
return updateInventory(plr, "SetPath", itemData, itemData)
```

## Decrementar

Decremento "amount" a un objeto "Apilable" (por defecto todos los items tienen "amount" pero de momento no hay funcion para aumentar la cantidad apilada de un objeto "no mutable")

```luau
function module.decrease(plr, key, amount)
	local path = string.format("inventory.index.%s", key)
	local itemData = PlayerState.GetPath(plr, path)
	if not itemData then return end
	
	if itemData.amount - amount <= 0 then
		clean(plr, key)
		return
	end
	
	PlayerState.Decrement(plr, `{path}.amount`, amount)
end
```

