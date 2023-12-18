# Understanding Operators in Luau

## Introduction

An operator is a symbol for performing an operation or conditional evaluation.

## Logical Operators

Logical operators in Luau are used for conditional evaluations, returning values based on boolean conditions. Unlike some languages, Luau considers both zero and the empty string as true.

- `and`: Returns the second argument only if both conditions are `true`.

  ```lua
  -- In the first example, 4 and 5 evaluates to 5 because both conditions are true. The
  print(4 and 5) -- 5
  -- The second example, nil and 12, results in nil since the first condition is false.
  print(nil and 12) -- nil
  -- The third example, false and 12, also evaluates to false.
  print(false and 12) -- false
  ```

- `or`: Returns the first argument if it's `true`; otherwise, returns the second argument.

  ```lua
  -- The first example, 4 or 5, evaluates to 4 because the first condition is true.
  print(4 or 5) -- 4
  -- The second example, nil or 12, results in 12 as the first condition is false.
  print(nil or 12) -- 12
  -- The third example, false or true, evaluates to true since the first condition is false.
  print(false or true) -- true
  ```

- `not`: The not operator returns the opposite boolean value of the argument.

  ```lua
  -- In the first example, not true results in false because the original condition is true.
  print(not true) -- false
  -- In the second example, not nil, the output is true as the original condition is false.
  print(not nil) -- true
  ```

## Relational Operators

Relational operators compare two parameters and return a boolean result.

| Operator | Description              | Example        |
| -------- | ------------------------ | -------------- |
| ==       | Equal to                 | 3 == 5 → false |
| ~=       | Not equal to             | 3 ~= 5 → true  |
| >        | Greater than             | 3 > 5 → false  |
| <        | Less than                | 3 < 5 → true   |
| >=       | Greater than or equal to | 3 >= 5 → false |
| <=       | Less than or equal to    | 3 <= 5 → true  |

## Arithmetic Operators

Lua supports various arithmetic operators.

| Operator | Description    | Example     |
| -------- | -------------- | ----------- |
| +        | Addition       | 1 + 1 = 2   |
| -        | Subtraction    | 1 - 1 = 0   |
| \*       | Multiplication | 5 \* 5 = 25 |
| /        | Division       | 10 / 5 = 2  |
| //       | Floor Division | 10 // 4 = 2 |
| ^        | Exponentiation | 2 ^ 4 = 16  |
| %        | Modulus        | 13 % 7 = 6  |
| -        | Unary negation | -2 = 0 - 2  |

## Compound Assignment Operators

Compound assignment operators perform an operation and assign the result to a variable in one step.

| Operator | Operation      | Example         | New Value of x |
| -------- | -------------- | --------------- | -------------- |
| +=       | Addition       | x += 2          | 5              |
| -=       | Subtraction    | x -= 2          | 1              |
| \*=      | Multiplication | x \*= 2         | 6              |
| /=       | Division       | x /= 2          | 1.5            |
| //=      | Floor Division | x //= 2         | 1              |
| %=       | Modulus        | x %= 2          | 1              |
| ^=       | Exponentiation | x ^= 2          | 9              |
| ..=      | Concatenation  | x ..= " World!" | "3 World!"     |

## Miscellaneous Operators

Miscellaneous operators include concatenation and length.

| Operator | Description          | Example                                      |
| -------- | -------------------- | -------------------------------------------- |
| ..       | Concatenates strings | print("Hello " .. "World!")                  |
| #        | Length of table      | If tableVar = {1, 2, 3}, then #tableVar == 3 |

## Conclusion

These operators are key to building efficient logic into your scripts, allowing you to create code that is responsive and adaptable to different situations.
