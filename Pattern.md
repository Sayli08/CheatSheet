# Java Pattern Operations Cheat Sheet

## Import Statement
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;
```

## Creating a Pattern
1. Compile a Pattern:
```java
Pattern pattern = Pattern.compile("regex");
```
- **Time Complexity:** O(1) (compilation)

## Matching a Pattern
1. Create a Matcher:
```java
Matcher matcher = pattern.matcher("inputString");
```
- **Time Complexity:** O(1)

## Finding Matches
1. Check for any match:
```java
boolean found = matcher.find();
```
- **Time Complexity:** O(n) where n is the length of the input string

2. Check if the entire string matches:
```java
boolean matches = matcher.matches();
```
- **Time Complexity:** O(n) where n is the length of the input string

## Accessing Match Information
1. Group:
```java
if (matcher.find()) {
    String group = matcher.group(); // Entire match
}
```
- **Time Complexity:** O(1)

2. Group with Index:
```java
if (matcher.find()) {
    String group1 = matcher.group(1); // First capturing group
}
```
- **Time Complexity:** O(1)

3. Start and End Positions:
```java
if (matcher.find()) {
    int start = matcher.start(); // Start position of the match
    int end = matcher.end(); // End position of the match
}
```
- **Time Complexity:** O(1)

## Replacing Matches
1. Replace all occurrences:
```java
String result = matcher.replaceAll("replacement");
```
- **Time Complexity:** O(n) where n is the length of the input string

2. Replace the first occurrence:
```java
String result = matcher.replaceFirst("replacement");
```
- **Time Complexity:** O(n) where n is the length of the input string

## Splitting a String
1. Using Pattern:
```java
String[] result = pattern.split("inputString");
```
- **Time Complexity:** O(n) where n is the length of the input string

## Example Usage
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Main {
    public static void main(String[] args) {
        String input = "GitHub:123, GitLab:456";

        // Compile a Pattern
        Pattern pattern = Pattern.compile("(\\w+):(\\d+)");

        // Create a Matcher
        Matcher matcher = pattern.matcher(input);

        // Find and access match information
        while (matcher.find()) {
            System.out.println("Full match: " + matcher.group(0)); // Entire match
            System.out.println("Service: " + matcher.group(1));    // First capturing group
            System.out.println("ID: " + matcher.group(2));         // Second capturing group
        }

        // Replace all occurrences
        String result = matcher.replaceAll("$1 replaced");
        System.out.println("Replaced string: " + result);
    }
}
```

## Explanation of Pattern `"(\\w+):(\\d+)"`
1. `\\w+`:
   - `\\w` matches any word character (alphanumeric character plus underscore). 
   - The `+` quantifier means "one or more" of the preceding element. 
   - Therefore, `\\w+` matches a sequence of one or more word characters. 

2. `:`:
   - This matches the literal colon character `:`.

3. `\\d+`:
   - `\\d` matches any digit (0-9).
   - The `+` quantifier means "one or more" of the preceding element.
   - Therefore, `\\d+` matches a sequence of one or more digits.

## Capturing Groups
- `(\\w+)` is the first capturing group, which captures the sequence of word characters before the colon.
- `(\\d+)` is the second capturing group, which captures the sequence of digits after the colon.

### Example Matches
This pattern would match strings like:
- `"username:1234"`
- `"GitHub:5678"`
- `"Repo1:42"`



