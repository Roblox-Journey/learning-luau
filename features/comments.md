# Understanding Comments in Luau

## Introduction

Comments are a way to include human-readable explanations in your Luau code without affecting its runtime behavior. The Luau parser ignores comments, making them useful for documentation and in-line notes.

> Single-line Comments

In Luau, single-line comments are defined with a double hyphen `--`. They can be placed anywhere outside a string and extend to the end of the line.

```lua
-- This is a single-line comment
local variable = "Hello, Luau!"
```

Use single-line comments for brief in-line notes. If your comment spans multiple lines, it's recommended to use multiple single-line comments.

```lua
-- This is the first line of a multi-line comment
-- Here's the second line of the comment
```

## Block Comments

You can define **multiline block comments** with double hyphens and double brackets `--[[]]`. Use block comments for documenting items:

- Use a block comment at the top of files to describe their purpose.
- Use a block comment before functions or objects to describe their intent.

```lua
--[[
  Shuts off the cosmic moon ray immediately.

  Should only be called within 15 minutes of midnight Mountain Standard
  Time, or the cosmic moon ray may be damaged.
]]
local function stopCosmicMoonRay()
end
```

> If necessary, you can nest multiple brackets inside a block comment using the same number of equal signs in both the beginning and ending bracket:

```lua
--[=[
In-depth detail about cosmic moon ray: [[[TOP SECRET]]]
]=]
```

## TODO Comments

Roblox Studio supports special **TODO** comments. Studio bolds any text following TODO (until broken by a space):

```lua
-- TODO: Finish the function below so that it actually does what its name implies.
local function stopWorldFromBlowingUp()
end
```

> Use TODO comments to keep track of and communicate issues within your code.

## Conclusion

Comments in code are beneficial for describing and annotating information. However, using them excessively can clutter your code, so exercise caution. When adding comments, strive for conciseness and focus on essential information to ensure that your code remains clear and readable.

> Remember: the quality of comments is as important as their presence.
