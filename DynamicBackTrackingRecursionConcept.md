
> **Dynamic Programming can use recursion or avoid recursion.**

- **Top-down DP:** recursion + data structure to store answers
- **Bottom-up DP:** loops + data structure to store answers
- Both store previously calculated subproblem answers.

## Correct Comparison Table

| Technique | Uses recursion? | Uses loops? | Uses a data structure? | What is stored? | Common data structures |
|---|---:|---:|---:|---|---|
| **Regular recursion** | **Yes** | Usually no | Not required | Nothing is cached; call stack remembers active calls | Call stack automatically |
| **Backtracking** | **Yes** | Often a loop inside recursion | Usually yes | Current choices/path and final results—not reusable subproblem answers | `ArrayList`, `StringBuilder`, `boolean[]`, `HashSet` |
| **Dynamic Programming** | **Maybe** | Maybe | **Yes** | Answers to previously solved subproblems | Array, 2D array, `HashMap` |
| **Top-down DP** | **Yes** | Sometimes | **Yes** | Answers calculated by recursive calls | `int[] memo`, `int[][] memo`, `HashMap<State, Answer>` |
| **Bottom-up DP** | **No** | **Yes** | **Yes** | Answers starting from the smallest states | `int[] dp`, `int[][] dp` |
| **Space-optimized DP** | **No** | **Yes** | Sometimes only variables | Only the few previous answers currently needed | Variables such as `previous` and `current` |

## Important Distinction

Not everything stored in a data structure makes a solution DP.

```text
Backtracking:
Stores the CURRENT PATH or choices.

Dynamic Programming:
Stores ANSWERS to repeated subproblems.
```

For example:

```java
// Backtracking: stores current choices
List<Integer> currentPath = new ArrayList<>();
```

```java
// Dynamic programming: stores calculated answers
int[] dp = new int[n + 1];
```

## Complete Relationship

```text
Recursion
│
├── Regular Recursion
│   ├── Uses recursion
│   └── Does not cache answers
│
├── Backtracking
│   ├── Uses recursion
│   ├── Stores the current path/choices
│   └── Choose → Recurse → Undo
│
└── Dynamic Programming
    ├── Stores answers to repeated subproblems
    │
    ├── Top-Down DP
    │   ├── Uses recursion
    │   └── Uses memoization/cache
    │
    └── Bottom-Up DP
        ├── Does not use recursion
        ├── Uses loops
        └── Uses a DP array/table
```

Strictly speaking, DP is not always “under recursion.” A more accurate chart is:

```text
Dynamic Programming
│
├── Top-Down DP
│   └── Recursion + Memoization
│
└── Bottom-Up DP
    └── Loops + Tabulation
```

## Same Problem Written Both Ways

### Top-Down DP: recursion + memo array

```java
static int fibonacci(int n, int[] memo) {
    if (n <= 1) {
        return n;
    }

    // Reuse previously calculated answer
    if (memo[n] != -1) {
        return memo[n];
    }

    memo[n] =
        fibonacci(n - 1, memo) +
        fibonacci(n - 2, memo);

    return memo[n];
}
```

Here:

```text
Recursion explores the states.
memo[] stores their answers.
```

### Bottom-Up DP: loop + DP array

```java
static int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }

    int[] dp = new int[n + 1];

    dp[0] = 0;
    dp[1] = 1;

    for (int index = 2; index <= n; index++) {
        dp[index] = dp[index - 1] + dp[index - 2];
    }

    return dp[n];
}
```

Here:

```text
The loop processes the states.
dp[] stores their answers.
No recursion is used.
```

## Space-Optimized Bottom-Up DP

Sometimes we do not need to store the entire DP array.

```java
static int fibonacci(int n) {
    if (n <= 1) {
        return n;
    }

    int previousTwo = 0;
    int previousOne = 1;

    for (int index = 2; index <= n; index++) {
        int current = previousOne + previousTwo;

        previousTwo = previousOne;
        previousOne = current;
    }

    return previousOne;
}
```

Here we store only the last two states:

```text
Time:  O(n)
Space: O(1)
```

## Final Memory Rule

| Technique | Remember it as |
|---|---|
| **Recursion** | Call the same method with a smaller input |
| **Backtracking** | Store choices: choose → recurse → undo |
| **Top-down DP** | Recursion stores answers in a cache |
| **Bottom-up DP** | Loops store answers in a table |
| **Optimized DP** | Loops store only the previous required answers |

```text
Path/choices stored        → Backtracking
Subproblem answers stored  → Dynamic Programming
Recursion + cache          → Top-down DP
Loop + table               → Bottom-up DP
```
