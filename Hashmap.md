# Java HashMap / Map - Quick Reference

```java
import java.util.*;
```

`Map<K, V>` stores **key-value pairs**.

- Keys are unique.
- Values may repeat.
- Putting an existing key replaces its old value.
- A `Map` is not a `Collection`; use `keySet()`, `values()`, or `entrySet()` to view its contents.

## 1. Declare the Right Map

```java
// Fast general-purpose map; no guaranteed order
Map<Integer, String> hashMap = new HashMap<>();

// Preserves insertion order
Map<Integer, String> linkedMap = new LinkedHashMap<>();

// Keeps keys sorted
Map<Integer, String> sortedMap = new TreeMap<>();

// Immutable map; rejects null keys and values
Map<String, Integer> fixedMap = Map.of("A", 1, "B", 2);

// Mutable copy
Map<String, Integer> mutableMap = new HashMap<>(fixedMap);
```

## 2. Core Operations

| Operation | Meaning / return | Average time |
|---|---|---:|
| `map.put(key, value)` | Insert or replace; returns old value or `null` | `O(1)` |
| `map.get(key)` | Return value or `null` | `O(1)` |
| `map.getOrDefault(key, defaultValue)` | Return value, otherwise the default | `O(1)` |
| `map.putIfAbsent(key, value)` | Insert only when key is missing | `O(1)` |
| `map.containsKey(key)` | Check whether key exists | `O(1)` |
| `map.containsValue(value)` | Search for a value | `O(n)` |
| `map.remove(key)` | Remove key; return old value or `null` | `O(1)` |
| `map.remove(key, value)` | Remove only if the exact pair exists | `O(1)` |
| `map.putAll(otherMap)` | Copy all entries | `O(m)` |
| `map.size()` / `map.isEmpty()` | Count entries / empty check | `O(1)` |
| `map.clear()` | Remove all entries | `O(n)` |

## 3. `putIfAbsent()` vs `getOrDefault()`

| Method | Use when | Does it modify the map? |
|---|---|---|
| `putIfAbsent()` | Add a key only if it does not exist | **Yes**, when absent |
| `getOrDefault()` | Read a value but use a fallback when missing | **No** |

### Initialize a list or object

```java
Map<Integer, List<Integer>> valuesByGroup = new HashMap<>();

valuesByGroup.putIfAbsent(groupId, new ArrayList<>());
valuesByGroup.get(groupId).add(value);
```

### Count frequency

```java
frequencyMap.put(
    number,
    frequencyMap.getOrDefault(number, 0) + 1
);
```

Shorter version:

```java
frequencyMap.merge(number, 1, Integer::sum);
```

> `getOrDefault(key, 0)` returns `0` when the key is missing, but it does **not** insert `key -> 0`.

## 4. High-Value Patterns

### Frequency map

```java
Map<Integer, Integer> frequencyMap = new HashMap<>();

for (int number : numbers) {
    frequencyMap.put(
        number,
        frequencyMap.getOrDefault(number, 0) + 1
    );
}
```

### Group values by key

```java
Map<String, List<Integer>> groups = new HashMap<>();

groups.computeIfAbsent(
    key,
    unusedKey -> new ArrayList<>()
).add(value);
```

`computeIfAbsent()` returns the existing value, or creates, inserts, and returns a new value.

### Store class objects as values

```java
Map<Integer, Athlete> athleteById = new HashMap<>();
athleteById.put(athlete.id, athlete);

Athlete selectedAthlete = athleteById.get(id);
```

## 5. Map Views and Iteration

### `entrySet()` - keys and values together

```java
Set<Map.Entry<String, Integer>> entries = map.entrySet();

for (Map.Entry<String, Integer> entry : map.entrySet()) {
    String key = entry.getKey();
    int value = entry.getValue();
}
```

### `keySet()` - keys only

```java
Set<String> keys = map.keySet();

for (String key : map.keySet()) {
    int value = map.get(key);
}
```

### `values()` - values only

```java
Collection<Integer> values = map.values();
```

### Lambda iteration

```java
map.forEach((key, value) -> {
    System.out.println(key + " -> " + value);
});
```

### Update an existing value while iterating

```java
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    entry.setValue(entry.getValue() + 1);
}
```

Do not structurally add or remove map entries inside an enhanced `for` loop. Use an iterator when removal is required.

## 6. Sorting

### Sort by key

```java
Map<String, Integer> sortedByKey = new TreeMap<>(map);
```

### Sort entries by value ascending

```java
List<Map.Entry<String, Integer>> entries =
    new ArrayList<>(map.entrySet());

entries.sort(Map.Entry.comparingByValue());
```

### Sort entries by value descending

```java
entries.sort(
    Map.Entry.<String, Integer>comparingByValue().reversed()
);
```

## 7. Nulls and Common Gotchas

- `HashMap` permits one `null` key and multiple `null` values.
- `LinkedHashMap` has the same null rules and preserves insertion order.
- `TreeMap` with natural ordering normally rejects `null` keys.
- `Map.of(...)` is immutable and rejects null keys and values.
- `map.get(key) == null` can mean either:
  - the key is missing, or
  - the key exists and maps to `null`.

Use `containsKey()` when that distinction matters:

```java
if (map.containsKey(key)) {
    Integer value = map.get(key);
}
```

## 8. Complexity Summary

| Map type | `get` / `put` / `remove` | Ordering |
|---|---:|---|
| `HashMap` | Average `O(1)` | No guaranteed order |
| `LinkedHashMap` | Average `O(1)` | Insertion order |
| `TreeMap` | `O(log n)` | Keys remain sorted |

Space complexity: **`O(n)`**.

## Memory Rules

```text
Need fast lookup?                 -> HashMap
Need insertion order?            -> LinkedHashMap
Need keys automatically sorted?  -> TreeMap
Need key + value during a loop?   -> entrySet()
Need keys only?                   -> keySet()
Need values only?                 -> values()
Need frequency counting?         -> getOrDefault() or merge()
Need to initialize a collection? -> putIfAbsent() or computeIfAbsent()
```
