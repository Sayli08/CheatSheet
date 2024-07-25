For using switch as an expression:

```markdown
# Java Switch Statement Cheat Sheet

## Traditional Switch Statement

### Syntax
```java
switch (expression) {
    case value1:
        // Statements
        break;
    case value2:
        // Statements
        break;
    // Other cases
    default:
        // Default statements
        break;
}
```

### Example
```java
int switchValue = 3;
switch (switchValue) {
    case 1:
        System.out.println("Value was 1");
        break;
    case 2:
        System.out.println("Value was 2");
        break;
    case 3:
    case 4:
    case 5:
        System.out.println("Was a 3, a 4, or a 5");
        System.out.println("Actually it was a " + switchValue);
        break;
    default:
        System.out.println("Was not 1, 2, 3, 4, or 5");
        break;
}
```

## Enhanced Switch Statement (Java 12+)

### Syntax
```java
switch (expression) {
    case value1 -> // Statements;
    case value2 -> // Statements;
    // Other cases
    default -> // Default statements;
}
```

### Example
```java
int switchValue = 3;
switch (switchValue) {
    case 1 -> System.out.println("Value was 1");
    case 2 -> System.out.println("Value was 2");
    case 3, 4, 5 -> {
        System.out.println("Was a 3, a 4, or a 5");
        System.out.println("Actually it was a " + switchValue);
    }
    default -> System.out.println("Was not 1, 2, 3, 4, or 5");
}
```

## Using Switch as an Expression (Java 12+)

### Syntax
```java
result = switch (expression) {
    case value1 -> // Expression;
    case value2 -> // Expression;
    // Other cases
    default -> // Default expression;
};
```

### Example
```java
int day = 3;
String dayType = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid day";
};

System.out.println(dayType); // Outputs: Weekday
```
##

# Let's expand on the explanation of using switch as an expression in Java:

### Switch as an Expression

- In Java 12 and later, the switch statement can be used as an expression. 
- This means that the switch can directly return a value, which can then be assigned to a variable or used in other expressions. 
- This makes the switch statement more powerful and concise.

#### Syntax
```java
result = switch (expression) {
    case value1 -> // Expression;
    case value2 -> // Expression;
    // Other cases
    default -> // Default expression;
};
```

### Key Features
1. **Arrow Syntax (`->`)**: Instead of using colons (`:`) and `break` statements, the arrow syntax is used to associate each case with an expression.
2. **Returning Values**: Each case in the switch expression can return a value, and these values can be directly assigned to a variable.
3. **No Fall-Through**: There's no need to use `break` statements to prevent fall-through; each case is isolated and returns a value independently.
4. **Multiple Labels**: You can use multiple labels for a single case, separated by commas.
5. **Compact and Readable**: The switch expression is more concise and easier to read compared to the traditional switch statement.

### Example
Here's an example demonstrating the use of switch as an expression:

```java
int day = 3;
String dayType = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid day";
};

System.out.println(dayType); // Outputs: Weekday
```

### Explanation of the Example
- **Variable Assignment**: The result of the switch expression is assigned to the variable `dayType`.
- **Cases**: The cases 1, 2, 3, 4, and 5 all map to the expression `"Weekday"`.
- **Multiple Labels**: The cases 6 and 7 map to the expression `"Weekend"`.
- **Default Case**: The default case handles any values that do not match the specified cases, returning `"Invalid day"`.
- **Output**: Based on the value of `day`, the corresponding string is returned and printed.

### Benefits
- **Conciseness**: The code is shorter and more readable compared to using a traditional switch statement with `break` statements.
- **Safety**: Since there's no fall-through, there's less risk of bugs due to missing `break` statements.
- **Flexibility**: It allows for more flexible and expressive code, especially when you need to return values from a switch.

### More Complex Example
Here's a more complex example that includes blocks of code for each case:

```java
int month = 4;
int daysInMonth = switch (month) {
    case 1, 3, 5, 7, 8, 10, 12 -> 31;
    case 4, 6, 9, 11 -> 30;
    case 2 -> {
        int year = 2024;
        if (year % 4 == 0 && (year % 100 != 0 || year % 400 == 0)) {
            yield 29;
        } else {
            yield 28;
        }
    }
    default -> throw new IllegalArgumentException("Invalid month: " + month);
};

System.out.println("Days in month: " + daysInMonth); // Outputs: Days in month: 30
```

### Explanation of the Complex Example
- **Variable Assignment**: The result of the switch expression is assigned to the variable `daysInMonth`.
- **Single Line Cases**: For months with a fixed number of days (31 or 30), the values are returned directly.
- **Block of Code for February**: For February, a block of code checks whether the year is a leap year and uses the `yield` statement to return the appropriate number of days.
- **Default Case**: The default case throws an exception if an invalid month is provided.

This example demonstrates how switch expressions can include blocks of code, which can use the `yield` statement to return values. 
This makes switch expressions very flexible and capable of handling complex logic.

By using switch as an expression, you can write more expressive, readable, and maintainable code.





## Key Differences

### Traditional Switch Statement
- Uses `case` labels followed by a colon (`:`).
- Requires explicit `break` statements to prevent fall-through.
- Supports `char`, `byte`, `short`, `int`, `String`, and `enum` types.

### Enhanced Switch Statement
- Uses `case` labels followed by an arrow (`->`).
- No need for `break` statements; no fall-through.
- Supports multiple labels per case, separated by commas.
- More concise and readable.

### Switch as an Expression
- Allows the use of switch in assignment statements.
- Each case can return a value, making switch more powerful and expressive.
- Available from Java 12 onwards.

## Notes
- Always use `default` to handle unexpected cases.
- Enhanced switch statements are available from Java 12 onwards.
- Use enhanced switch statements for improved readability and reduced errors due to fall-through.
- **Valid types for switch statements**: `char`, `byte`, `short`, `int`, `String`, and `enum` types.
```

