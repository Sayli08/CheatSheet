
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


2. Using `charAt`:
```java
String input = "GitHub";
for (int i = 0; i < input.length(); i++) {
    char ch = input.charAt(i);
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
The `substring` method includes the character at the start index but excludes the character at the end index. So, `str.substring(7, 17)` will include the characters from index 7 to 16.

```java
String str = "GitHub Repository";
String subStr = str.substring(7, 17);  // "Repository"
```

### Explanation of Time Complexity for `substring`:
The `substring` method in Java does not actually take O(n) time complexity; it operates in O(1) time complexity. This is because `substring` does not create a new character array; it uses the same underlying character array as the original string and simply adjusts the offset and count to represent the new string.

However, there are a few nuances to keep in mind:

- **Java 7 and Earlier Versions**: In these versions, `substring` used the same underlying character array as the original string, making it an O(1) operation.

- **Java 7 Update 6 and Later Versions**: Starting from this version, the implementation was changed to avoid memory leaks. The `substring` method creates a new character array, making it an O(n) operation where n is the length of the substring.

**Time Complexity:** 
- O(1) for Java 7 and earlier versions
- O(n) for Java 7 update 6 and later versions, where n is the length of the substring.

## Checking Prefix of a String:
1. Use `startsWith`:
```java
String str = "GitHub Repository";
boolean isPrefix = str.startsWith("Git");  // true
boolean isNotPrefix = str.startsWith("Hub");  // false
```

**Time Complexity:** O(k) where k is the length of the prefix string

## Convert Integer to String:

1. Using `String.valueOf`:
```java
int num = 123;
String str = String.valueOf(num);  // "123"
```

**Time Complexity:** O(1)

2. Using `Integer.toString`:
```java
int num = 123;
String str = Integer.toString(num);  // "123"
```

**Time Complexity:** O(1)

3. Using `Integer.toString` with a radix (base):
```java
int num = 123;
String str = Integer.toString(num, 10);  // "123" in base 10
String strHex = Integer.toString(num, 16);  // "7b" in base 16
```

**Time Complexity:** O(1)

4. Using String concatenation:
```java
int num = 123;
String str = "" + num;  // "123"
```

**Time Complexity:** O(1)

## Example Usage:
```java
public class Main {
    public static void main(String[] args) {
        int num = 123;

        // Using String.valueOf
        String str1 = String.valueOf(num);
        System.out.println(str1);  // Output: "123"

        // Using Integer.toString
        String str2 = Integer.toString(num);
        System.out.println(str2);  // Output: "123"

        // Using Integer.toString with radix
        String str3 = Integer.toString(num, 10);
        System.out.println(str3);  // Output: "123"
        
        String strHex = Integer.toString(num, 16);
        System.out.println(strHex);  // Output: "7b"

        // Using String concatenation
        String str4 = "" + num;
        System.out.println(str4);  // Output: "123"
    }
}
```
###Note: All the methods above have a time complexity of O(1) because converting an integer to a string involves a constant amount of work regardless of the integer's value.
