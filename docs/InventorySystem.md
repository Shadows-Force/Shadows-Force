# Inventory System

<br>

## Añadir al Inventario

Añado y actualizo el Inventario

```luau
function module.add(plr, itemData)
	local path = string.format("inventory.index.%s", itemData.key)
	local data = PlayerState.GetPath(plr, path)
	if data then
		warn("Item already exists")
		return
	end
	return updateInventory(plr, "SetPath", itemData, itemData)
end
```

<br>

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

<br>

## Limpiar o Quitar Item

```luau
function module.remove(plr, key)
	clean(plr, key)
end
```

<br>

## Funciones Auxiliares

### UpdateInventory

Actualizo el inventario a las rutas necesarias

```luau
local function updateInventory(plr, method: Methods, item, data)
	local ok, err = pcall(function()
		PlayerState[method](plr, `inventory.index.{item.key}`, data)
		PlayerState[method](plr, `inventory.type.{item.type}.{item.key}`, data)
		PlayerState[method](plr, `inventory.rarity.{item.display.rarity}.{item.key}`, data)
	end)
	
	if not ok then
		warn(`[Inventory] Error updating inventory: {err}`)
	end
	
	return ok
end
```

<br>


### Clean

Limpo todas las rutas usadas por el Item

```luau
local function clean(plr, key)
	local item = PlayerState.GetPath(plr, `inventory.index.{key}`)
	if not item then return end
	updateInventory(plr, "SetPath", item, nil)
end
```

<br>

<a href="ShopSystem.md#captura-de-pantalla">← Regresar</a>
