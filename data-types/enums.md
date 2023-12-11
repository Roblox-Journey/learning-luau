# Understanding Enums Data Type

## Introduction

> What are Enums ?

Enums, short for enumerations, provide a set **list of items**. Acess these enums through the **global object** called Enum.

For a full list of Enums and their items, see Enums in the API Reference.

## Get Items from Enums

To retrieve all items from an Enum, use the `GetEnumItems()` method on the desired enum.

> The example below illustrates how to apply `GetEnumItems()` to the `PartType` enum.

```lua
-- GetEnumItems() retrieves all items from the specified enum (PartType, in this case).
local partTypes = Enum.PartType:GetEnumItems()

-- Loop through each item in the enum and print it.
for _, enumItem in ipairs(partTypes) do
  print(enumItem)
end
```

> This code will output

```yaml
Enum.PartType.Ball
Enum.PartType.Block
Enum.PartType.Cylinder
```

## Enum Items

In Luau, an EnumItem is the data type used for items within enums. It possesses there straigh forward properties

- `Name` The name assigned to the EnumItem.
- `Value` The numerical index associated with the EnumItem.
- `EnumType` The parent Enum to which the EnumItem belongs.

Certain object properties are exclusively tied to specific enums. For instance, the `Shape` property of a `Part` object is a item of the `PartType` Enum.

> The following code snippet illustrates how to access and print the properties of the `PartType.Cylinder` EnumItem.

```lua
print(Enum.PartType.Cylinder.Name) --> Cylinder
print(Enum.PartType.Cylinder.Value) --> 2
print(Enum.PartType.Cylinder.EnumType) --> Part
```

> This example showcases how to retrieve and display essential information about an **EnumItem**, making it easier to work with and understand enums in Luau.

## Assigning Enum Items

To set an EnumItem as property value, use the full Enum declaration. Alternatively, use its Value or EnumType.

```lua
-- Create a new part
local part = Instance.new("Part")
part.Parent = workspace

-- By EnumItem (best practice)
part.Shape = Enum.PartType.Cylinder

-- By EnumItem Value
part.Shape = Enum.PartType.Cylinder.Value
part.Shape = 2 -- Equivalent to Enum value

-- By EnumItem Name
part.Shape = Enum.PartType.Cylinder.Name
part.Shape = "Cylinder" -- Equivalent to Enum name
```

> This concise guide illustrates different ways to assign **EnumItem values** to the `Shape` property of a `Part` in Luau.
