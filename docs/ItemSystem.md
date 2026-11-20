# Item System

### Crear Item

Obtengo los Datos por defecto del Item y valido:

```luau
local defaultData = getItemData(item)
if not defaultData then warn("Item data not found") return false end
```

<br>

### Comprobar Datos

Hago una comparacion para comprobar que los datos pasados concuerden con la estructura de la data del Item por defecto, y valido:

```luau
local ok = validateData(data, defaultData)
if not ok then data = defaultData end
```

<br>

### Metodos

Obtengo los metodos del item y valido

```luau
local methods = getItemMethods(item)	
if not methods then warn("methods not found") return false end
```

