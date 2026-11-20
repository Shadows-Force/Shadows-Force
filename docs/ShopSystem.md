# Shop System
sistema de compras de Items

<br>

### Precios

obtengo la lista de precios y valido:

```luau
local itemPrices = getItemPrice(itemId)
if not itemPrices then warn("Item price not found") return false end
```

<br>

### Item

Creo el Item de manera "Lite" y valido:

```luau
local itemData = Item.new(itemId, "lite")
if not itemData then warn("Item data not found") return false end
```

<br>

