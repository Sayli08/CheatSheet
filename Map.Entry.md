# Java `Map.Entry` — Quick Cheat Sheet

`Map.Entry<K, V>` represents **one key-value pair** from a map.

```text
"Sayli" -> 90
```

Here:

```text
Key   = "Sayli"
Value = 90
```

## Declaration

```java
Map.Entry<String, Integer> entry;
```

Get entries from a map:

```java
Set<Map.Entry<String, Integer>> entries = map.entrySet();
```

## Core API

| API | Purpose |
|---|---|
| `entry.getKey()` | Get the key |
| `entry.getValue()` | Get the value |
| `entry.setValue(newValue)` | Update the value in the original map |
| `entry.equals(other)` | Compare two entries |
| `entry.hashCode()` | Get entry hash code |

## Iterate Over Entries

```java
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    String key = entry.getKey();
    int value = entry.getValue();

    System.out.println(key + " -> " + value);
}
```

## Update Values

```java
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    entry.setValue(entry.getValue() + 5);
}
```

```text
90 → 95
85 → 90
```

`entry.setValue()` changes the value in the original map.

## `entrySet().forEach()`

```java
map.entrySet().forEach(entry -> {
    System.out.println(
        entry.getKey() + " -> " + entry.getValue()
    );
});
```

## `map.forEach()` vs `entrySet()`

| Method | Lambda/loop receives |
|---|---|
| `map.forEach((key, value) -> {})` | Key and value separately |
| `map.entrySet().forEach(entry -> {})` | One `Map.Entry` object |
| `for (... : map.entrySet())` | One `Map.Entry` object |

## Convert Entries to a List

Useful when entries need to be sorted:

```java
List<Map.Entry<String, Integer>> entries =
    new ArrayList<>(map.entrySet());
```

## Sort Entries

| Requirement | Comparator |
|---|---|
| Key ascending | `Map.Entry.comparingByKey()` |
| Value ascending | `Map.Entry.comparingByValue()` |
| Value descending | `Map.Entry.comparingByValue().reversed()` |

```java
entries.sort(Map.Entry.comparingByKey());
```

```java
entries.sort(Map.Entry.comparingByValue());
```

```java
entries.sort(
    Map.Entry.<String, Integer>comparingByValue()
        .reversed()
);
```

## Remove Entries

```java
map.entrySet().removeIf(
    entry -> entry.getValue() < 90
);
```

## Important Rules

| Rule | Explanation |
|---|---|
| `entrySet()` is backed by the map | Updating/removing entries changes the original map |
| Keys cannot be updated | There is no `entry.setKey()` |
| Values can be updated | Use `entry.setValue()` |
| HashMap entry order is unspecified | Do not depend on iteration order |
| Use a list for sorting | A `Set` cannot be sorted directly |

## Memory Rule

```text
entry.getKey()           → Read key
entry.getValue()         → Read value
entry.setValue(value)    → Update value

map.entrySet()           → All key-value entries
new ArrayList<>(entrySet) → Sortable entry list
```
