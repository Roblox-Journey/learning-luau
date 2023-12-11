# Understanding Tuplas Data Type

## Introduction

Tuples are a collection of values that are grouped together. They are similar to tables, but they have some important differences.
Tuples are **Immutable**, you cannot change their value once they are created. Additionally, tuples have a fixed length, meaning you cannot add or remove values from them.

## Creating Tuplas

Tuples can be created using parentheses `()`. For example, the following line of code creates a tupla with three values:

```lua
  local tuple = (1, "two", true)
```

## Accessing Values in a Tuple

To access a specific value in a tuple, you use the corresponding index. Remember that indices in Luau start from 1. Let's print the third element of our tuple.

```lua
local tuple = (1, "two", true)
print(tuple[3]) --> true
```

## Conclusion

Tuples in Luau provide an effective way to organize and access data. Whether using conventional or named tuples, you have a valuable tool at your disposal. Keep exploring the official documentation [Tuples](https://create.roblox.com/docs/luau/tuples).
