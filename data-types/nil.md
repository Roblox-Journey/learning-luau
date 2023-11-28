# Nil

## Introduction

> What is Nil ?

In Luau, `nil` serves as a representation of **non-existence** or **nothingness**. It stands apart from other values and data types, allowing you to effectively eliminate variables or remove values from tables. Notably, `nil` and `false` are the only values that do not evaluate to `true`.

Luau incorporates a **garbage collector** designed to remove data that scripts no longer access. To optimize performance, consider redefining large variables as `nil` in lengthy scripts when they are no longer necessary, facilitating their removal by the garbage collector.

## Basic Usage

```lua
local variableToDelete = 5
print(variableToDelete) -- 5

-- Set variable to nil for removal
variableToDelete = nil
print(variableToDelete) -- nil
```

> In Tables

```lua
local dictionaryTable = {
	Monday = 1,
	Tuesday = 2,
	Wednesday = 3
}

-- Access and output value of 'Tuesday' key
print(dictionaryTable.Tuesday) -- 2

-- Clear 'Tuesday' key using nil
dictionaryTable.Tuesday = nil

-- Output value of key again (now nil)
print(dictionaryTable.Tuesday) -- nil
```

## Removing Objects from View

You can utilize `nil` to clear properties of objects, effectively removing them from the experience. For instance, setting the `Parent` of an object to `nil` removes it from view. To reintroduce the object, simply reassign the `Parent`. The following example illustrates using `nil` to manage the visibility of a `Part`:

```lua
-- Create a new brick
local part = Instance.new("Part")

-- Parent new Part to the workspace, making it viewable
part.Parent = workspace
task.wait(1)

-- Remove the Part from view (not from memory)
part.Parent = nil
task.wait(1)

-- Reintroduce the Part to view
part.Parent = workspace
task.wait(1)

-- Remove the part from view again
part.Parent = nil

-- Clear part reference for garbage collector
part = nil
```

## Conclusion

By adopting these simple practices, you can harness the power of nil in Luau to manage variables, tables, and objects effectively.
