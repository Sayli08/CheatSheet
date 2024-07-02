
# Java String Operations

## Syntax:
```java
String input = "GitHub";
```

**Time Complexity:** O(1)

## Length:
```java
String input = "GitHub";
input.length();  // 6
```

**Time Complexity:** O(1)

## Access Characters in String:
1. Use `charAt`:
```java
String input = "GitHub";
Character current = input.charAt(2);  // 't'
```

**Time Complexity:** O(1)

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

**Time Complexity:** O(n) where n is the length of the string

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

**Time Complexity:** O(n) where n is the length of the string

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

**Time Complexity:** O(n) where n is the length of the string

## Remove Whitespace from Both Sides of a String:
Use `trim`:
```java
String myStr = "       Hello World!   ";
myStr.trim();  // "Hello World!"
```

**Time Complexity:** O(n) where n is the length of the string

## Index of the Last Occurrence of the Given Character:
Use `lastIndexOf`:
```java
String myStr = "GitHub Repository";
//                01234567890123456
// When calculating length, it counts from 1
myStr.length(); // 17

// When calculating index, it starts from 0
myStr.lastIndexOf(" "); // 6
```

**Time Complexity:** O(n) where n is the length of the string

## Extracting Substrings:
1. Use `substring`:
   
The `substring` method includes the character at the start index but excludes the character at the end index.
So, `str.substring(7, 17)` will include the characters from index 7 to 16.

```java
String str = "GitHub Repository"; // 0 to 5 is GitHub , 6 is space, 7 to 16 is Repository 
String subStr = str.substring(7, 17);  // "Repository"
```

**Time Complexity:** O(n) where n is the length of the substring

## Checking Prefix of a String:
1. Use `startsWith`:
```java
String str = "GitHub Repository";
boolean isPrefix = str.startsWith("Git");  // true
boolean isNotPrefix = str.startsWith("Hub");  // false
```

**Time Complexity:** O(k) where k is the length of the prefix string
