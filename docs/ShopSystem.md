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

### Aumento o Descuento

aplico el multiplicador a la lista de precios, si no existe igualo a 1 o a su valor original

```luau
itemPrices.multiplier = priceMultiplier[itemId] or 1
```

<br>

### Cobrar el Dinero

espero respuesta positiva de "economy" sobre el cobro del item y valido:

```luau
local ok = economy.decrement(plr, itemPrices.economy)
if not ok then warn("err in decrement") return false end
```
