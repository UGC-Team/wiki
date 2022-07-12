- [Formatting](#formatting)
    - [Indentation](#indentation)
- [Naming](#naming)
    - [Function naming](#function-naming)
    - [Value and object variable naming](#value-and-object-variable-naming)
    - [Constants naming](#constants-naming)
    - [Module/package naming](#modulepackage-naming)
    - [Class names](#class-names)
- [Commenting](#commenting)
    - [Simple commenting](#simple-commenting)
    - [Function commenting](#function-commenting)
    - [Class commenting](#class-commenting)
    - [Variable commenting](#variable-commenting)

# Formatting

### Indentation

* Use 4 spaces per indentation level. 
* Eg:
```lua
for i,v in ipairs(t) do
        if type(v) == "string" then
            print(v)
        end
    end
```

# Naming

### Function naming

* Using mixedCase: differs from CapitalizedWords by initial lowercase character. 
* Eg: 
```lua
function onUpdate()
    -- Update function for objects
end

function Lib.loadCsvFile(filePath, tRow, indexNumber)
    -- Load config from CSV file
end
```

### Value and object variable naming 

* Variables holding values or objects are typically lowercase and short (e.g. color, part, entity). 
* Using mixedCase: differs from CapitalizedWords by initial lowercase character. 
* Eg:
```lua
local allRows = {}
local rowValue = 123
```

### Constants naming 

* Constants are often given in ALL_CAPS.
```lua
local GAME_LOGIC_FPS = 12
local CONST_1 = "ABC"
local CONST_2 = 456
```

### Module/package naming 

* Module names are often short and lowercase, with "`_`" between words.
* Eg:

```lua
base.common
base.data
game.manager
game.network
```

### Class names 

* Using CamelCase. Start with a capital letter, words are separated by capital letters.
* Eg:
```lua
local EntityManager = class("EntityManager")
local NetworkManager = class("NetworkManager")
local PlayerController = class("PlayerController")
```

# Commenting

### Simple commenting

* Use a space after `--`.
* Eg:
```lua
return nil  -- not found    (suggested)
return nil  --not found     (discouraged)
```

### Function commenting

* Full format:
```lua
---@param param_name MY_TYPE[|other_type] [@comment]
---@return MY_TYPE[|OTHER_TYPE] [@comment]
---@private|@public|@protected
```
* Eg:
```lua
---Update function
---@param tick int
---@return int
---@private
function MyClass:onUpdate(name, handler)
    -- Update handler

    return 1
end
```

### Class commenting

* Full format:
```lua
--@class MY_CLASS[:PARENT_CLASS] [@comment]
```
* Example:
```lua
---@class Car : Transport @define class Car extends Transport
---@field public objID int
---@field private _var1 int
---@field onUpdate fun(self: Car): void
local cls = class()

function cls:test()
end
```

### Variable commenting

* Full format:
  * Single variable:
    ```lua
    ---@type MY_TYPE[|OTHER_TYPE] [@comment]
    ```
  * Array type:
    ```lua
    ---@type MY_TYPE[]
    ```
  * Table type:
    ```lua
    ---@type table<KEY_TYPE, VALUE_TYPE>
    ```
* Eg:
  * Local variable:
    ```lua
    ---@type Car @instance of car
    local car1 = {}
    ```
  * Properties:
    ```lua
    local obj = {}
    ---@type Car @property type
    obj.car = getCar()
    ```
  * Array type:
    ```lua
    ---@type Car[]
    local list = {}
    ```
  * Table type:
    ```lua
    ---@type table<string, Car>
    local dict = {}
    ```
