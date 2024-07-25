
# Java Math Functions

## Math.round
Rounds a floating-point number to the nearest integer.

### Syntax
```java
long result = Math.round(double value);
int result = Math.round(float value);
```

### Example
```java
double value1 = 5.6;
float value2 = 3.4f;
long roundedValue1 = Math.round(value1); // 6
int roundedValue2 = Math.round(value2); // 3
```

## Math.PI
Represents the value of π (pi), approximately 3.14159.

### Syntax
```java
double pi = Math.PI;
```

### Example
```java
double circumference = 2 * Math.PI * radius;
```

## Math.sqrt
Calculates the square root of a number.

### Syntax
```java
double result = Math.sqrt(double value);
```

### Example
```java
double value = 16.0;
double sqrtValue = Math.sqrt(value); // 4.0
```

## Math.pow
Raises a number to the power of another number.

### Syntax
```java
double result = Math.pow(double base, double exponent);
```

### Example
```java
double base = 2.0;
double exponent = 3.0;
double powerValue = Math.pow(base, exponent); // 8.0
```

## Math.abs
Returns the absolute value of a number.

### Syntax
```java
int result = Math.abs(int value);
long result = Math.abs(long value);
float result = Math.abs(float value);
double result = Math.abs(double value);
```

### Example
```java
int value1 = -10;
double value2 = -5.5;
int absValue1 = Math.abs(value1); // 10
double absValue2 = Math.abs(value2); // 5.5
```

## Math.max
Returns the greater of two values.

### Syntax
```java
int result = Math.max(int a, int b);
long result = Math.max(long a, long b);
float result = Math.max(float a, float b);
double result = Math.max(double a, double b);
```

### Example
```java
int a = 10;
int b = 20;
int maxValue = Math.max(a, b); // 20
```

## Math.min
Returns the smaller of two values.

### Syntax
```java
int result = Math.min(int a, int b);
long result = Math.min(long a, long b);
float result = Math.min(float a, float b);
double result = Math.min(double a, double b);
```

### Example
```java
int a = 10;
int b = 20;
int minValue = Math.min(a, b); // 10
```

## Math.random
Returns a random double value between 0.0 (inclusive) and 1.0 (exclusive).

### Syntax
```java
double randomValue = Math.random();
```

### Example
```java
double randomValue = Math.random();
System.out.println(randomValue); // Example output: 0.7310674112186997
```

## Math.log
Returns the natural logarithm (base e) of a value.

### Syntax
```java
double result = Math.log(double value);
```

### Example
```java
double value = 10.0;
double logValue = Math.log(value); // 2.302585092994046
```

## Math.exp
Returns Euler's number e raised to the power of a value.

### Syntax
```java
double result = Math.exp(double value);
```

### Example
```java
double value = 2.0;
double expValue = Math.exp(value); // 7.38905609893065
```

## Math.sin
Returns the trigonometric sine of an angle.

### Syntax
```java
double result = Math.sin(double angle);
```

### Example
```java
double angle = Math.toRadians(30); // converting degrees to radians
double sineValue = Math.sin(angle); // 0.5
```

## Math.cos
Returns the trigonometric cosine of an angle.

### Syntax
```java
double result = Math.cos(double angle);
```

### Example
```java
double angle = Math.toRadians(60); // converting degrees to radians
double cosineValue = Math.cos(angle); // 0.5
```

## Math.tan
Returns the trigonometric tangent of an angle.

### Syntax
```java
double result = Math.tan(double angle);
```

### Example
```java
double angle = Math.toRadians(45); // converting degrees to radians
double tangentValue = Math.tan(angle); // 1.0
```
