# Split String by New Line

```java
String text = """
        Hello
        World
        Java
        """;

String[] lines = text.split("\n");
```

Result:

```text
["Hello", "World", "Java"]
```

More robust:

```java
String[] lines = text.split("\\R");
```

`\\R` = any line break.
