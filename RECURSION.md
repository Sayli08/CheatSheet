
```text
                    RECURSION
        function calls itself on smaller problem
                     /        \
                    /          \
                   ↓            ↓
          BACKTRACKING       MEMOIZATION
          try choices        store repeated
          choose             subproblem results
          explore                 |
          undo                    ↓
                            DYNAMIC PROGRAMMING
                              /           \
                             /             \
                            ↓               ↓
                     TOP-DOWN           BOTTOM-UP
                   Memoization          Tabulation
                 recursion + cache      loop + table
                 big → small            small → big
```

| Concept | Remember |
|---|---|
| **Recursion** | Call itself with smaller problem + base case |
| **Backtracking** | Choose → Explore → Undo |
| **Memoization** | Recursion + remember answers |
| **Top-Down DP** | Memoization: big problem → smaller |
| **Bottom-Up DP** | Tabulation: solve small → build final |

**Key relationship:**  
**Backtracking uses recursion to explore choices.**  
**Memoization is Top-Down Dynamic Programming.**  
**Bottom-Up DP usually removes recursion and uses loops/table.**
