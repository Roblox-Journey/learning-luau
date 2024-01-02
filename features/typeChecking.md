# Understanding Type Checking in Luau

## Introduction

Luau, the scripting language used in Roblox game development, empowers developers with a gradual type system. This system enhances code quality by providing warnings, errors, and suggestions through type annotations and inference.

- ### Defining Your Own Types

  - In Luau, you can define custom types using the `type` keyword.

    > **Let's take an example**

    ```lua
    type Vector2 = { x: number, y: number }
    ```

    > Here, we've defined a type called `Vector2` that represents a 2D vector with `x` and `y` components, both of type `number`. This helps make your code more self-explanatory and reduces the chances of type-related errors.

- ### Inference Modes

  - Luau offers three type inference modes, allowing you to control the strictness of type checking. These modes are set at the beginning of your script using comments.

    > **Let's explore them**

    - `--!nocheck`: Disables type checking altogether. This can be useful in specific scenarios where you want to skip type validation temporarily.

    - `--!nonstrict`: This is the default mode for all scripts. In this mode, Luau checks variable types only if they are explicitly annotated. It strikes a balance between flexibility and type safety.

    - `--!strict`: Asserts all types based on either inferred or explicitly annotated types. This mode is the most rigorous, ensuring comprehensive type checking throughout your code.

- ### Choosing the Right Mode

  - Selecting the appropriate inference mode depends on your project's needs. If you're starting with Luau, sticking to the default `--!nonstrict` mode is a sensible choice. It provides a good balance between flexibility and catching potential errors.

- ### Visualizing Type Mismatches

  - Luau makes it easy to identify type mismatches. In the **[Script Editor](https://create.roblox.com/docs/studio/script-editor)**, any discrepancies are highlighted, and warnings are surfaced in the **[Script Analysis](https://create.roblox.com/docs/studio/script-editor#script-analysis)** window. This visual feedback is invaluable in catching and rectifying potential issues before they impact your game.

## Types

A type annotation can be defined using the `:` operator after a local variable, followed by a type definition. By default, in `nonstrict` mode, all variables are assigned the type `any`.

> **Example**

```lua
local foo: string = "bar"
local x: number = 5
```

There are four **primitive types** that can be used in an annotation:

- `nil` - no value
- `boolean` - true or false
- `number` - a numeric value
- `string` - text

Within Roblox, all classes, data types, and enums have their own types that you can check against:

> **Example**

```lua
local somePart: Part = Instance.new("Part")
local brickColor: BrickColor = somePart.BrickColor
local material: Enum.Material = somePart.Material
```

To make a type optional, use a `?` at the end of the annotation:

```lua
local foo: string? = nil
```

This will allow the variable to be either the specified type (in this case `string`) or `nil`.

### Literal Types

You can also specify the exact value that a string or boolean can have by using literal types

```lua
local alwaysHelloWorld: "Hello world!" = "Hello world!"
alwaysHelloWorld = "Just hello!" -- Type error: Type '"Just hello!"' could not be converted into '"Hello world!"'

local alwaysTrue: true = false -- Type error: Type 'false' could not be converted into 'true'
```

### Type Casts

Sometimes, you might need to assist the typechecker by explicitly casting a value to a different type with the `::` operator

```lua
local myNumber = 1
local myString: string

myString = myNumber -- Not OK; type conversion error
myString = myNumber :: any -- OK; all expressions can be cast to 'any'
local myFlag = myNumber :: boolean -- Not OK; types are unrelated
```

## Function Typing

### Adding Types to Parameters

- Consider the following addition function:

  ```lua
  local function add(x, y)
    return x + y
  end
  ```

  This function works correctly with `numbers` but may produce errors if given `strings`. To prevent this, add types to the parameters:

  ```lua
  local function add(x: number, y: number)
    return x + y
  end
  ```

  Now, Luau knows that this function only accepts `numbers` and will issue a warning if given anything else:

  ```lua
  add(5, 10)
  add(5, "foo")  -- Type error: string could not be converted into number
  ```

### Defining the Return Type

- To define the return type, use the `:` operator at the end of the function definition:

  ```lua
  local function add(x: number, y: number): number
  ```

  This indicates that the function returns a `number`.

> **Returning Multiple Types**

- If a function returns multiple types, enclose them in parentheses:

  ```lua
  local function FindSource(script: BaseScript, pattern: string): (string, number)
    return "Result", 42  -- Type errors if not followed
  end
  ```

  Here, FindSource returns a `string` and a `number`.

### Defining Functional Types

- Functional types are defined using the syntax `(in) -> out`. In the case of the previous functions:

  ```lua
  type add = (x: number, y: number) -> number
  type FindSource = (script: BaseScript, pattern: string) -> (string, number)
  ```

  Now, you can use add and `FindSource` as types in other parts of your code, promoting clarity and preventing potential type errors.

## Table Types

Luau does not have a `table` type, instead, table types are defined using `{}` syntax. One way of defining tables is using the `{type}` syntax, which defines a list type.

```lua
local numbers: {number} = {1, 2, 3, 4, 5}
local characterParts: {Instance} = LocalPlayer.Character:GetChildren()
```

Define index types using `{[indexType]: valueType}`:

```lua
local numberList: {[string]: number} = {
  Foo = 1,
  Baz = 10
}

numberList["bar"] = true -- Type error: boolean can't convert to number
```

Tables can also have explicit string indices defined in a type.

```lua
type Car = {
  Speed: number,
  Drive: (Car) -> ()
}

local taxi: Car = {Speed = 30, Drive = drive}

function drive(car)
-- Always go the speed limit
end
```

## Variadics

In programming, the ability to handle a variable number of arguments in a function is extremely useful. Luau, the robust scripting language, supports this functionality through the concept of "Variadics." Let's explore this with clarity and examples.

### Basic Variadic Function

Let's start with a function that sums an arbitrary amount of numbers:

```lua
local function addLotsOfNumbers(...)
  local sum = 0

  for _, v in {...} do
    sum += v
  end

  return sum
end

print(addLotsOfNumbers(1, 2, 3, 4, 5))  -- Output: 15
print(addLotsOfNumbers(1, 2, "car", 4, 5))  -- Error: Attempt to add string to number
```

Here, `...` represents a variable number of arguments. The function iterates through these arguments, summing them up and returning the result.

### Typing Variadic

When using variadics, inadvertent type errors can occur. In the above example, an attempt to add a string to numbers doesn't raise a type warning. However, we can rectify this by assigning a type to the variable arguments:

```lua
local function addLotsOfNumbers(...: number)

print(addLotsOfNumbers(1, 2, "car", 4, 5))  -- Type error: string could not be converted into number
```

Now, attempting to add a `string` results in a type error.

### Defining a custom Type for Variadics

However, when attempting to define a function type for variadics, the conventional method doesn't work. This is because the `:` operator is unsuitable for this situation. Instead, we use the `...type` syntax:

```lua
type addLotsOfNumbers = (...number) -> number
```

This type declaration specifies that the `addLotsOfNumbers` function accepts a variable number of arguments of type `number` and returns a `number`.

## Unions and Intersections

### Union of Types

- Type union is used when a value can be of more than one type. In the example below, we create the `numberOrString` type, which can be either a `number` or a `string`:

  ```lua
  type numberOrString = number | string

  local numString1: numberOrString = 42  -- Valid
  local numString2: numberOrString = "hello"  -- Valid
  local numString3: numberOrString = true  -- Type error
  ```

  In the example, `numString1` and `numString2` are assigned correctly, while `numString3` generates a type error because a `boolean` is not part of the defined type union.

### Intersection of Types

- Type intersection is used when a value needs to simultaneously satisfy the conditions of two types. Here, we create the `type1` and `type2` types, and then combine them into `type1and2`:

  ```lua
  type type1 = {foo: string}
  type type2 = {bar: number}
  type type1and2 = type1 & type2

  local obj: type1and2 = {foo = "hello", bar = 1}  -- Valid
  local objInvalid: type1and2 = {foo = "hello"}  -- Type error
  ```

  In the example, `obj` is assigned correctly because it contains the properties of both `type1` and `type2`, while `objInvalid` results in a type error because it lacks the `bar` property.

## Defining an Inferred Type

You can use the `typeof` function in a type definition for inferred types:

```lua
type Car = typeof({
	Speed = 0,
	Wheels = 4
})  --> Car: {Speed: number, Wheels: number}
```

One way to use `typeof` is to define a metatable type using `setmetatable` inside the `typeof` function:

```lua
type Vector = typeof(setmetatable({}::{
	x: number,
	y: number
}, {}::{
	__add: (Vector, Vector|number) -> Vector
}))

-- Vector + Vector would return a Vector type
```

## Generics

Generics in Lua are a powerful tool for creating flexible and reusable code by allowing you to define parameters for types. Let's break down the concept with a practical example.

> Consider a simple State object without generics:

```lua
local State = {
  Key = "TimesClicked",
  Value = 0
}
```

In this case, the type for `State` is explicitly defined:

```lua
type State = {
  Key: string,
  Value: number
}
```

> Now, let's introduce generics to make the Value type dynamic:

```lua
type GenericType<T> = T
```

Here, `<T>` signifies a type that can be substituted with any other type. Think of it as a placeholder that allows flexibility. Now, let's apply this to a List:

```lua
type List<T> = {T}

local Names: List<string> = {"Bob", "Dan", "Mary"}  -- Type becomes {string}
local Fibonacci: List<number> = {1, 1, 2, 3, 5, 8, 13}  -- Type becomes {number}
```

In this example, `List<T>` allows you to create a list with a specific type (`string` or `number`). The generic type `<T>` is replaced with the actual type when you use it.

Generics can also handle multiple substitutions inside the brackets:

```lua
  type Map<K, V> = {[K]: V}
```

Now, let's apply this to our `State` object to make the Value type dynamic:

```lua
type State<T> = {
  Key: string,
  Value: T
}
```

By using `State<T>`, you can customize the type of Value based on what you need. For instance:

```lua
local ClickCount: State<number> = {Key = "TimesClicked", Value = 42}  -- Type becomes {number}
local UserName: State<string> = {Key = "Username", Value = "John"}  -- Type becomes {string}
```

### Function Generics

Functions can also use generics. The State example infers the value of `T` from the function's incoming arguments.

To define a generic function, add a `<>` to the function name:

```lua
local function State<T>(key: string, value: T): State<T>
  return {
    Key = key,
    Value = value
  }
end

local Activated = State("Activated", false) -- State<boolean>
local TimesClicked = State("TimesClicked", 0) -- State<number>
```

In summary, generics provide a flexible way to write code that can adapt to different data types. They enhance code reusability and make your Lua programs more adaptable and scalable.

## Type Exports

To make it so a type can be used outside of a **[ModuleScript](https://create.roblox.com/docs/reference/engine/classes/ModuleScript)**, use the `export` keyword:

> Types Module in ReplicatedStorage

```lua
export type Cat = {
  Name: string,
  Meow: (Cat) -> ()
}
```

> Script Using the Types Module

```lua
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Types = require(ReplicatedStorage.Types)

local newCat: Types.Cat = {
  Name = "metatablecat",
  Meow = function(self)
    print(`{self.Name} said meow`)
  end
}

newCat:Meow()
```

## Conclusion

Type checking, or type verification, plays a fundamental role in preventing errors related to data manipulation. By defining and using types explicitly, as in the examples we have created, we ensure consistency and clarity in the code. This not only helps detect errors earlier but also makes the code more understandable for other developers. In summary, type checking is an essential practice to strengthen the reliability and readability of the code.
