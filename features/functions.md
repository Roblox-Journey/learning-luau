# Uderstanding Functions in Luau

## Introduction

Functions are essential blocks of code in Luau that allow you to execute a set of instructions repeatedly. Whether connected to events or assigned as callbacks, functions play a crucial role in creating modular and organized code.

- ### Basic Function Structure

  - A function definition in Luau includes the following components:

    - **Scope**: Specify whether the function is global or local.
    - **Keyword**: Use the `function` keyword to define a function.
    - **Name**: Choose a name for your function using camelCase.
    - **Parameters**: Enclose the function parameters in parentheses `()`.
    - **Body**: The block of code containing the instructions of the function.
    - **End Keyword**: Conclude the function definition with the `end` keyword.

  - **Example**: Simple Addition Function

    ```lua
    -- This function has no parameters and returns nil
    local function addOneAndTwo()
      local result = 1 + 2
      print(result)
    end

    -- Calling the function without a return
    addOneAndTwo() -- Output: 3
    ```

    > In this example, the function `addOneAndTwo` adds `1` and `2`, storing the result in a variable called `result`, and then prints the result. The function is called using `addOneAndTwo()`, resulting in the output `3`.

## Parameters

In Luau, parameters are like placeholders or variables that you use to pass information into a function. They exist only within the function's scope, meaning they can only be accessed and used within that specific function. By default, functions in Luau have no parameters.

- ### Defining Parameters

  - When you create a function, you can specify parameters by listing them within the parentheses after the function name. For example:

    ```lua
    -- This function has two parameters: num1 and num2
    local function addNumbers(num1, num2)
      print(num1 + num2)
    end
    ```

    > Here, `num1` and `num2` are the parameters of the `addNumbers` function.

- ### Using Parameters

  - When you call a function, you provide values for its parameters. If you provide more values than the function expects, Luau simply ignores the extra ones. If you provide fewer values, Luau automatically sets the missing parameters to `nil`.

    ```lua
    addNumbers(2, 3)   -- Output: 5
    addNumbers(5, 6, 7) -- Output: 11 (extra parameter '7' is ignored)
    addNumbers(9)      -- Output: attempt to perform arithmetic (add) on number and nil
    ```

  1. In the **first example**, `addNumbers(2, 3)`, `num1` is set to 2, and `num2` is set to 3, resulting in the sum being printed (`5`).

  2. In the **second example**, `addNumbers(5, 6, 7)`, only the first two values are used, and the third one (`7`) is ignored.

  3. The **third example**, `addNumbers(9)`, demonstrates an attempt to use a function with fewer parameters than expected. In this case, `num1` is set to 9, but `num2` is automatically set to `nil`, leading to an error when trying to perform arithmetic with `nil`.

## Return

In Luau, the `return` keyword is crucial for a function to provide a specific result after a computation. It's important to note that you can return multiple values from a single function.

- ### Let's explore this through some clear examples:

  - **Example 1**: Returning a Single Value

    ```lua
    -- This function returns a single value
    local function addNumbers(num1, num2)
      local result = num1 + num2
      return result
    end

    -- Calling the function and printing the result
    print(addNumbers(1, 2)) -- Output: 3
    local seven = addNumbers(3, 4)
    print(seven) -- Output: 7
    ```

    > In the above example, the `addNumbers` function takes two numbers as parameters, adds them, and returns the result. The `print(addNumbers(1, 2))` call prints the returned value, while the variable **seven** stores the result of the subsequent call.

  - **Example 2**: Returning a Multiple Values

    ```lua
    -- This function returns multiple values: sum and subtract
    local function addAndSubtract(num1, num2)
      local sum = num1 + num2
      local subtract = num1 - num2
      return sum, subtract
    end

    -- Calling the function and expecting multiple return values
    local sum, subtract = addAndSubtract(2, 3)
    print(sum) -- Output: 5
    print(subtract) -- Output: -1
    ```

    > In the second example, the `addAndSubtract` function performs both addition and subtraction on the provided numbers. It returns two distinct values, and when calling the function, we expect and print these multiple values separately.

> ⚠️ **Important Note**: When using the `return` keyword, it's crucial to end the function execution with the `end` keyword. Do not add code between the `return` command and `end`, as it will result in an error.

## Methods

Luau, employs a powerful concept called methods to organize code within objects like classes or tables. Methods are essentially functions tied to an object, expecting the object itself (referred to as `self`) as the first argument. Let's delve into the key aspects of methods using examples.

- ### Syntax: Dot Notation vs. Colon Notation

  - Methods can be called using either dot notation (`.`) or colon notation (`:`). However, it's crucial to note the difference. Dot notation requires explicitly passing `self` as an argument, while colon notation automatically includes `self` as the first argument.

    ```lua
    -- Using dot notation
    firstPart.Destroy(firstPart)
    -- Using colon notation
    secondPart:Destroy()
    ```

  - **Common Methods in Roblox**

    - All objects in Roblox, descending from Instance, share common methods like `Instance:Destroy()`, `Instance:Clone()`, and `Instance:FindFirstChild()`.

      ```lua
      local firstPart = Instance.new("Part")
      local secondPart = Instance.new("Part")
      -- ... (assume both parts are parented to workspace)
      firstPart.Destroy(firstPart) -- Dot notation
      secondPart:Destroy() -- Colon notation
      ```

- ### Defining Methods

  - To create a method in a table, specify the method name as the key and the function as the value. The `self` parameter in the method refers to the table itself. Parameters, if any, follow `self` in the method definition.

    ```lua
    local testButton = {
      enabled = true,
      changeEnabled = function(self, isEnabled)
        self.enabled = isEnabled
        print(self.enabled)
      end
    }
    ```

- ### Calling Methods

  - Calling a method involves using colon notation, passing the table itself as the first argument.

    ```lua
    testButton:changeEnabled(false) -- Invoking the method
    ```

## Callbacks

Callbacks are functions that respond to the execution of another function or process. Unlike event handlers, callbacks yield until they complete their execution. In Roblox, some functions, such as `delay()` and `spawn()`, accept callbacks as parameters. One can find callbacks as write-only members of certain classes in the Roblox Studio API.

- **Widely used callbacks include**:

  - `MarketplaceService.ProcessReceipt`: Handles developer product purchases.
  - `BindableFunction.OnInvoke`: Calls the function when a script invokes BindableFunction.
  - `RemoteFunction.OnClientInvoke`: Calls the function when the server fires the RemoteFunction to a specific client or to all clients.
  - `RemoteFunction.OnServerInvoke`: Calls the function when a client invokes the RemoteFunction on the server.

### Setting Callbacks

To set a callback, you assign a function to it. For example, let's consider `BindableFunction.OnInvoke`. This callback is associated with a BindableFunction, and you can set either a named or anonymous function to it. You can then invoke the function using the `:Invoke()` method on the callback. The arguments you pass to `:Invoke()` are forwarded to the callback, and the return value from the callback is then returned to the caller of `:Invoke()`.

- **Here's an example**:

  ```lua
  -- Creating a BindableFunction
  local bindableFunction = Instance.new("BindableFunction")

  -- Setting the callback function
  bindableFunction.OnInvoke = function(number)
  return 2 * number
  end

  -- Invoking the callback
  print(bindableFunction:Invoke(42)) -- Output: 84
  ```

  > In this example, the callback function simply doubles the input number. You can customize the callback function based on your specific requirements.

Understanding and effectively utilizing callbacks is essential for creating dynamic and responsive scripts in Roblox. Whether you are handling in-game purchases, responding to player actions, or facilitating communication between server and client, callbacks provide a powerful mechanism to enhance the functionality of your Roblox game

## Function Techniques

- ### Event Handlers

  - When programming in Luau within the Roblox environment, it's crucial to grasp the concept of Event Handlers. These are code blocks that execute a specific function when an event occurs.

    - **Creating an Event Handler**:

      - In the provided code, observe the following structure:

        ```lua
        local Players = game:GetService("Players")

        local function onPlayerAdded(player)
          print(player.Name .. " joined the game!")
        end

        Players.PlayerAdded:Connect(onPlayerAdded)
        ```

        - `game:GetService("Players")`: Here, we are obtaining the Players service from the game. This service is essential for interacting with players present in the game.

        - `local function onPlayerAdded(player) ... end`: We are defining a function named `onPlayerAdded`. This function will be executed when the `PlayerAdded` event is triggered, i.e., when a new player joins the game.

        - `print(player.Name .. " joined the game!")`: Inside the `onPlayerAdded` function, we are using `print()` to display a message in the console. This message will include the name of the newly added player.

        - `Players.PlayerAdded:Connect(onPlayerAdded)`: Here, we are connecting our `onPlayerAdded` function to the `PlayerAdded` event. This means that whenever a new player enters the game, our function will be called automatically.

        > **Output**:

        Let's assume two players, "Player1" and "Player2," join the game. When executing this code, the console will display:

        ```yaml
        Player1 joined the game!
        Player2 joined the game!
        ```

- ### Anonymous Functions

  - Luau, a powerful scripting language, allows you to create functions without names, aptly called anonymous functions. These functions are particularly useful for tasks like callbacks and event handling. In this guide, we'll delve into the basics of anonymous functions and explore their application through practical examples.

    - **Syntax and Scope**

      - Similar to named functions, anonymous functions in Luau start and end with the `function` and `end` keywords. However, unlike named functions, you don't need the `local` keyword to indicate local scope because anonymous functions inherently possess local scope.

        ```lua
        -- Anonymous function example
        local myAnonymousFunction = function(parameter)
          -- Function body
        end
        ```

    - **Callbacks with Anonymous Functions**

      - One common use of anonymous functions is as callbacks. Consider the following example, where an anonymous function is employed as a callback for the `task.delay()` function:

        ```lua
        -- Anonymous function in a callback to task.delay()
        task.delay(2, function(exactTimeElapsed)
          print(exactTimeElapsed) -- Output: 2.0064592329945
        end)
        ```

        In this case, the anonymous function is executed after a delay of 2 seconds, receiving the exact time elapsed as a parameter. This concise syntax is advantageous for short, one-off operations.

    - **Event Handling with Anonymous Functions**

      - Anonymous functions are also handy for event handling. Let's look at an example involving the `Players.PlayerAdded` event:

        ```lua
        -- Anonymous function in an event handler
        local Players = game:GetService("Players")
        Players.PlayerAdded:Connect(function(player)
          print(player.Name .. " joined the game!")
        end)
        ```

        Here, the anonymous function is connected to the `PlayerAdded` event. When a player joins the game, the function is invoked, printing a message indicating the player's name and the action.

- ### Functions in ModuleScripts

  - You can reuse functions across multiple scripts by storing them in [ModuleScripts](). Functions are a Luau data type, so you can store them in tables with other data.

- ### Variadic Functions

  - Luau, a versatile scripting language, supports variadic functions, allowing them to accept a variable number of arguments. This flexibility is particularly useful in scenarios where the number of inputs may vary. Let's explore the basics of variadic functions in Luau with clear examples.

  - **Understanding Variadic Functions**

    - A variadic function, such as Luau built-in `print()`, can take any number of arguments. Consider the following examples:

      ```lua
      print(2, "+", 2, "=", 2+2) -- Output: 2 + 2 = 4
      print( string.format("The %s is a %s!", "cake", "lie") ) -- Output: The cake is a lie!
      print( string.byte(115, 101, 99, 114, 101, 116) ) -- Output: secret
      ```

  - **Defining Variadic Functions**

    - To create your own variadic function, use the `...` token as the last or only parameter. This token collects the extra arguments into a table for convenient handling:

      ```lua
      local function variadic(named, ...)
        local arguments = {...} -- Pack extra arguments into a table
        print("Named argument = ", named)
        for i, value in ipairs(arguments) do
          print("Input No. ", i, "=", value)
        end
      end

      variadic(10, "Hi", 20, "Variadic Function")
      -- Output:
      -- Named argument = 10
      -- Input No. 1 = Hi
      -- Input No. 2 = 20
      -- Input No. 3 = Variadic Function
      ```

  - **Argument Forwarding**

    - Variadic functions can act as wrappers, forwarding arguments to other functions. Here's an example:

      ```lua
      local function printAround(functionToPrintAround, ...)
        print("Before")
        functionToPrintAround(...)
        print("After")
      end

      local function addNumbers(x, y, z)
        print("x =", x)
        print("y + z =", y + z)
      end

      printAround(addNumbers, 1, 2, 3)
      -- Output:
      -- Before
      -- x = 1
      -- y + z = 5
      -- After
      ```

  - **Calling a Variadic Function with Arrays**

    - If you have a table of values and want to pass them to a global variadic function like `print()`, use the `unpack()` function to pass the values instead of the entire table:

      ```lua
      local squares = {1, 4, 9, 16, 25}
      print( "The first 5 square numbers are:", unpack(squares) )
      -- Output: The first 5 square numbers are: 1 4 9 16 25
      ```

> Understanding and utilizing variadic functions in Luau enhances your ability to create flexible and dynamic code. Experiment with these concepts to deepen your understanding and improve your scripting skills.
