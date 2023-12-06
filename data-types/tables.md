# Understandint Tables Data type

## Introduction

> What are Tables ?

Tables are versatile data structures caplable of storing various values of any **non-nil** type, such as booleans, numbers, strings, functions, and even other tables.

> Contructing tables is easy com curly braces (`{}`):

```lua
  -- Create an empty table assigned to the variable "myTable"
  local myTable = {}
  print(myTable) -- {}
```

Tables in Luau can function as **arrays** or **dictionaries**. Arays use an ordened list of numbers indices, while dictionaries can have indices of numbers, strings, or objects.

> For more details and functions to work with tables, refer to the [table](https://create.roblox.com/docs/pt-br/reference/engine/libraries/table) library in Luau.

## Arrays

An arrays is like a list of things in order. You can use it to keep a bunch of information organized, like a list of players with special powers.

- **Creating Arrays**

  - Making an array is easy. Just put your items inside **curly braces ( {} )** and separate them with **commas**.

    ```lua
    local testArray = {"A string", 1234, 3.14159, workspace.Camera}
    print(testArray)
    ```

- **Reading from Arrays**

  - To get something from the array, use **square brackets ( [] )** with the indice of the item inside.

    ```lua
      local testArray = {"A string", 1234, 3.14159, workspace.Camera}
      print(testArray[1]) --> A string
      print(testArray[2]) --> 1234
      print(testArray[3]) --> 3.14159
      print(testArray[4]) --> Camera
    ```

    > ⚠️ Remember, Luau starts counting at `1`, not `0`!

- **Writing to Arrays**

  - To change something in the array, use the **square brackets ( [] )** with the indice of the item and put `=` and new value.

  ```lua
      local testArray = {"A string", 3.14159, workspace.Camera}
      testArray[2] = 1234
      testArray[4] = "New tring"

      print(testArray[2]) --> 1234
      print(testArray[4]) --> New string
  ```

- **Interating over Arrays**

  - If you want go to through each item in the array, use a loop. You can also use a loop that count from **1** to the **length of the array**

    ```lua
    local testArray = {"A string", 3.14159, workspace.Camera, "New string"}

    -- Loop 1 using general interation
    -- ipairs(testArray) returns index-value pairs for each item in the array.
    -- index is the index of the item.
    -- value is the value of the item.
    for index, value in ipairs(testArray) do
      print(index, value)
    end

    -- Loop 2 using array length operator
    -- #testArray returns the length of the array.
    -- index is the loop control variable, ranging from 1 to the length of the array.
    for index = 1, #testArray do
      print(index, testArray[index])
    end
    ```

    1. **General Iteration Loop**

       - In the first example, we use a general loop with the `ipairs()` function. This is useful when you want to go through all items in the array in the order they appear, without worrying about specific indices.

         > This loop goes through the array and prints the **index** and **value** of each item. In this case, it will print.

    2. **Loop using the Array Length Operator**

       - The second example uses a loop that counts from **1** to **the length of the array**. This is done using the `#` operator to get the length of the array.

         > This Loop also goes through the array and prints the **index** and **value** of each item. The output will be the same as the general interation loop.

  - Both loops are effective ways to traverse an array; choose the one that best fits your situation. The general interation loop is useful whe you need both indices and values, while the loop useing the array length operator is handy when you only need values and don't care about specific indices.

- **Inserting Items**

  - Inserting items into arrays is a crucial operation when you want to add new elements to your array. Luau provide two common methods for inserting items: using [`table.insert()`](https://create.roblox.com/docs/pt-br/reference/engine/libraries/table#insert) and using a convenient syntax with **square brackets ( [] )**.

    ```lua
    local testArray = {"A string", 3.14159}

    -- table.insert(testArray, "New string") adds "New string" to the end of testArray.
    table.insert(testArray, "New string")

    -- testArray[#testArray + 1] = "Another new string" is a convenient way to add "Another new string" to the end of the array.
    testArray[#testArray + 1] = "Another new string"

    print(testArray[3]) --> New string
    print(testArray[4]) --> Another new string
    ```

  - **Inserting at a Specific Position**

    - If you want to insert an item at a specific position in the array, you can provide a indice value as the second argument to `table.insert()`. This shifts existing items to higher indices.

      ```lua
      local testArray = {"First item", "Next item"}

      -- table.insert(testArray, 2, "NEW ITEM #2") inserts "NEW ITEM #2" at the second position in testArray.
      table.insert(testArray, 2, "NEW ITEM #2")

      print(testArray[1]) --> First item
      print(testArray[2]) --> NEW ITEM #2
      print(testArray[3]) --> Next item
      ```

  - These insertion methods are flexible and allow you to manage your arrays efficiently, whether you're adding items to the end or inserting them at specific positions. Choose the method that suits your needs best!

- **Removing Items**

  - To take something out, use [`table.remove()`](https://create.roblox.com/docs/pt-br/reference/engine/libraries/table#remove). It removes the item at the position you specify and moves the others back.

    ```lua
    local testArray = {"First item", "Next item", "Last item"}

    -- table.remove(testArray, 2) This line removes the item at position 2 from the array ("Next item")
    table.remove(testArray, 2)

    print(testArray[1]) --> First item
    print(testArray[2]) --> Last item
    ```

## Dictionaries

Dictionaries, an upgrade from arrays, hold key-value pairs, where keys can be numbers, strings, or objects.

- **Creating Dictionaries**

  - Create dictionary with **key-value** pairs using **curly braces ( {} )**.

    ```lua
    local testDictionary = {
      FruitName = "Lemon",
      FruitColor = "Yellow",
      Sour = true
    }
    ```

    - **Keys** can be numbers, strings, or objects. For object key, use **square brackets ( [] )**

      ```lua
      local part = Instance.new("Part")

      local testDictionary = {
        PartType = "Block",
        [part] = true
      }
      ```

  - **Reading from Dictionaries**

    - To read from dictionary, use **square backets ( [] )** and specify the key

      ```lua
        local part = Instance.new("Part")

        local testDictionary = {
          PartType = "Block",
          [part] = true
        }

        print(testDictionary["PartType"]) --> Block
        print(testDictionary[part]) --> true
      ```

  - **Writing to Dictionaries**

    - Define or rewrite a key's value, use the **square brackets ( [] )** with the key of the item and put `=` and new value.

      ```lua
        local testDictionary = {
          FruitName = "Lemon",
          Suor = true
        }

        testDictionary[FruitName] = "Cherry"
        testDictionary[Suor] = false
        testDictionary[FruitCount] = 10


        print(testDictionary[FruitName]) --> Cherry
        print(testDictionary[Suor]) --> false
        print(testDictionary[FruitCount]) = 10
      ```

  - **Iterating over Dictionaries**

    - Iterating over dictionaries allows you to access and process each key-value pair. Use the `pairs()` function in a **for loop** to traverse the dictionary.

      ```lua
      local testDictionary = {
        FruitName = "Lemon",
        FruitColor = "Yellow",
        Sour = true
      }

      for key, value in pairs(testDictionary) do
        print(key, value)
      end
      ```

      In the example above, `key` represents the key of the dictionary, and `value` represents the value associated with that key. The for loop iterates over each key-value pair in the `testDictionary`.

      > **Output Result**

      ```yaml
      FruitName Lemon
      Sour true
      FruitColor Yellow
      ```

      Note that unlike using `ipairs()` on an array, using `pairs()` on a dictionary doesn't guarantee that items will be returned in the same order as they appear in the dictionary. **The order is not guaranteed in Lua dictionaries**.

      > This technique is useful for performing operations on all elements of a dictionary, such as display, processing, or data manipulation.

  - **Removing Key-Value Pairs**

    - To remove or delete a key-value pair from a dictionary, you set the value associated with the `key` to `nil`.

      ```lua
      local exampleDictionary = {
        FruitName = "Lemon",
        FruitColor = "Yellow",
        Sour = true
      }

      -- Removing the key-value pair "Sour"
      exampleDictionary["Sour"] = nil

      -- Iterating over the modified dictionary
      for key, value in pairs(exampleDictionary) do
        print(key, value)
      end
      ```

      In this example, the line `exampleDictionary["Sour"] = nil` removes the key-value pair where the key is **"Sour"** The result of the subsequent iteration shows that the pair has been removed as it's no longer displayed in the console:

      > **Output Result**

      ```yaml
      FruitName Lemon
      FruitColor Yellow
      ```

      > By setting the value associated with a `key` to `nil`, you effectively eliminate that key-value pair from the dictionary. This can be useful when you need to dynamically adjust the content of the dictionary during program execution.

## Tables as Reference

When you assign a table to a new variable, Luau **doesn't make a copy**. Instead, the new variable becomes a reference to the original table. Any changes to the original table reflect in all references.

```lua
local originalArray = {10, 20}

-- Assign the table to a new variable
local arrayReference = originalArray

-- Both show the same values
print("Original:", originalArray[1], originalArray[2])
print("Reference:", arrayReference[1], arrayReference[2])

-- Change values in the original table
originalArray[1] = 1000
originalArray[2] = 2000

-- Now both references reflect the changes
print("Reference:", arrayReference[1], arrayReference[2])
```

> **Resulting Output**

```yaml
Original: 10 20
Reference: 10 20
Reference: 1000 2000
```

## Cloning Tables

- **Shallow Clone**

  - A shallow clone refers to creating a new table that is a copy of the original table, but it only copies the immediate values of the original table, not any nested tables within it. In Luau, you can achieve a shallow clone using the [`table.clone()`](https://create.roblox.com/docs/pt-br/reference/engine/libraries/table#clone) method.

    > Here's a breakdown

    ```lua
      local original = {
        key = "value",
        engine = "Roblox",
        playerID = 505306092
      }

      local clone = table.clone(original)
    ```

    In this example, `original` is a table with three key-value pairs. When you use `table.clone(original)`, it creates a new table `clone` that has the same key-value pairs as `original`. Importantly, if any of the values in the original table are themselves tables, the `table.clone()` method won't create separate copies of those nested tables; it will simply copy references to them. This means changes made to nested tables within the ` ` will also affect the original and vice versa.

    > In summary, a shallow clone captures the structure of the original table and copies its immediate contents. If the original table has nested tables, a shallow clone maintains references to those nested tables rather than creating new copies.

- **Deep Clone**

  - In Luau, a deep clone involves creating a copy of a table that not only duplicates the top-level elements but also ensures that any nested tables within the original table are duplicated as well. This is essential when dealing with complex data structures containing multiple layers of tables.

    > Here's a breakdown of the code for creating a deep clone

    ```lua
      local function deepCopy(original)
        local copy = {}
        for k, v in pairs(original) do
          if type(v) == "table" then
            v = deepCopy(v)  -- Recursively deep copy nested tables
          end
          copy[k] = v
        end
        return copy
      end
    ```

    > **Function Explanation**

    1. The `deepCopy` function takes a table (`original`) as input.
    2. It initializes an empty table (`copy`) to store the cloned elements.
    3. It then iterates over the key-value pairs of the original table using `pairs`.
    4. For each key-value pair, it checks if the value (`v`) is itself a table. If it is, the function recursively calls itself to deep copy the nested table.
    5. The key-value pair is then added to the `copy` table.
    6. The function returns the cloned table (`copy`).

    > Now, let's consider an example table with nested structures:

    ```lua
      local original = {
        key = "value",
        playerInfo = {
          playerID = 505306092,
          playerName = "PlayerName"
        },
        otherInfo = {
          {
            {1, 3, 5, 7, 9}
          }
        }
      }

      local clone = deepCopy(original)
    ```

    In this example, `clone` is a deep clone of the `original` table. It not only replicates the top-level keys and values but also ensures that any nested tables within `playerInfo` and `otherInfo` are also cloned. This guarantees that modifications to the cloned table won't affect the original and vice versa, providing a true independent duplicate.

    > Deep cloning is particularly useful when working with intricate data structures, such as configurations, where preserving the entire hierarchy is crucial.
