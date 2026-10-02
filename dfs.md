````markdown
# Java DFS - Quick Reference

```java
import java.util.*;
```

**DFS (Depth-First Search)** follows one path as deeply as possible, then backtracks.

## 1. When to Use DFS

| Problem asks for | Use |
|---|---|
| Check whether a path exists | DFS |
| Visit every reachable node | DFS |
| Count connected components | DFS |
| Count islands or regions | DFS |
| Detect cycles | DFS |
| Tree traversal | DFS |
| Generate combinations or paths | DFS + backtracking |
| Shortest path in an unweighted graph | Prefer BFS |

> DFS does **not** guarantee the shortest path.

---

## 2. Recursive Graph DFS

```java
static void dfs(
        int node,
        List<List<Integer>> graph,
        boolean[] visited
) {
    // Mark immediately
    visited[node] = true;

    // Process node
    System.out.println(node);

    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            dfs(neighbor, graph, visited);
        }
    }
}
```

Call it:

```java
boolean[] visited = new boolean[graph.size()];
dfs(startNode, graph, visited);
```

### Basic flow

```text
Mark current node
Process current node
Visit every unvisited neighbor
Return when no neighbors remain
```

---

## 3. Iterative Graph DFS

Uses an explicit stack instead of recursion.

```java
static void dfs(
        int startNode,
        List<List<Integer>> graph
) {
    Deque<Integer> stack = new ArrayDeque<>();
    boolean[] visited = new boolean[graph.size()];

    stack.push(startNode);
    visited[startNode] = true;

    while (!stack.isEmpty()) {
        int node = stack.pop();

        // Process node
        System.out.println(node);

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                stack.push(neighbor);
            }
        }
    }
}
```

### Stack operations

| Operation | Meaning | Time |
|---|---|---:|
| `stack.push(x)` | Add to top | `O(1)` |
| `stack.pop()` | Remove and return top | `O(1)` |
| `stack.peek()` | Read top | `O(1)` |
| `stack.isEmpty()` | Check whether empty | `O(1)` |

Use:

```java
Deque<Integer> stack = new ArrayDeque<>();
```

instead of the older `Stack<Integer>` class.

---

## 4. When to Mark Visited

### Recursive DFS

Mark when entering the function:

```java
visited[node] = true;
```

### Iterative DFS

Mark when pushing:

```java
if (!visited[neighbor]) {
    visited[neighbor] = true;
    stack.push(neighbor);
}
```

Marking early prevents the same node from being added repeatedly.

---

## 5. Build an Adjacency List

```java
int numberOfNodes = 5;

List<List<Integer>> graph = new ArrayList<>();

for (int node = 0; node < numberOfNodes; node++) {
    graph.add(new ArrayList<>());
}
```

### Undirected edge

```java
graph.get(first).add(second);
graph.get(second).add(first);
```

### Directed edge

```java
graph.get(from).add(to);
```

---

## 6. Disconnected Graph

One DFS only visits the component containing its starting node.

```java
int components = 0;
boolean[] visited = new boolean[numberOfNodes];

for (int node = 0; node < numberOfNodes; node++) {
    if (!visited[node]) {
        dfs(node, graph, visited);
        components++;
    }
}
```

Each new DFS call discovers one connected component.

---

## 7. Path Exists

```java
static boolean pathExists(
        int node,
        int target,
        List<List<Integer>> graph,
        boolean[] visited
) {
    if (node == target) {
        return true;
    }

    visited[node] = true;

    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]
                && pathExists(neighbor, target, graph, visited)) {
            return true;
        }
    }

    return false;
}
```

---

## 8. Grid DFS

```java
static void dfs(
        int row,
        int col,
        int[][] grid,
        boolean[][] visited
) {
    int rows = grid.length;
    int columns = grid[0].length;

    // Invalid cell or stopping condition
    if (row < 0 || row >= rows
            || col < 0 || col >= columns
            || grid[row][col] == 0
            || visited[row][col]) {
        return;
    }

    visited[row][col] = true;

    dfs(row - 1, col, grid, visited); // Up
    dfs(row + 1, col, grid, visited); // Down
    dfs(row, col - 1, grid, visited); // Left
    dfs(row, col + 1, grid, visited); // Right
}
```

> Check boundaries before accessing `grid[row][col]`.

---

## 9. Grid DFS Using Directions

```java
static final int[][] DIRECTIONS = {
    {-1, 0},
    {1, 0},
    {0, -1},
    {0, 1}
};

static void dfs(
        int row,
        int col,
        int[][] grid,
        boolean[][] visited
) {
    visited[row][col] = true;

    for (int[] direction : DIRECTIONS) {
        int nextRow = row + direction[0];
        int nextCol = col + direction[1];

        if (nextRow >= 0 && nextRow < grid.length
                && nextCol >= 0 && nextCol < grid[0].length
                && grid[nextRow][nextCol] == 1
                && !visited[nextRow][nextCol]) {

            dfs(nextRow, nextCol, grid, visited);
        }
    }
}
```

---

## 10. Count Islands

```java
static int countIslands(int[][] grid) {
    int rows = grid.length;
    int columns = grid[0].length;

    boolean[][] visited = new boolean[rows][columns];
    int islands = 0;

    for (int row = 0; row < rows; row++) {
        for (int col = 0; col < columns; col++) {
            if (grid[row][col] == 1 && !visited[row][col]) {
                dfs(row, col, grid, visited);
                islands++;
            }
        }
    }

    return islands;
}
```

Each DFS visits one entire island.

---

## 11. Binary Tree DFS

```java
class TreeNode {
    int value;
    TreeNode left;
    TreeNode right;

    TreeNode(int value) {
        this.value = value;
    }
}
```

### Preorder: Node → Left → Right

```java
static void preorder(TreeNode node) {
    if (node == null) {
        return;
    }

    System.out.println(node.value);
    preorder(node.left);
    preorder(node.right);
}
```

### Inorder: Left → Node → Right

```java
static void inorder(TreeNode node) {
    if (node == null) {
        return;
    }

    inorder(node.left);
    System.out.println(node.value);
    inorder(node.right);
}
```

### Postorder: Left → Right → Node

```java
static void postorder(TreeNode node) {
    if (node == null) {
        return;
    }

    postorder(node.left);
    postorder(node.right);
    System.out.println(node.value);
}
```

A tree normally does not need a `visited` set because child edges do not point back to the parent.

---

## 12. Cycle Detection: Undirected Graph

Pass the parent because the edge returning to the parent is not a cycle.

```java
static boolean hasCycle(
        int node,
        int parent,
        List<List<Integer>> graph,
        boolean[] visited
) {
    visited[node] = true;

    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            if (hasCycle(neighbor, node, graph, visited)) {
                return true;
            }
        } else if (neighbor != parent) {
            return true;
        }
    }

    return false;
}
```

---

## 13. Cycle Detection: Directed Graph

Use three states:

```text
0 = unvisited
1 = visiting
2 = completely processed
```

```java
static boolean hasCycle(
        int node,
        List<List<Integer>> graph,
        int[] state
) {
    if (state[node] == 1) {
        return true;
    }

    if (state[node] == 2) {
        return false;
    }

    state[node] = 1;

    for (int neighbor : graph.get(node)) {
        if (hasCycle(neighbor, graph, state)) {
            return true;
        }
    }

    state[node] = 2;
    return false;
}
```

Finding an edge to a `visiting` node means a directed cycle exists.

---

## 14. DFS With Backtracking

Backtracking uses this pattern:

```text
Choose
Recurse
Undo the choice
```

### Generate subsets

```java
static void generateSubsets(
        int index,
        int[] numbers,
        List<Integer> current,
        List<List<Integer>> result
) {
    if (index == numbers.length) {
        result.add(new ArrayList<>(current));
        return;
    }

    // Choose the current number
    current.add(numbers[index]);

    generateSubsets(
        index + 1,
        numbers,
        current,
        result
    );

    // Undo the choice
    current.remove(current.size() - 1);

    // Skip the current number
    generateSubsets(
        index + 1,
        numbers,
        current,
        result
    );
}
```

Always copy a mutable path when storing it:

```java
result.add(new ArrayList<>(current));
```

Do not write:

```java
result.add(current);
```

because every result would reference the same mutable list.

---

## 15. Returning Information Upward

Example: height of a binary tree.

```java
static int height(TreeNode node) {
    if (node == null) {
        return 0;
    }

    int leftHeight = height(node.left);
    int rightHeight = height(node.right);

    return 1 + Math.max(leftHeight, rightHeight);
}
```

The recursive call returns information from the children back to the parent.

---

## 16. DFS Postorder and Topological Sort

For a directed acyclic graph:

```java
static void dfs(
        int node,
        List<List<Integer>> graph,
        boolean[] visited,
        List<Integer> order
) {
    visited[node] = true;

    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            dfs(neighbor, graph, visited, order);
        }
    }

    // Add after processing all neighbors
    order.add(node);
}
```

After all DFS calls:

```java
Collections.reverse(order);
```

Reverse DFS postorder gives a topological ordering only when the graph has no directed cycle.

---

## 17. DFS vs BFS

| Feature | DFS | BFS |
|---|---|---|
| Data structure | Recursion or stack | Queue |
| Exploration | Deep first | Level by level |
| Shortest unweighted path | Not guaranteed | Guaranteed |
| Connected components | Yes | Yes |
| Tree traversal | Yes | Yes |
| Backtracking problems | Commonly used | Rare |
| Time for graph | `O(V + E)` | `O(V + E)` |

---

## 18. Complexity

| Input | Time | Extra space |
|---|---:|---:|
| Graph with adjacency list | `O(V + E)` | `O(V)` |
| Graph with adjacency matrix | `O(V²)` | `O(V)` |
| `rows × columns` grid | `O(rows × columns)` | `O(rows × columns)` |
| Binary tree | `O(n)` | `O(height)` |

Recursive DFS space includes the recursion call stack.

A graph shaped like a long chain can produce recursion depth `O(V)` and may cause:

```text
StackOverflowError
```

Use iterative DFS when the graph may be extremely deep.

---

## 19. Common Mistakes

- Forgetting the `visited` set in a graph containing cycles.
- Marking a node too late.
- Forgetting disconnected components.
- Assuming DFS finds the shortest path.
- Accessing a grid cell before validating its coordinates.
- Missing the recursion base case.
- Forgetting to undo a backtracking choice.
- Saving the same mutable list instead of copying it.
- Using recursive DFS when the input depth may be extremely large.

---

## 20. Interview Checklist

```text
1. What does each node or state represent?
2. What is the base case?
3. Should I use recursion or an explicit stack?
4. How will I track visited nodes?
5. How do I generate neighbors?
6. Do I process before or after recursion?
7. Do I need to undo a choice?
8. Can the graph be disconnected?
9. What are the time and space complexities?
```

## Memory Rules

```text
Normal DFS:
Mark → Process → Explore → Return

Backtracking:
Choose → Explore → Undo

Recursive DFS:
Uses the call stack

Iterative DFS:
Uses an explicit stack

Need shortest unweighted path:
Use BFS
```
````
