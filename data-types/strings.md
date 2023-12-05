# Understanding String Data Type

## Introduction

> What are Strings ?

A **string** is a bunch of characters like letters, numbers, and symbols all strung together. It's what we use to store most of our text-based information.

## Declaring String

In Luau, creating strings is easy. Just wrap your text with quotes, usually **double quotes (")**, but **single quotes (')** work too. If you need to include the opposite quote inside, switch or use an [espaced quote](#escaping-strings).

```lua
local stringOne = "Hello, World!"
print(stringOne) --> Hello, World!

local stringTwo = 'Hello, "World"!'
print(stringTwo) --> Hello, "World"!
```

> For mutiline strings or when mixing single and double quotes, use double bracktes:

```lua
local stringOne = [[
  Hello
  world!
  Hello "word"!
  Hello 'word'!
]]

print(stringOne)
--> Hello
--> world!
--> Hello "world"!
--> Hello 'world'!
```

> If you find yourself needing brackets inside the string. match the number of equal signs at the beginning and end

```lua
local stringOne = [=[Hello
[[world!]]
]=]

print(stringOne)
--> Hello
--> [[world!]]
```

## Combining Strings

> What is concatenate and how to combine strings ?

To merge strings, simply use two dots **(..)**. No automatic spaces are added, so ensure spaces at the end/begining of strings or insert a space between them.

```lua
local hello = "Hello"
local helloWithSpace = "Hello "
local world = "world!"

local stringOne = hello .. world
local stringTwo = helloWithSpace .. world
local stringThree = hello .. " " .. world

print(stringOne) --> Helloworld!
print(stringTwo) --> Hello world!
print(stringThree) --> Hello world!
```

> For `print()`, you can use commas **(,)** to add spaces between arguments.

```lua
local hello = "Hello"
local world = "world"
local exclamationMark = "!"

print(hello .. world .. exclamationMark) --> Helloworld!
print(hello, world .. exclamationMark) --> Hello world!
print(hello, world, exclamationMark) --> Hello world!
```

Now, combining strings is as simple as connecting them with `..` or using `,` in `print()` for automatic spaces.

## Converting Strings

> How can I convert a string to number ?

Coverting a string to a number is easy with the `tonumber()` function. If the string contains a number, it gives you that **number**; otherwise, it returns **nil**.

```lua
local numericString = "123"
print(tonumber(numericString)) --> 123

local alphanumericString = "Hello123"
print(tonumber(alphanumericString)) --> nil
```

## Escaping Strings

To include special characters in a string, just add a **backslash ( \ )** before the character.

> Here's how

- **Single Quotes**

  - To include a single quote in a single-quoted string, use `\'`:

    ```lua
    local stringOne = 'Hello \'world\'!'
    print(stringOne) --> Hello 'world'!
    ```

- **Double Quotes**

  - To include a double quote in a double-quoted string, use `\"`:

    ```lua
    local stringTwo = "Hello \"world\"!"
    print(stringTwo) --> Hello "world"!
    ```

> Certain characters following backslashes produce **special characters** rather than escaped characters:

- To add a new line, use `\n`
  ```lua
    local stringOne = "Hello\nworld!"
    print(stringOne)
    --> Hello
    ---> world!
  ```
- To inser a horizontal tab, use `\t`
  ```lua
    local stringTwo = "Hello\tworld!"
    print(stringTwo) --> Hello    world!
  ```

## String Interpolation

> What are String Imterpolation ?

String interpolation in Luau is a handy feature allowing you to embed expressions within strings using **backticks (`)**.

- **Basic Interpolation**

  - Declare an interpolated string using **backticks** and insert expressions inside curly brackets

    ```lua
    local name = "JhoN"
    local stringOne = `Hello {name}!`
    print(stringOne) --> Hello JhoN!
    ```

- **Expressions in Interpolations**

  - Although variables are the most common usage, you can use any expression, including math.

    ```lua
    local world = "world"
    local number = 1

    local stringOne = `Hello {world}, {number} time!`
    local stringTwo = `Hello {world}, {number + 1} times!`

    local letters = {"w", "o", "r", "l", "d"}
    local stringThree = `Hello {table.concat(letters)} a third time!`

    print(stringOne) --> Hello world, 1 time!
    print(stringTwo) --> Hello world, 2 times!
    print(stringThree) --> Hello world a third time!
    ```

- **Escape Rules in Interpolations**

  - Follow standard escape rules for backticks, curly brackets, and backslashes.

    ```lua
    local name = "JhoN"
    local stringOne = `Hello \`{name}\`!`
    print(stringOne) --> Hello `JhoN`!
    ```

String interpolation is a versatile tool in Luau, offering a straightforward way to build dynamic strings with embedded expressions.

## Math Conversion

When you perform mathematical operations on a string, Luau automatically converts the string to a number

```lua
print("55" + 10)  --> 65
print("55" - 10)  --> 45
print("55" * 10)  --> 550
print("55" / 10)  --> 5.5
print("55" % 10)  --> 5
```

Luau takes care of the conversion seamlessly. However, if the **string doesn't represent a number**, it throws an **error**:

```lua
print("Hello" + 10) --> Error: attempt to perform arithmetic (add) on string and number
```

So, keep in mind that the string needs to have a valid numeric representation for these operations to work smoothly.

## String Pattern Reference

A string pattern is like a secret code you create using different characters. You can use this code with functions like `string.match()` and `string.gmatch()` to find specific parts, or pieces, of a longer string. It's like finding hidden words in a sentence!

- **Direct Matches**

  - In Luau functions, like `string.match()`, you can perform direct matches to find specific words or patterns in a string. However, be cautious with **magic characters**.

    ```lua
    local matchOne = string.match("Welcome to Roblox!", "Roblox")
    local matchTwo = string.match("Welcome to my awesome game!", "Roblox")

    print(matchOne)  --> Roblox
    print(matchTwo)  --> nil
    ```

    > In this case, the code checks for the presence of the word **"Roblox"** in two different strings, showing the result of each match.

- **Character Classes**

  - Character classes make advanced string searches easier by allowing you to look for items that fall within a specific category, like letters, digits, spaces, or punctuation.

    > **Official Character Classes**:

    | Class | Represents                                | Example Match                        |
    | ----- | ----------------------------------------- | ------------------------------------ |
    | .     | Any character                             | 32kasGJ1%fTlk?@94                    |
    | %a    | Uppercase or lowercase letter             | aBcDeFgHiJkLmNoPqRsTuVwXyZ           |
    | %l    | Lowercase letter                          | abcdefghijklmnopqrstuvwxyz           |
    | %u    | Uppercase letter                          | ABCDEFGHIJKLMNOPQRSTUVWXYZ           |
    | %d    | Any digit (number)                        | 0123456789                           |
    | %p    | Any punctuation character                 | !@#;,.                               |
    | %w    | Alphanumeric character (letter or number) | aBcDeFgHiJkLmNoPqRsTuVwXyZ0123456789 |
    | %s    | Space or whitespace character             | ' ', '\n', and '\r'                  |
    | %c    | Special control character                 |                                      |
    | %x    | Hexadecimal character                     | 0123456789ABCDEF                     |
    | %z    | The NULL character (\0)                   |                                      |

  - For single-letter character classes like `%a` and `%s`, the corresponding uppercase letter represents the **"opposite"** of the class. For example, `%p` represents a punctuation character, while `%P` represents all characters except punctuation.

- **Magic Characters**

  - In pattern matching, there are **12 "magic characters"** reserved for special purposes. To search for these characters explicitly, use the `%` symbol to escape them.

    ```lua
    -- Example: Matching "roblox.com" in the string "What is roblox#com?"
    -- Here, the period is interpreted as "any character"
    local matchOne = string.match("What is roblox#com?", "roblox.com")
    print(matchOne) --> roblox#com

    -- Escape the period with % to treat it as a literal period character
    local matchTwo = string.match("I love roblox.com!", "roblox%.com")
    print(matchTwo) --> roblox.com
    ```

    > In the second example, by using `%`, the period is treated as a regular character, allowing an exact match for **"roblox.com"** in the string **"I love roblox.com!"**.

- **Anchors**

  - In Lua, you can use special symbols `^` and `$` to search for patterns at the start or end of a string.

    - **Start of String**

      - To find a pattern at the beginning of a string, use `^`:

        ```lua
        -- Example 1: Matches because "first" is at the beginning
        local startOne = string.match("first second third", "^first")
        print(startOne)  --> first

        -- Example 2: Doesn't match because "first" isn't at the beginning
        local startTwp = string.match("third second first", "^first")
        print(startTwo)  --> nil
        ```

    - **End of String**

      - To find a pattern at the end of a string, use `$`:

        ```lua
        -- Example 3: Matches because "third" is at the end
        local endOne = string.match("first second third", "third$")
        print(endOne)  --> third

        -- Example 4: Doesn't match because "third" isn't at the end
        local endTwo = string.match("third second first", "third$")
        print(endTwo)  --> nil
        ```

    - **Full String Match**

      - You can use both `^` and `$` together to ensure a pattern matches the entire string, not just part of it:

        ```lua
        -- Example 5: Matches because "Roblox" is the entire string (equality)
        local matchOne = string.match("Roblox", "^Roblox$")
        print(matchOne)  --> Roblox

        -- Example 6: Doesn't match because "Roblox" isn't at the beginning AND end
        local matchTwo = string.match("I play Roblox", "^Roblox$")
        print(matchTwo)  --> nil

        -- Example 7: Matches because "Roblox" is contained within "I play Roblox"
        local matchThree = string.match("I play Roblox", "Roblox")
        print(matchThree)  --> Roblox
        ```

  > These symbols help you precisely locate patterns in strings, either at the start, end, or throughout the entire string.

- **Character Class Modifiers**

  - A character class in Lua helps match specific characters in a string. Initially, a basic pattern like `"%d"` locates the first digit in a string. For example:
    ```lua
    local match = string.match("The Cloud Kingdom has 25 power gems", "%d")
    print(match)  --> 2
    ```
  - To enhance control over matching, modifiers can be added to the character class. Here's a simplified guide:
    | Quantifier | Meaning |
    |------------|--------------------------------------------------|
    | + | Match 1 or more of the preceding character class|
    | - | Match as few of the preceding character class as possible|
    | \* | Match 0 or more of the preceding character class |
    | ? | Match 1 or less of the preceding character class |
    | %n | For n between 1 and 9, matches a substring equal to the nth captured string|
    | %bxy | The balanced capture matching x, y, and everything between (e.g., `%b()` matches a pair of parentheses and everything between them)|
  - Applying a modifier to the original pattern `"%d+"` instead of `"%d"` yields a different result:

    ```lua
    local match1 = string.match("The Cloud Kingdom has 25 power gems", "%d")
    print(match1)  --> 2

    local match2 = string.match("The Cloud Kingdom has 25 power gems", "%d+")
    print(match2)  --> 25
    ```

    > Using `%d+` in the pattern now captures one or more digits, producing the expected output of `25` instead of just `2`.

- **Character Sets**

  - Character sets come in handy when a single character class falls short. Imagine you want to match both lowercase letters `%l` and punctuation characters `%p` in one go. Sets, defined by brackets `[]`, make this easy.

    In the example below, see the power of sets `"[%l%p]+"` versus without `"%l%p+"`.

    ```lua
    --> 1.
    local match1 = string.match("Hello!!! I am another string.", "[%l%p]+")  -- Set
    print(match1)  --> ello!!!

    --> 2.
    local match2 = string.match("Hello!!! I am another string.", "%l%p+")  -- Non-set
    print(match2)  --> o!!!
    ```

    1. The first command **(set)** tells Luau to find both lowercase letters and punctuation. The `+` says to grab as many as possible, stopping at the space `ello!!!`.

    2. In the second command **(non-set)**, the + applies only to %p before it. So, Luau snags just the first lowercase character `o` before the punctuation `!!!`.

    Sets can also be **"opposites"** of themselves. Add a `^` at the start, and it finds everything except what's in the set. `"[%p%s]+"` finds punctuation and spaces, while `"[^%p%s]+"` finds anything but punctuation and spaces.

    Lastly, sets support ranges, letting you find matches between specific starting and ending characters. This advanced feature is explained in more detail in the [Lua 5.1 Manual](https://www.lua.org/manual/5.1/manual.html#5.4.1).

- **String Captures**

  - String captures are like snapshots of specific parts within a larger text pattern. They're enclosed in parentheses and help us grab and save matching portions of text. Check out this straightforward example:

    ```lua
    local pattern = "(%a+)%s?=%s?(%d+)"

    local key1, val1 = string.match("TwentyOne = 21", pattern)
    print(key1, val1)  --> TwentyOne 21

    local key2, val2 = string.match("TwoThousand= 2000", pattern)
    print(key2, val2)  --> TwoThousand 2000

    local key3, val3 = string.match("OneMillion=1000000", pattern)
    print(key3, val3)  --> OneMillion 1000000
    ```

    In this snippet, we're capturing words `%a+` and digits `%d+` around an equal sign. The `?` makes spaces around the equal sign optional, so it works whether spaces are there or not.

    > But wait, there's more! We can even nest captures, like in this example:

    ```lua
    local places = "The Cloud Kingdom is heavenly, The Forest Kingdom is peaceful"
    local pattern = "(The%s(%a+%sKingdom)[%w%s]+)"

    for description, kingdom in string.gmatch(places, pattern) do
      print(description)
      print(kingdom)
    end
    ```

    Here, we're capturing descriptions and nested kingdoms from a string. The iterator first captures the entire `"description"` pattern, then dives in to get the `"kingdom"` within. It does this for each matching pair, making it easy to extract specific information.

    > That's it! With captures, you can pinpoint and extract the information you need from strings with ease.
