# Java Set — Quick Reference

```java
import java.util.*;
```

`Set<E>` stores **unique elements**.

- Duplicate elements are not allowed.
- A `Set` is a `Collection`.
- Sets do not provide index-based access.
- Ordering depends on the implementation.

## 1. Declare the Right Set

```java
// Fast general-purpose set; no guaranteed order
Set<Integer> hashSet = new HashSet<>();

// Preserves insertion order
Set<Integer> linkedSet = new LinkedHashSet<>();

// Keeps elements sorted
Set<Integer> sortedSet = new TreeSet<>();

// Immutable set
Set<Integer> fixedSet = Set.of(10, 20, 30);

// Mutable copy
Set<Integer> mutableSet = new HashSet<>(fixedSet);
```

## 2. Main Set Implementations

| Implementation | Ordering | Duplicates | `null` | Main operations |
|---|---|---:|---|---:|
| `HashSet` | No guaranteed order | No | One `null` allowed | Average `O(1)` |
| `LinkedHashSet` | Insertion order | No | One `null` allowed | Average `O(1)` |
| `TreeSet` | Sorted order | No | Normally not allowed | `O(log n)` |
| `EnumSet` | Enum declaration order | No | Not allowed | Very fast, usually `O(1)` |
| `CopyOnWriteArraySet` | Insertion order | No | Allowed | Reads fast; writes expensive |
| `Set.of(...)` | Unspecified | No | Not allowed | Immutable |

## 3. Core Set APIs

| Operation | Meaning | `HashSet` average | `TreeSet` |
|---|---|---:|---:|
| `set.add(value)` | Add value; return `false` if duplicate | `O(1)` | `O(log n)` |
| `set.remove(value)` | Remove value | `O(1)` | `O(log n)` |
| `set.contains(value)` | Check whether value exists | `O(1)` | `O(log n)` |
| `set.size()` | Number of elements | `O(1)` | `O(1)` |
| `set.isEmpty()` | Check whether empty | `O(1)` | `O(1)` |
| `set.clear()` | Remove everything | `O(n)` | `O(n)` |
| `set.addAll(other)` | Add all elements | Average `O(m)` | `O(m log n)` |
| `set.containsAll(other)` | Check whether all exist | Average `O(m)` | `O(m log n)` |
| `set.removeAll(other)` | Remove matching elements | Depends on set sizes | Depends |
| `set.retainAll(other)` | Keep only common elements | Depends on set sizes | Depends |
| `set.removeIf(condition)` | Remove matching elements | `O(n)` | `O(n)` |
| `set.toArray()` | Convert to array | `O(n)` | `O(n)` |

`n` = current set size, `m` = number of elements being processed.

## 4. Add, Check and Remove

```java
Set<Integer> numbers = new HashSet<>();

boolean addedFirst = numbers.add(10);   // true
boolean addedAgain = numbers.add(10);   // false: duplicate

boolean exists = numbers.contains(10);  // true
boolean removed = numbers.remove(10);   // true
```

`add()` is useful for detecting duplicates:

```java
if (!numbers.add(value)) {
    System.out.println("Duplicate: " + value);
}
```

## 5. Iteration

### Enhanced `for` loop

```java
for (int number : numbers) {
    System.out.println(number);
}
```

### `forEach()`

```java
numbers.forEach(number -> {
    System.out.println(number);
});
```

Short version:

```java
numbers.forEach(System.out::println);
```

### Iterator

```java
Iterator<Integer> iterator = numbers.iterator();

while (iterator.hasNext()) {
    int number = iterator.next();

    if (number < 0) {
        iterator.remove();
    }
}
```

Use `iterator.remove()` when removing elements during iteration.

## 6. Set Operations

Suppose:

```java
Set<Integer> first =
    new HashSet<>(Arrays.asList(1, 2, 3));

Set<Integer> second =
    new HashSet<>(Arrays.asList(3, 4, 5));
```

### Union — all elements

```text
{1, 2, 3} ∪ {3, 4, 5} = {1, 2, 3, 4, 5}
```

```java
Set<Integer> union = new HashSet<>(first);
union.addAll(second);
```

### Intersection — common elements

```text
{1, 2, 3} ∩ {3, 4, 5} = {3}
```

```java
Set<Integer> intersection = new HashSet<>(first);
intersection.retainAll(second);
```

### Difference — elements only in the first set

```text
{1, 2, 3} - {3, 4, 5} = {1, 2}
```

```java
Set<Integer> difference = new HashSet<>(first);
difference.removeAll(second);
```

### Subset check

```java
boolean isSubset = first.containsAll(smallerSet);
```

## 7. High-Value Patterns

### Detect duplicates

```java
Set<Integer> seen = new HashSet<>();

for (int number : numbers) {
    if (!seen.add(number)) {
        System.out.println("Duplicate: " + number);
    }
}
```

### Remove duplicates from a list

```java
List<Integer> numbers =
    Arrays.asList(3, 1, 3, 2, 1);

// No guaranteed order
Set<Integer> unique = new HashSet<>(numbers);
```

Preserve original order:

```java
Set<Integer> unique =
    new LinkedHashSet<>(numbers);
```

Convert back to a list:

```java
List<Integer> result = new ArrayList<>(unique);
```

### Track visited elements

```java
Set<String> visited = new HashSet<>();

if (visited.add(node)) {
    // node was not previously visited
}
```

### Find unique characters

```java
Set<Character> characters = new HashSet<>();

for (char character : text.toCharArray()) {
    characters.add(character);
}
```

## 8. `HashSet`

Best for fast lookup when ordering does not matter.

```java
Set<String> names = new HashSet<>();

names.add("Sayli");
names.add("Advik");
names.add("Sayli"); // Ignored
```

```text
Average add/contains/remove: O(1)
Worst case: O(n)
Space: O(n)
```

Iteration order is not guaranteed.

## 9. `LinkedHashSet`

Best when you need uniqueness and insertion order.

```java
Set<Integer> numbers = new LinkedHashSet<>();

numbers.add(30);
numbers.add(10);
numbers.add(20);
```

Iteration order:

```text
30, 10, 20
```

```text
Average add/contains/remove: O(1)
Space: O(n), with extra links for ordering
```

## 10. `TreeSet`

Best when elements must stay sorted.

```java
TreeSet<Integer> numbers = new TreeSet<>();

numbers.add(30);
numbers.add(10);
numbers.add(20);
```

Iteration order:

```text
10, 20, 30
```

```text
add/contains/remove: O(log n)
first/last: O(log n)
Space: O(n)
```

### Important `TreeSet` APIs

| API | Meaning |
|---|---|
| `set.first()` | Smallest element |
| `set.last()` | Largest element |
| `set.lower(x)` | Greatest element strictly `< x` |
| `set.floor(x)` | Greatest element `<= x` |
| `set.higher(x)` | Smallest element strictly `> x` |
| `set.ceiling(x)` | Smallest element `>= x` |
| `set.pollFirst()` | Remove and return smallest |
| `set.pollLast()` | Remove and return largest |
| `set.subSet(a, b)` | Elements from `a` inclusive to `b` exclusive |
| `set.headSet(x)` | Elements smaller than `x` |
| `set.tailSet(x)` | Elements greater than or equal to `x` |

### Example

```java
TreeSet<Integer> set =
    new TreeSet<>(Arrays.asList(10, 20, 30, 40));

set.first();       // 10
set.last();        // 40

set.lower(30);     // 20
set.floor(30);     // 30

set.higher(30);    // 40
set.ceiling(25);   // 30
```

## 11. Custom `TreeSet` Comparator

### Descending integers

```java
Set<Integer> descending =
    new TreeSet<>(Comparator.reverseOrder());
```

### Class objects

```java
Set<Athlete> athletes =
    new TreeSet<>(
        Comparator.comparingInt(athlete -> athlete.score)
    );
```

Score descending:

```java
Set<Athlete> athletes =
    new TreeSet<>(
        Comparator.comparingInt(
            (Athlete athlete) -> athlete.score
        ).reversed()
    );
```

### Tie-breaker

```java
Set<Athlete> athletes =
    new TreeSet<>((first, second) -> {

        // Score descending
        int result =
            Integer.compare(second.score, first.score);

        if (result != 0) {
            return result;
        }

        // Name ascending
        return first.name.compareTo(second.name);
    });
```

### Important `TreeSet` Rule

If the comparator returns `0`, `TreeSet` considers the elements duplicates.

```java
Comparator.comparingInt(athlete -> athlete.score)
```

Two athletes with the same score would be considered equal by the set, even if their names differ.

Use a tie-breaker when both should remain:

```java
Comparator
    .comparingInt((Athlete athlete) -> athlete.score)
    .thenComparing(athlete -> athlete.name);
```

## 12. `EnumSet`

Use only with enum values.

```java
enum Day {
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY
}
```

```java
EnumSet<Day> weekdays =
    EnumSet.range(Day.MONDAY, Day.FRIDAY);
```

Other declarations:

```java
EnumSet<Day> allDays = EnumSet.allOf(Day.class);

EnumSet<Day> noDays = EnumSet.noneOf(Day.class);

EnumSet<Day> weekend =
    EnumSet.of(Day.SATURDAY, Day.SUNDAY);
```

## 13. Immutable Sets

```java
Set<String> names =
    Set.of("Sayli", "Advik", "Sam");
```

Not allowed:

```java
names.add("Alex");    // UnsupportedOperationException
names.remove("Sam");  // UnsupportedOperationException
```

`Set.of()` also rejects:

- Duplicate values
- `null` values

Mutable copy:

```java
Set<String> mutableNames =
    new HashSet<>(names);
```

## 14. Set vs List vs Map

| Structure | Stores | Duplicates | Index/key access |
|---|---|---:|---|
| `List<E>` | Elements | Yes | By index |
| `Set<E>` | Unique elements | No | No index |
| `Map<K,V>` | Key-value pairs | Keys: no | By key |

## 15. Common Gotchas

### No index access

Invalid:

```java
set.get(0);
```

Convert to a list if index access is required:

```java
List<Integer> list = new ArrayList<>(set);
int first = list.get(0);
```

### Do not modify during enhanced iteration

Avoid:

```java
for (int number : set) {
    set.remove(number);
}
```

Use:

```java
set.removeIf(number -> number < 0);
```

Or use an iterator.

### Mutable objects in a `HashSet`

Do not change fields used by `equals()` or `hashCode()` after inserting an object into a `HashSet`.

```java
set.add(person);

// Dangerous if name is used by equals/hashCode
person.name = "Different Name";
```

The set may no longer find the object correctly.

## 16. Complexity Summary

| Set type | `add` | `contains` | `remove` | Ordering |
|---|---:|---:|---:|---|
| `HashSet` | Average `O(1)` | Average `O(1)` | Average `O(1)` | None |
| `LinkedHashSet` | Average `O(1)` | Average `O(1)` | Average `O(1)` | Insertion |
| `TreeSet` | `O(log n)` | `O(log n)` | `O(log n)` | Sorted |
| `EnumSet` | Usually `O(1)` | Usually `O(1)` | Usually `O(1)` | Enum declaration |

Space complexity: **`O(n)`**.

## Memory Rules

```text
Need fast lookup?                  → HashSet
Need insertion order?             → LinkedHashSet
Need automatically sorted values? → TreeSet
Need enum values?                 → EnumSet

Need to detect a duplicate?       → !set.add(value)
Need all elements?                → addAll()
Need common elements?             → retainAll()
Need only first-set elements?     → removeAll()
Need to remove by condition?      → removeIf()
Need index access?                → Convert Set to List
```
