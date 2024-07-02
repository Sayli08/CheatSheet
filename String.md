
# Java String Operations

## Syntax:
```java
String input = "GitHub";
```

## Length:
```java
String input = "GitHub";
digits.length();  // 6
```

## Access Characters in String:
1. Use `charAt`:
```java
String input = "GitHub";
Character current = input.charAt(2);  // 't'
```

## Iterate Through Characters in String:
1. Convert String into `char[]` Arrays:
```java
char[] chArrays = input.toCharArray();
for(char ch : chArrays) {
    // Do something with ch
}
```
OR
```java
for(char ch : input.toCharArray()) {
    // Do something with ch
}
```

## Separate the String Based on Some Character:
1. Split:
```java
String str = "geekss@for@geekss";
String[] arrOfStr = str.split("@");
for (String a : arrOfStr) {
    System.out.println(a);
}
```
**Output:**
```
geekss
for
geekss
```

2. Splitting string on multiple spaces in Java:
```java
String str = "Split  this   string";
String[] words = str.split("\\s+");
for (String word : words) {
    System.out.println(word);
}
```
**Output:**
```
Split
this
string
```

## Remove Whitespace from Both Sides of a String:
Use `trim`:
```java
String myStr = "       Hello World!   ";
myStr.trim();  // "Hello World!"
```

## Index of the Last Occurrence of the Given Character:
Use `lastIndexOf`:
```java
String myStr = "GitHub Repository";
//              
// When calculating length, it counts from 1
myStr.length(); // 16

// When calculating index, it starts from 0
myStr.lastIndexOf(" "); // 6
```
