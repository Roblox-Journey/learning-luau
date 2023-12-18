# Understanding Variables in Luau

## Introduction

In programming, a variable is like a named container that stores information. The information, or value, can be a number, text, or other data types.

## Naming Variables

Choosing a good name for a variable is important.

- **Follow these rules**

  - Start with a letter and use letters, digits, and underscores.

    ```lua
    LETTERS   -- valid
    a1        -- valid
    var_name  -- valid
    _test     -- valid
    ```

    > Avoid **reserved words** and don't start with a **digit**.

    ```lua
    if        -- NOT valid
    25th      -- NOT valid
    ```

  - Be mindful of case sensitivity; `TestVar` and `TESTVAR` are different names.
  - Avoid names with all uppercase letters or underscores, as Luau may use them internally.

## Best Practices

Make your code readable

- **Spell out words fully for clarity**
- **Follow naming conventions**
  - Use `PascalCase` for class and enum-like objects.
  - Use `PascalCase` for Roblox APIs; camelCase is mostly deprecated.
  - Use `camelCase` for local variables, member values, and functions.
  - Use `LOUD_SNAKE_CASE` for local constants.

## Reserved Names

Certain words are reserved and can't be used as variable names in Luau.

```lua
and
for
or
break
function
repeat
do
if
return
else
in
then
elseif
local
true
end
nil
until
false
not
while
```

## Assigning Values

To create a variable and assign a value, use the `=` operator. Specify the variable on the left and the value on the right. If no value is given, it defaults to `nil`.

```lua
local nilVar
local x = 10
local word = "Hello"
local reference = workspace.Camera

print(nilVar)      -- nil
print(x)           -- 10
print(word)        -- Hello
print(reference)   -- Camera
```

## Assigning Values to Multiple Variables

Assign values to multiple variables in a single line. Extra variables get `nil`, and extra values are ignored.

```lua
local a, b, c = 1, 2, 3
local d, e, f = 4, 5 -- extra variable gets nil
local g, h = 7, 8, 9 -- extra value is ignored

print(a, b, c) -- 1, 2, 3
print(d, e, f) -- 4, 5, nil
print(g, h) -- 7, 8
```

## Changing Values

To update a variable's value, assign a new value to it.

```lua
local x, y = 10, 20
print(x, y) -- 10, 20

x = 1000
y = 2000
print(x, y) -- 1000, 2000
```

## Conclusion

In Luau, understanding variables is key to effective programming. They act as **containers for information**, holding values that can be manipulated. Follow **naming rules**, **best practices**, and be mindful of **reserved keywords**. Use the **assignment operator =** to create and update variables.

> Understanding these fundamental concepts will set a solid foundation for your Luau programming journey.
