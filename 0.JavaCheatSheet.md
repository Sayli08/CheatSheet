
# Java Cheat Sheet

## 1. Java Operators

### Arithmetic Operators
| Operator | Description         | Example  |
|----------|---------------------|----------|
| `+`      | Addition            | `a + b`  |
| `-`      | Subtraction         | `a - b`  |
| `*`      | Multiplication      | `a * b`  |
| `/`      | Division            | `a / b`  |
| `%`      | Modulus (Remainder) | `a % b`  |

### Comparison Operators
| Operator | Description            | Example  |
|----------|------------------------|----------|
| `==`     | Equal to               | `a == b` |
| `!=`     | Not equal to           | `a != b` |
| `>`      | Greater than           | `a > b`  |
| `<`      | Less than              | `a < b`  |
| `>=`     | Greater than or equal to | `a >= b` |
| `<=`     | Less than or equal to  | `a <= b` |

### Logical Operators
| Operator | Description | Example |
|----------|-------------|---------|
| `&&`     | Logical AND | `a && b`|
| `||`     | Logical OR  | `a || b`|
| `!`      | Logical NOT | `!a`    |

### Bitwise Operators
| Operator | Description            | Example    |
|----------|------------------------|------------|
| `&`      | Bitwise AND            | `a & b`    |
| `|`      | Bitwise OR             | `a | b`    |
| `^`      | Bitwise XOR            | `a ^ b`    |
| `~`      | Bitwise Complement     | `~a`       |
| `<<`     | Left shift             | `a << 2`   |
| `>>`     | Right shift            | `a >> 2`   |
| `>>>`    | Unsigned right shift   | `a >>> 2`  |

## 2. Abbreviated (Compound) Operators

| Abbreviated Operator | Equivalent To              | Example           | Description                         |
|----------------------|----------------------------|-------------------|-------------------------------------|
| `+=`                 | `a = a + b`                | `a += b`          | Add and assign                      |
| `-=`                 | `a = a - b`                | `a -= b`          | Subtract and assign                 |
| `*=`                 | `a = a * b`                | `a *= b`          | Multiply and assign                 |
| `/=`                 | `a = a / b`                | `a /= b`          | Divide and assign                   |
| `%=`                 | `a = a % b`                | `a %= b`          | Modulus and assign                  |
| `&=`                 | `a = a & b`                | `a &= b`          | Bitwise AND and assign              |
| `|=`                 | `a = a | b`                | `a |= b`          | Bitwise OR and assign               |
| `^=`                 | `a = a ^ b`                | `a ^= b`          | Bitwise XOR and assign              |
| `<<=`                | `a = a << b`               | `a <<= b`         | Left shift and assign               |
| `>>=`                | `a = a >> b`               | `a >>= b`         | Right shift and assign              |
| `>>>=`               | `a = a >>> b`              | `a >>>= b`        | Unsigned right shift and assign     |
| `++`                 | `a = a + 1`                | `a++` or `++a`    | Increment by 1                      |
| `--`                 | `a = a - 1`                | `a--` or `--a`    | Decrement by 1                      |

## 3. `if-then` Statement

```java
if (condition) {
    // Code to execute if condition is true
} else if (anotherCondition) {
    // Code to execute if the anotherCondition is true
} else {
    // Code to execute if all conditions are false
}
```

**Example:**

```java
int a = 10;
if (a > 5) {
    System.out.println("a is greater than 5");
} else if (a == 5) {
    System.out.println("a is equal to 5");
} else {
    System.out.println("a is less than 5");
}
```

## 4. `for` Loop

```java
for (initialization; condition; update) {
    // Code to execute in the loop
}
```

**Example:**

```java
for (int i = 0; i < 10; i++) {
    System.out.println("i = " + i);
}
```

## 5. `switch-case` Statement

```java
switch (variable) {
    case value1:
        // Code to execute for value1
        break;
    case value2:
        // Code to execute for value2
        break;
    // Add more cases as needed
    default:
        // Code to execute if no case matches
        break;
}
```

**Example:**

```java
int day = 3;
switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    case 4:
        System.out.println("Thursday");
        break;
    case 5:
        System.out.println("Friday");
        break;
    default:
        System.out.println("Weekend");
        break;
}
```
