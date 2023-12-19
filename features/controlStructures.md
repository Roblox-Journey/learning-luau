# Understanding Control Structures in Luau

## Introduction

Control structures play a crucial role in managing the flow of Luau code execution.

> Let's explore the four main types of control structures in Luau with simplicity and clarity.

- **if then else**
  - An `if-then-else` statement allows you to execute code only if a specified condition is `true`. The code inside the block is executed, and if the condition is `false`, an alternative block of code is executed. This type of statement ensures that code execution doesn't repeat.
- **while loop**
  - A `while` loop executes code only if a specified condition is `true` and repeats execution as long as the condition remains `true`. This is useful when you want to repeat a certain block of code until a condition is no longer met.
- **repeat loop**
  - A `repeat` loop executes code and repeats execution as long as the specified condition is `true`. Unlike `while` loops, the code inside a repeat loop is **guaranteed to execute at least once**.
- **for loop**
  - A `for` loop executes code a set number of times based on specified inputs. It's particularly useful when you know the number of iterations in advance.

> The conditions for **if statements**, **while loops**, and **repeat loops** can be any Luau expression or value. In Luau, **both zero and the empty string are considered true** if a value isn't false or nil. This is a unique feature compared to other scripting languages.

## If Statements

If statements in Luau allow you to control the flow of your code based on certain conditions.

### Basic If Statements

The fundamental `if` statement checks a condition. If the condition is `true`, Luau executes the code between `then` and `end`.

> Here's an example:

```lua
-- This won't print because the condition is false
if 2 + 2 == 5 then
  print("Two plus two is five")
end
```

### Adding Conditions with elseif

When the initial if condition is `false`, you can use an `elseif` statement to test for additional conditions. If any `elseif` condition is `true`, the code block following it will be executed.

> Take a look:

```lua
if 2 + 2 == 5 then
  print("Two plus two is five") -- Doesn't print because the condition is false
elseif 2 + 3 == 5 then
  print("Two plus three is five") -- This will print as 2 + 3 does equal 5
end
```

### Handling All Cases with else

If none of the conditions specified by `if` and `elseif` are `true`, you can use the `else` statement to execute a default code block.

> Check out this example:

```lua
if 2 + 2 == 5 then
  print("Two plus two is five") -- Doesn't print because the condition is false
elseif 2 + 3 == 5 then
  print("Two plus three is five") -- This will print as 2 + 3 does equal 5
else
  print("All conditions failed") -- This will print when both if and elseif conditions are false
end
```

### Execution Order

In a chain of `if`, `elseif`, and `else` conditions, Luau tests conditions from top to bottom. It stops at the **first true condition**, executing the corresponding code block, and skips the rest of the conditions.

## While loops

In Luau, a `while-do` loop is used to repeatedly execute a block of code as long as a specified condition remains `true`.

> Let's break down the basics in a clear and straightforward manner

- **Syntax**

  ```lua
  while condition do
  -- code to execute while the condition is true
  end
  ```

- **Example: Countdown Timer**

  - Consider a countdown timer where we want to display the seconds remaining until it reaches zero.

    ```lua
    local timeRemaining = 10

    while timeRemaining > 0 do
      print("Seconds remaining: " .. timeRemaining)
      timeRemaining -= 1
    end
    ```

    > **Output**

    ```yaml
    Seconds remaining: 10
    Seconds remaining: 9
    Seconds remaining: 8
    Seconds remaining: 7
    Seconds remaining: 6
    Seconds remaining: 5
    Seconds remaining: 4
    Seconds remaining: 3
    Seconds remaining: 2
    Seconds remaining: 1
    ```

    > **Code Explanation**

    1. **Initialization**: Set the initial value for `timeRemaining` to `10`.
    2. **While Loop**: The loop checks if `timeRemaining` is greater than `0`. If `true`, it executes the code inside the loop.
    3. **Print Statement**: Displays the current value of `timeRemaining`.
    4. **Countdown**: Decreases the value of `timeRemaining` by `1` in each iteration.
    5. **Loop Continuation**: The loop continues until `timeRemaining` is no longer greater than `0`.
    6. **Print Statement (Outside the Loop)**: Displays **"Timer reached zero!"** after the loop ends.

### Infinite Loops

> What is an Infinite Loop?

An infinite loop is a loop that continues running indefinitely. In Luau, we achieve this by setting the condition of a `while—do` loop to `true`.

- **Example Code**

  ```lua
  while true do
    print("Looping...")
    task.wait(0.5)
  end
  ```

  > **Output**

  ```lua
  Looping...
  Looping...
  Looping...
  Looping...
  ...
  ```

  > **Code Explanation**

  1. The `while true` do statement creates a loop that will continue as long as the condition remains `true`.
  2. Inside the loop, `print("Looping...")` outputs **"Looping..."** to the console, indicating that the loop is executing.
  3. The `task.wait(0.5)` function introduces a **delay of 0.5 seconds**. Including a delay is **crucial to prevent freezing and crashes**.

> ⚠️ **Include a Delay**: Always include a delay, such as `task.wait()`, in an infinite loop. This prevents the experience from **freezing** and **crashing**.

## Repeat Loops

The `repeat—until` loop in Luau repeats a code block until a specified condition becomes `true`. Unlike some programming languages, in Luau, the conditional test is evaluated after the code block runs, ensuring that the code block always executes at least once. It's particularly useful when you want to perform an action until a certain condition is met.

- **Syntax**

  ```lua
  repeat
  -- Code to be executed
  until condition
  ```

- **Example: Current Goblin Count**

  ```lua
  -- Initialize the goblin count
  local currentGoblinCount = 18

  -- Count goblins up to a maximum of 25
  repeat
    currentGoblinCount += 1
    print("Current goblin count: " .. currentGoblinCount)
  until currentGoblinCount == 25

  -- After the loop completes
  print("Finish Goblins Count!")
  ```

  > **Output**

  ```yaml
  Current goblin count: 19
  Current goblin count: 20
  Current goblin count: 21
  Current goblin count: 22
  Current goblin count: 23
  Current goblin count: 24
  Current goblin count: 25
  Finish Goblins Count!
  ```

  > **Code Explanation**

  1. **Initialization**: Start by initializing the variable (`currentGoblinCount` in this case) outside the loop with an initial value.

  2. **Repeat Block**: The code block inside the `repeat` loop is executed at least once. In this example, it count a goblin, increments the goblin count, and prints the current count.

  3. **Condition Check**: The loop continues until the specified condition (`currentGoblinCount == 25`) becomes `true`.

  4. **Output**: After the loop completes, the script continues, and in this case, a message is printed indicating that goblins count are finished.

## For Loops

For loops in Luau are used to execute a block of code a specified number of times, either based on a numerical counter or the number of items in a collection.

> Let's delve into numeric for loops for a clearer understanding.

### Numeric For Loops

- In a numeric for loop, execution is determined by a counter. The loop is initiated with a start value, end value, and an optional increment.

  - **Syntax**

    ```lua
    for counter = start, stop, increment do
      -- code block to be executed
    end
    ```

    1. **Start**: Initial value of the counter.
    2. **Stop**: Loop continues until the counter reaches this value.
    3. **Increment**: Optional value added to the counter after each iteration. Defaults to `1` if not specified.

  - **Examples**

    - Basic loop from 1 to 3:

      ```lua
      for counter = 1, 3 do
        print(counter)
      end
      ```

      > **Output**

      ```yaml
      1
      2
      3
      ```

    - Loop with a step of 2:

      ```lua
      for counter = 1, 6, 2 do
        print(counter)
      end
      ```

      > **Output**

      ```yaml
      1
      3
      5
      ```

    - Loop with a negative increment:

      ```lua
      for counter = 2, 0, -0.5 do
        print(counter)
      end
      ```

      > **Output**

      ```yaml
      2
      1.5
      1
      0.5
      0
      ```

      > Remember, the increment can be any numeric value, including decimals. Numeric for loops are a powerful tool in Luau for repetitive tasks, and understanding their syntax and behavior is crucial for efficient scripting.

### Generic For Loops

In Luau, the generic for loop is a powerful construct that allows you to iterate over various types of collections, providing flexibility in handling both **arrays** and **dictionaries**.

Luau uses iterator functions to traverse different types of collections. The commonly used iterator functions are:

- `ipairs()`: Iterates over arrays (numeric indices).
- `pairs()`: Iterates over dictionaries (all indices, including non-numeric).

Additionally, the string library provides `string.gmatch()` for iterating over strings.

- **Generalized Iteration**

  - > Direct Table Iteration

    - You can directly iterate over a table using the `in` keyword, simplifying the loop structure:

      ```lua
      for i, v in {1, 2, 3, 4, 5} do
          print(i, v)
      end
      ```

  - > Custom Iterators with `__iter` Metamethod

    - Create custom iterators using the `__iter` metamethod. In this example, we iterate over an array in reverse order:

      ```lua
      local myTable = {1, 2, 3, 4, 5}

      local myMetatable = {
        __iter = function(self)
          local i = #self
          local firstRun = true
          return function()
            if firstRun then
              firstRun = false
              return i, self[i]
            else
              i -= 1
              if i > 0 then
                return i, self[i]
              end
            end
          end
        end
      }

      setmetatable(myTable, myMetatable)

      for i, v in myTable do
        print(i, v)
      end
      ```

- **Iterating Over Arrays**

  - Use `ipairs()` to iterate over arrays, providing both index and value:

    ```lua
    local array = {"a", "b", "c", "d", "e"}

    for index, value in ipairs(array) do
      print(index, value)
    end
    ```

- **Iterating Over Dictionaries**

  - For dictionaries, use pairs() to iterate over all indices, including non-numeric:

    ```lua
    local dictionary = {
      [1] = "a",
      ["Hello"] = "b",
      [5] = "c",
      [true] = "d",
      ["World"] = "f",
      [false] = "e",
    }

    for key, value in pairs(dictionary) do
      print(key, value)
    end
    ```

## Breaking Loops

To exit a loop prematurely, employ the `break` statement.

> In this example, we break an infinite while-do loop after a specified timeout:

```lua
local secondsElapsed = 0
local timeout = 5

while true do
  task.wait(1)
  secondsElapsed += 1
  print("Seconds elapsed:", secondsElapsed)

  if secondsElapsed == timeout then
    break
  end
end

print("Five seconds elapsed. Time to move on!")
```
