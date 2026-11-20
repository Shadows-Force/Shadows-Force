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

<br>

### Creacion del Item

Dependiendo de la peticion se crea la metatabla o solo una tabla para casos de guardado

```luau
local self = mode == "lite" and data or setmetatable(data, {__index = function(_, key)
		return methods[key] or module[key]
	end,})
	
	self.key = id or generateIdentity(data)
	self.amount = data.config.isMutable and 1 or amount or 1
	
	return self
```
