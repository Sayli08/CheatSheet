
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

## Notes
- Always use `default` to handle unexpected cases.
- Enhanced switch statements are available from Java 12 onwards.
- Use enhanced switch statements for improved readability and reduced errors due to fall-through.
```

This cheat sheet provides a quick reference to the syntax and usage of both traditional and enhanced switch statements in Java, along with examples and key differences.
