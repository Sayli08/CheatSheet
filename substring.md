## Java `substring()` — Inclusive vs Exclusive

Syntax:

```java
str.substring(start, end)
```

- `start` index is **inclusive**
- `end` index is **exclusive**

Example:

```java
String s = "GitHub";
//          012345

s.substring(0, 3);   // "Git"
```

Why?

```text
start = 0 → include index 0
end   = 3 → stop before index 3
```

So it takes:

```text
index: 0 1 2
char : G i t
```

### Important: `substring(0, 0)`

```java
s.substring(0, 0);
```

This is **valid Java**, but it returns:

```java
""
```

an **empty string**.

Why?

```text
Start at index 0
Stop before index 0
→ there are no characters to take
```

So:

```java
s.substring(0, 0);   // ""
s.substring(0, 1);   // "G"
s.substring(0, 2);   // "Gi"
s.substring(1, 3);   // "it"
```

### Easy rule

```text
substring(i, j)

takes characters from:

i → j - 1
```

Number of characters returned:

```text
j - i
```

Example:

```java
s.substring(2, 5);
```

takes:

```text
2, 3, 4
```

and returns `5 - 2 = 3` characters.

### Interview memory trick

```text
[start, end)

[  → included
)  → excluded
```

So Java substring behaves like:

```text
[start, end)
```
