Sure, here is the updated markdown with a use case for using switch as an expression:

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

