# Java PriorityQueue - Quick Reference

```java
import java.util.*;
```

`PriorityQueue<E>` is a heap that keeps the **highest-priority element at the top**.

- Java uses a **min-heap by default** when elements have natural ordering.
- `peek()` returns the top element without removing it.
- `poll()` returns and removes the top element.
- The heap contains every element, but **only the top is guaranteed**.
- The remaining elements follow heap order and are **not completely sorted**.

## 1. Min Heap and Max Heap

| Requirement | Declaration | Top of heap |
|---|---|---|
| Integer min-heap | `new PriorityQueue<>()` | Smallest integer |
| Integer max-heap | `new PriorityQueue<>(Collections.reverseOrder())` | Largest integer |

```java
// MIN HEAP - smallest value at top
PriorityQueue<Integer> minHeap =
    new PriorityQueue<>();

// MAX HEAP - largest value at top
PriorityQueue<Integer> maxHeap =
    new PriorityQueue<>(Collections.reverseOrder());
```

## 2. Core Operations

| Operation | Example | Return | Time |
|---|---|---|---:|
| Insert | `pq.offer(value)` | `boolean` | `O(log n)` |
| Insert | `pq.add(value)` | `boolean` | `O(log n)` |
| Read top | `pq.peek()` | Top or `null` | `O(1)` |
| Remove top | `pq.poll()` | Top or `null` | `O(log n)` |
| Count elements | `pq.size()` | `int` | `O(1)` |
| Check empty | `pq.isEmpty()` | `boolean` | `O(1)` |
| Find a value | `pq.contains(value)` | `boolean` | `O(n)` |
| Remove a specific value | `pq.remove(value)` | `boolean` | `O(n)` |
| Remove everything | `pq.clear()` | `void` | `O(n)` |

### Empty PriorityQueue

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();

pq.peek(); // null
pq.poll(); // null
```

| Safe on empty queue | Throws on empty queue |
|---|---|
| `peek()` returns `null` | `element()` throws `NoSuchElementException` |
| `poll()` returns `null` | `remove()` throws `NoSuchElementException` |

For primitive assignment, check for `null` first:

```java
Integer top = pq.poll();
int value = top == null ? 0 : top;
```

> `poll()` itself does **not** return `0`; it returns `null` when empty.

## 3. Building a PriorityQueue

| Method | What happens | Time |
|---|---|---:|
| `pq.offer(x)` | Insert one item and sift up | `O(log n)` |
| `n` calls to `offer()` | Repeat insertion `n` times | `O(n log n)` |
| `new PriorityQueue<>(collection)` | Bottom-up heap construction | `O(n)` |
| `pq.addAll(collection)` | Adds elements through repeated insertion | Usually `O(m log(n + m))` |

```java
List<Integer> values =
    Arrays.asList(5, 2, 8, 1);

// Bottom-up heap construction
PriorityQueue<Integer> minHeap =
    new PriorityQueue<>(values);
```

## 4. How a Comparator Works

```java
(first, second) ->
    Integer.compare(first, second)
```

| Comparator result | Meaning |
|---:|---|
| Negative | `first` comes before `second` |
| Zero | They tie in comparator order |
| Positive | `first` comes after `second` |

### Direction Rule

```java
// MIN: first compared with second
Integer.compare(first, second);

// MAX: reverse the arguments
Integer.compare(second, first);
```

Avoid subtraction:

```java
// Avoid: may overflow
(first, second) -> first - second

// Safe
(first, second) ->
    Integer.compare(first, second)
```

## 5. Natural Types

### Integer

```java
PriorityQueue<Integer> minHeap =
    new PriorityQueue<>();

PriorityQueue<Integer> maxHeap =
    new PriorityQueue<>(
        Collections.reverseOrder()
    );
```

### String

```java
// Alphabetically smallest string first
PriorityQueue<String> minHeap =
    new PriorityQueue<>();

// Alphabetically largest string first
PriorityQueue<String> maxHeap =
    new PriorityQueue<>(
        Collections.reverseOrder()
    );
```

### Character

```java
PriorityQueue<Character> minHeap =
    new PriorityQueue<>();

PriorityQueue<Character> maxHeap =
    new PriorityQueue<>(
        Collections.reverseOrder()
    );
```

`Integer`, `String`, and `Character` implement `Comparable`, so Java already knows their natural ordering.

## 6. Heap Stores Indices but Compares `score[]`

The heap contains indices:

```java
PriorityQueue<Integer>
```

The comparator uses each index to read its score.

### Minimum score first

```java
PriorityQueue<Integer> minHeap =
    new PriorityQueue<>(
        (firstIndex, secondIndex) ->
            Integer.compare(
                score[firstIndex],
                score[secondIndex]
            )
    );
```

`peek()` returns the index having the smallest score.

### Maximum score first

```java
PriorityQueue<Integer> maxHeap =
    new PriorityQueue<>(
        (firstIndex, secondIndex) ->
            Integer.compare(
                score[secondIndex],
                score[firstIndex]
            )
    );
```

`peek()` returns the index having the largest score.

> Without the comparator, Java compares the integer indices themselves, not `score[index]`.

## 7. Why `int[]` Needs a Comparator

This works without a comparator:

```java
PriorityQueue<Integer> minHeap =
    new PriorityQueue<>();
```

`Integer` has natural ordering.

But an array does not implement `Comparable`:

```java
int[] pair = {value, index};
```

Java does not know whether it should compare `pair[0]` or `pair[1]`.

```java
// MIN HEAP based on value
PriorityQueue<int[]> minHeap =
    new PriorityQueue<>(
        (first, second) ->
            Integer.compare(
                first[0],
                second[0]
            )
    );
```

```text
pair[0] = value
pair[1] = index
```

### Array Comparator Table

| Requirement | Comparator | Top |
|---|---|---|
| Value ascending | `Integer.compare(a[0], b[0])` | Smallest value |
| Value descending | `Integer.compare(b[0], a[0])` | Largest value |
| Index ascending | `Integer.compare(a[1], b[1])` | Smallest index |
| Index descending | `Integer.compare(b[1], a[1])` | Largest index |

## 8. Class Objects

```java
class Athlete {
    String name;
    int score;
}
```

### Score ascending

```java
PriorityQueue<Athlete> minHeap =
    new PriorityQueue<>(
        Comparator.comparingInt(
            athlete -> athlete.score
        )
    );
```

### Score descending

```java
PriorityQueue<Athlete> maxHeap =
    new PriorityQueue<>(
        Comparator.comparingInt(
            (Athlete athlete) -> athlete.score
        ).reversed()
    );
```

### Lambda style

```java
// Score ascending
PriorityQueue<Athlete> minHeap =
    new PriorityQueue<>(
        (first, second) ->
            Integer.compare(
                first.score,
                second.score
            )
    );

// Score descending
PriorityQueue<Athlete> maxHeap =
    new PriorityQueue<>(
        (first, second) ->
            Integer.compare(
                second.score,
                first.score
            )
    );
```

## 9. Tie-Breakers

A tie-breaker decides what happens when the primary values are equal.

### Score descending, name ascending

```java
PriorityQueue<Athlete> heap =
    new PriorityQueue<>((first, second) -> {

        // Primary: larger score first
        int byScore = Integer.compare(
            second.score,
            first.score
        );

        if (byScore != 0) {
            return byScore;
        }

        // Tie-breaker:
        // alphabetically smaller name first
        return first.name.compareTo(
            second.name
        );
    });
```

For:

```text
Amy: 100
Zoe: 100
Sam: 90
```

Poll order:

```text
Amy: 100
Zoe: 100
Sam: 90
```

The score rule is checked first. The name rule is used only when scores tie.

### Comparator utility style

```java
PriorityQueue<Athlete> heap =
    new PriorityQueue<>(
        Comparator.comparingInt(
            (Athlete athlete) ->
                athlete.score
        )
        .reversed()
        .thenComparing(
            athlete -> athlete.name
        )
    );
```

## 10. Map Entries in a PriorityQueue

Suppose:

```java
Map<Integer, Integer> rowToScore =
    new HashMap<>();
```

```text
key   = row number
value = score
```

The heap contains `Map.Entry<Integer, Integer>` objects, not the entire map.

### Weakest first: score ascending, row ascending on tie

```java
PriorityQueue<
    Map.Entry<Integer, Integer>
> minHeap =
    new PriorityQueue<>((first, second) -> {

        int byScore = Integer.compare(
            first.getValue(),
            second.getValue()
        );

        if (byScore != 0) {
            return byScore;
        }

        return Integer.compare(
            first.getKey(),
            second.getKey()
        );
    });

minHeap.addAll(rowToScore.entrySet());
```

Poll returns an entry:

```java
Map.Entry<Integer, Integer> entry =
    minHeap.poll();

int row = entry.getKey();
int score = entry.getValue();
```

### Strongest first: score descending, larger row wins tie

```java
PriorityQueue<
    Map.Entry<Integer, Integer>
> maxHeap =
    new PriorityQueue<>((first, second) -> {

        int byScore = Integer.compare(
            second.getValue(),
            first.getValue()
        );

        if (byScore != 0) {
            return byScore;
        }

        return Integer.compare(
            second.getKey(),
            first.getKey()
        );
    });

maxHeap.addAll(rowToScore.entrySet());
```

## 11. Frequency Map to PriorityQueue

```java
Map<Integer, Integer> frequencyMap =
    new HashMap<>();
```

```text
key   = number
value = frequency
```

Requirement:

1. Larger frequency is better.
2. If frequencies tie, the larger number is better.

```java
PriorityQueue<
    Map.Entry<Integer, Integer>
> maxHeap =
    new PriorityQueue<>((first, second) -> {

        int byFrequency = Integer.compare(
            second.getValue(),
            first.getValue()
        );

        if (byFrequency != 0) {
            return byFrequency;
        }

        return Integer.compare(
            second.getKey(),
            first.getKey()
        );
    });

maxHeap.addAll(frequencyMap.entrySet());
```

Take the top `x` distinct numbers:

```java
int currentXSum = 0;

for (int count = 0;
     count < x && !maxHeap.isEmpty();
     count++) {

    Map.Entry<Integer, Integer> entry =
        maxHeap.poll();

    int number = entry.getKey();
    int frequency = entry.getValue();

    currentXSum += number * frequency;
}
```

Example:

```text
frequencyMap = {2=3, 4=2, 5=2}

Poll order:
(2,3), (5,2), (4,2)

For x = 2:
2*3 + 5*2 = 16
```

## 12. What Does the Heap Contain?

| Declaration | Stored item | `peek()` / `poll()` returns |
|---|---|---|
| `PriorityQueue<Integer>` | Integer | `Integer` |
| `PriorityQueue<String>` | String | `String` |
| `PriorityQueue<int[]>` | Array reference | `int[]` |
| `PriorityQueue<Athlete>` | Athlete object | `Athlete` |
| `PriorityQueue<Map.Entry<K,V>>` | Map entry | `Map.Entry<K,V>` |

```java
int index = indexHeap.peek();

Athlete athlete =
    athleteHeap.peek();

int[] pair =
    pairHeap.peek();

Map.Entry<Integer, Integer> entry =
    entryHeap.peek();
```

## 13. Comparator Summary

| Stored type | Min / ascending | Max / descending |
|---|---|---|
| `Integer` | `new PriorityQueue<>()` | `new PriorityQueue<>(Collections.reverseOrder())` |
| `String` | `new PriorityQueue<>()` | `new PriorityQueue<>(Collections.reverseOrder())` |
| `int[]` by value | `Integer.compare(a[0], b[0])` | `Integer.compare(b[0], a[0])` |
| Index by `score[]` | `Integer.compare(score[a], score[b])` | `Integer.compare(score[b], score[a])` |
| Object by score | `Integer.compare(a.score, b.score)` | `Integer.compare(b.score, a.score)` |
| Map entry by value | `Integer.compare(a.getValue(), b.getValue())` | `Integer.compare(b.getValue(), a.getValue())` |

## 14. Important Gotchas

- `PriorityQueue` does not permit `null` elements.
- Iterating over a heap does not produce sorted order.
- Only `peek()` and `poll()` expose the current highest-priority element.
- To obtain fully sorted output, repeatedly call `poll()`.
- `contains(value)` and `remove(value)` are `O(n)`.
- If an object's priority changes after insertion, the heap does not automatically reorder it.
- Remove and reinsert an object after changing its priority.
- Use `Integer.compare()` instead of subtraction to avoid overflow.

## Memory Rules

```text
Default PriorityQueue
    -> Min-heap

Collections.reverseOrder()
    -> Max-heap

Min comparator
    -> compare(first, second)

Max comparator
    -> compare(second, first)

Only the top is guaranteed
    -> Remaining elements are not sorted

Empty peek() / poll()
    -> null

Array or custom object
    -> Comparator required unless Comparable

Primary values tie
    -> Apply a tie-breaker

Map into heap
    -> addAll(map.entrySet())

Need sorted output
    -> Repeatedly poll()
```
