 ## Recursion — Concise Approach

| Step | What to think |
|---|---|
| **1. Define the function** | What should `solve(n)` return/do? |
| **2. Base case** | When should recursion stop? |
| **3. Make problem smaller** | Call the same function with a smaller input |
| **4. Recursive call** | `solve(smallerInput)` |
| **5. Return/combine** | Use the smaller result to build the current answer |

```java
int solve(int n) {

    // 1. Base case
    if (n == 0) {
        return 0;
    }

    // 2. Recursive relation
    return something + solve(n - 1);
}
```

### Memory trick

```text
BASE CASE
   ↓
MAKE INPUT SMALLER
   ↓
CALL YOURSELF
   ↓
RETURN / COMBINE RESULT
```

Most important:

> Every recursive call must move **toward the base case**.


That line means:

```java
return something + solve(n - 1);
```

- `solve(n - 1)` → solve the **smaller problem**
- `something + ...` → combine the smaller answer with the current work
- `return` → send that result back to the previous recursive call

Example:

```java
int sum(int n) {
    if (n == 0) return 0;

    return n + sum(n - 1);
}
```

For `sum(3)`:

```text
3 + sum(2)
3 + 2 + sum(1)
3 + 2 + 1 + sum(0)
= 6
```

So the pattern is:

```text
return currentWork + recursiveAnswer;
```
