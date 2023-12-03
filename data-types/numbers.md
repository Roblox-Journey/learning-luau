# Understanding Number Data Types

## Introduction

> What are Numbers or Doubles ?

In Luau, numbers, also knows as doubles, represent [double-precision (64-bit) floating-point]() values. They cover a vast range, from `-1.7 * 10^308 to 1.7 * 10^308`, providing around 15 digits of precision, whether positive or negative.

## Signed and Unsigned

The sign of a number indicates its positivity or negativity. For instance, `1` is positive, and `-1` is negative. Remarkably, in Luau, `-0` is equivalent to `0`.

```lua
print(0 == -0) --> true
print(-0 > 1) --> false
print(-0 < 1) --> true
print(-0 > -1) --> true
print(-0 < -1) --> false
```

## Number Classifications

While Luau doesn't explicitly differentiate between integers and numbers, some API references make this distinction for specific use cases.

- `Float`

  - The **float** type represents numbers with decimals, like **1.5** or **-0.75**. It's good for mast uses, not as precise as some, but id saves memory.

- `Integers`

  - The **intergers** are whole numbers, like **5** or **-100**. They're good for counting and measuring things if a function needs an integerm it might round or giver an error if you try to use a non-whole number.

- `Int64`

  - The **Int64** is a big whole number type. It's often used for IDs in Roblox, like `Player.UserId`. Some Roblox functions, sunch as `MarketplaceService:PromptPurchase()` and `TeleportService:Teleport()` want these big numbers as inputs.

## Number Notation

In Roblox Lua, numbers are written in different ways:

- **Decimal (base-10)**

  - Write the digits normally with an optional decimal point.
  - For example: `7`, `1.25`, or `-22.5`.

- **Scientific Notation**

  - Write a dicimal number followed by `e` or `e+` and an integer.
  - For example: `12e3` is 12 x 10^3 (12.000).

- **Hexadecimal (base-16)**

  - Start the number with `0x`, followed by **0-9** or **A-F** (**case insensitive**).
  - For example: `0xF` is 15, and `0x3FC` is 1020.

- **Binary (base-2)**

  - Start the number with `Ob` followed by 0s or 1s.
  - For example: `Ob1100` represents 12 in decimal format.

> For long numbers, you can optionally use underscores to improve readability, **except** at the beginning. For example, `1_234_567` is the same as `1234567`, both of which are equivalent to 1,234,567.

## Operations

In Luau, you can do things with numbers using operators. There are two types:

- **[Logical And Relational Operators]()**

  - They help you compare and manipulate numbers.
  - Examples include comparingg if one number is greater than another or checking if two numbers are equal.

    ```lua
    local a = 5
    local b = 10

    print(a > b) --> false
    print(a == b) --> false
    ```

- **Mathematical Functions**

  - You can also use special **math** functions for more complex operations
  - Examples are `math.sqrt()` (square root) and `math.exp()` (exponential)

    ```lua
    local x = 25

    print(math.sqrt(x)) --> 5
    print(math.exp(x)) --> around 720.05
    ```

  - These functions are part of the [math]() library in Luau.

- **Bitwise Operations**

  - For even more advanced operations, you can use **bitwise operations** from the [bit32]() library.
  - These operations work on the individual bits of numbers.

    ```lua
    local m = 5
    local n = 3

    print(bit32.band(m, n)) --> 1 (bitwise AND)
    print(bit32.bord(m, n)) --> 7 (bitwise OR)
    ```

> These tools give you the power to play with numbers in different ways!

## Type Introspection

> Determining if a value is a number

In Luau, figuring out if something is a number is easy. You can use either `type(x)` or `typeof(x)`, and both will tell you if `x` is a number. They will say say **number** if it is.

```lua
  local testInt = 5
  local testDecimal = 9.12761656
  local testString = "Hello"

  -- Using type()
  print(type(testInt)) --> number
  print(type(testDecimal)) --> number
  print(type(testString)) --> string

  -- Using typeof()
  print(typeof(testInt)) --> number
  print(typeof(testDecimal)) --> number
  print(typeof(testString)) --> string
```

> So, if you ever wonder whether a value like `testInt`, `testDecimal`, or `testString` is a number, just use one of these methods, and they'll give you a clear answer.

## Rounding Functions

> How to Do Number Rounding Easily?

You can easily round numbers using three functions: `math.floor()`, `math.ceil()`, and `math.modf()`.

- **Determinate if a Number is an Integer**

  - To check if a number `x` is an integer, you can use the expression `math.floor(x) == x`

- **Round a Number Down**

  - To round a number down, simply use `math.floor()`.
  - It returns the largest integer less than or equal to the given number.

    ```lua
    print(math.floor(3.3)) --> 3
    print(math.floor(-3.3)) --> 4
    ```

- **Round a Number Up**

  - For rouding a number up to the nearest integer, use `math.ceil()`.
  - This function returns the smallest integer greater than or equal to the provided number.

    ```lua
    print(math.ceil(3.3)) --> 4
    print(math.ceil(-3.3)) --> -3
    ```

- **Round a Number Towards Zero**
  - When you want to round a number towards zero and also get the fractional difference, use `math.modf()`.
  - It returns two values: the **integer** part and the **fractional** part.
    ```lua
    print(math.modf(3.3)) --> 3 0.3
    print(math.modf(-3.3)) --> -3 -0.3
    ```

> These simple functions make rouding number a breeze in Luau!
