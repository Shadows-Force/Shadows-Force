# Economy System

### Funciones Set, Increment y Decrement

```luau
function module.set(plr:Player, currencies: {[string]: number})
	return update(plr, "SetPath", currencies)
end

function module.increment(plr, currencies)
	return update(plr, "Increment", currencies)
end

function module.decrement(plr, currencies)
	return update(plr, "Decrement", currencies)
end
```

<br>

## Funciones Auxiliares

```luau
local function update(plr, method: methods, currencies: {[string]: number})
	for currency, value in currencies do
		if not value or value < 0 then return end
		local money = PlayerState.GetPath(plr, `economy.{currency}`)
		if not money then return end
		if method == "Decrement" and (money - value) < 0 then return end
	end
	
	for currency, value in currencies do
		PlayerState[method](plr, `economy.{currency}`, value)
	end
	
	return true
end
```
