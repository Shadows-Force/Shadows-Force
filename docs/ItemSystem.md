# Item System

## Crear Item

Obtengo los Datos por defecto del Item

```luau
local defaultData = getItemData(item)
if not defaultData then warn("Item data not found") return false end
```
