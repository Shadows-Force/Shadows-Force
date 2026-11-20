# Item System

### Funciones de Herencia

```luau
function module:equip()
	print("default equip")
end

function module:unequip()
	print("default unequip")
end

function module:use()
	print("default use")
end
```

<br>

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

<br>

## Codigo Completo:

```luau
function module.new(item: string, mode: mode, data: {[string]: any}, id: string, amount: number)
	local defaultData = getItemData(item)
	
	if not defaultData then warn("Item data not found") return false end
	
	local ok = validateData(data, defaultData)
	
	if not ok then data = defaultData end
	
	local methods = getItemMethods(item)
	
	if not methods then warn("methods not found") return false end
	
	local self = mode == "lite" and data or setmetatable(data, {__index = function(_, key)
		return methods[key] or module[key]
	end,})
	
	self.key = id or generateIdentity(data)
	self.amount = data.config.isMutable and 1 or amount or 1
	
	return self
end
```

<br>

## Funciones Auxiliares:

### SortTable

ordeno la tabla

```luau
local function SortTable(original)
	local sorted = {}
	local keys = {}

	-- Recolectamos las claves
	for key in pairs(original) do
		table.insert(keys, key)
	end

	-- Las ordenamos alfabéticamente
	table.sort(keys, function(a, b)
		return tostring(a) < tostring(b)
	end)

	-- Creamos la nueva tabla insertando en orden
	for _, key in ipairs(keys) do
		sorted[key] = type(original[key]) ~= "table" and original[key] or SortTable(original[key])
	end

	return sorted
end
```

<br>

### GetMethods

obtengo la tabla de metodos

```luau
local function getItemMethods(item: string)
	local ok, meth = pcall(function()
		return require(script.Methods[item])
	end)
	
	if not ok then
		return false
	end
	
	return meth
end
```

<br>

### GetData

obtengo la lista de data del item:

```luau
local function getItemData(item: string)
	local ok, data = pcall(function()
		local data = require(script.Data[item])
		return data
	end)
	
	if not ok then
		return false
	end
	
	return data
end
```

<br>

### validateData

Valido la Data Custom con la original

```luau
local function validateData(custom, default)
	if not custom then
		return false
	end
	
	for key, value in pairs(default) do
		if type(value) == "table" then
			if not validateData(custom[key], value) then
				return false
			end
		end
		
		if custom[key] == nil then
			return false
		end
	end
	
	if not validateData(default, custom) then
		return false
	end
	
	return true
end
```

<br>

### GenerateKey 

genero UID o Hash dependiendo si es mutable o no

```luau
local function generateIdentity(data)
	if data.config.isMutable then
		return HttpService:GenerateGUID(false)
	end
	
	return hashing.SHA2.SHA256(HttpService:JSONEncode(SortTable(data)))
end
```

<br>

<a href="ShopSystem.md#captura-de-pantalla">← Regresar</a>
