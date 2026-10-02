# Java BFS — Quick Reference

```java
import java.util.*;
```

BFS means **Breadth-First Search**.

It explores nodes **level by level** using a **queue**.

```text
Start
  ↓
Visit all nodes 1 step away
  ↓
Visit all nodes 2 steps away
  ↓
Continue level by level
```

## 1. When to Use BFS

Look for:

- Shortest path in an **unweighted graph**
- Minimum number of moves or steps
- Level-order traversal
- Nodes at distance `k`
- Closest destination
- Spread or infection problems
- Grid traversal
- Multiple starting points
- Words such as:
  - “minimum steps”
  - “shortest path”
  - “nearest”
  - “fewest moves”
  - “level by level”

## 2. Data Structures

| Purpose | Data structure |
|---|---|
| Nodes waiting to be processed | `Queue` |
| Prevent duplicate visits | `HashSet` or `boolean[]` |
| Graph connections | Adjacency list |
| Grid directions | Direction array |
| Distance | `int[]`, `Map`, or queue state |

```java
Queue<Integer> queue = new ArrayDeque<>();
Set<Integer> visited = new HashSet<>();
```

Prefer:

```java
Queue<Integer> queue = new ArrayDeque<>();
```

instead of:

```java
Queue<Integer> queue = new LinkedList<>();
```

## 3. Queue APIs

| Operation | Syntax | Time |
|---|---|---:|
| Add to back | `queue.offer(value)` | `O(1)` |
| Remove from front | `queue.poll()` | `O(1)` |
| Read front | `queue.peek()` | `O(1)` |
| Check empty | `queue.isEmpty()` | `O(1)` |
| Number of items | `queue.size()` | `O(1)` |

```text
BFS removes from the front
and adds new nodes to the back.
```

## 4. Basic BFS Steps

```text
1. Add the starting node to the queue.
2. Mark the starting node visited.
3. While the queue is not empty:
      a. Remove one node.
      b. Process it.
      c. Visit its neighbors.
      d. Add unvisited neighbors to the queue.
      e. Mark them visited immediately.
```

## 5. Basic Graph BFS Template

```java
static void bfs(
        int start,
        List<List<Integer>> graph) {

    Queue<Integer> queue = new ArrayDeque<>();
    boolean[] visited = new boolean[graph.size()];

    queue.offer(start);
    visited[start] = true;

    while (!queue.isEmpty()) {

        int current = queue.poll();

        // Process current node
        System.out.println(current);

        for (int neighbor : graph.get(current)) {

            if (!visited[neighbor]) {

                // Mark when adding to queue
                visited[neighbor] = true;
                queue.offer(neighbor);
            }
        }
    }
}
```

## 6. Why Mark Visited When Enqueuing?

Correct:

```java
if (!visited[neighbor]) {
    visited[neighbor] = true;
    queue.offer(neighbor);
}
```

Avoid marking only after `poll()`:

```java
int current = queue.poll();
visited[current] = true;
```

If marking is delayed, multiple nodes may add the same neighbor to the queue.

Example:

```text
A → C
B → C
```

Both `A` and `B` may enqueue `C`.

Memory rule:

```text
ENQUEUE → MARK VISITED IMMEDIATELY
```

## 7. Graph BFS with a `HashSet`

Use this when nodes are strings, URLs, objects, or unknown IDs.

```java
static void bfs(
        String start,
        Map<String, List<String>> graph) {

    Queue<String> queue = new ArrayDeque<>();
    Set<String> visited = new HashSet<>();

    queue.offer(start);
    visited.add(start);

    while (!queue.isEmpty()) {

        String current = queue.poll();

        System.out.println(current);

        for (String neighbor :
                graph.getOrDefault(
                    current,
                    Collections.emptyList()
                )) {

            if (visited.add(neighbor)) {
                queue.offer(neighbor);
            }
        }
    }
}
```

This works because:

```java
visited.add(neighbor)
```

returns:

```text
true  → neighbor was not already present
false → neighbor was already visited
```

## 8. Build an Adjacency List

### Undirected graph

```java
int numberOfNodes = 5;

List<List<Integer>> graph =
    new ArrayList<>();

for (int node = 0;
     node < numberOfNodes;
     node++) {

    graph.add(new ArrayList<>());
}

for (int[] edge : edges) {

    int first = edge[0];
    int second = edge[1];

    graph.get(first).add(second);
    graph.get(second).add(first);
}
```

### Directed graph

```java
for (int[] edge : edges) {
    int from = edge[0];
    int to = edge[1];

    graph.get(from).add(to);
}
```

## 9. BFS Traversal Example

Graph:

```text
0 → 1, 2
1 → 3
2 → 4
3 → none
4 → none
```

Queue flow:

| Step | Remove | Add | Queue after step |
|---:|---:|---|---|
| Start | — | `0` | `[0]` |
| 1 | `0` | `1, 2` | `[1, 2]` |
| 2 | `1` | `3` | `[2, 3]` |
| 3 | `2` | `4` | `[3, 4]` |
| 4 | `3` | Nothing | `[4]` |
| 5 | `4` | Nothing | `[]` |

Traversal:

```text
0, 1, 2, 3, 4
```

## 10. Level-by-Level BFS

Use `queue.size()` to find how many nodes belong to the current level.

```java
static void bfsByLevel(
        int start,
        List<List<Integer>> graph) {

    Queue<Integer> queue = new ArrayDeque<>();
    boolean[] visited = new boolean[graph.size()];

    queue.offer(start);
    visited[start] = true;

    int level = 0;

    while (!queue.isEmpty()) {

        int levelSize = queue.size();

        for (int count = 0;
             count < levelSize;
             count++) {

            int current = queue.poll();

            System.out.println(
                "Node: " + current +
                ", Level: " + level
            );

            for (int neighbor :
                    graph.get(current)) {

                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.offer(neighbor);
                }
            }
        }

        level++;
    }
}
```

Important:

```java
int levelSize = queue.size();
```

must be calculated **before** processing the level.

New neighbors added during the loop belong to the next level.

## 11. Binary Tree Level-Order BFS

```java
class TreeNode {
    int value;
    TreeNode left;
    TreeNode right;
}
```

```java
static List<List<Integer>> levelOrder(
        TreeNode root) {

    List<List<Integer>> result =
        new ArrayList<>();

    if (root == null) {
        return result;
    }

    Queue<TreeNode> queue =
        new ArrayDeque<>();

    queue.offer(root);

    while (!queue.isEmpty()) {

        int levelSize = queue.size();

        List<Integer> currentLevel =
            new ArrayList<>();

        for (int count = 0;
             count < levelSize;
             count++) {

            TreeNode current = queue.poll();

            currentLevel.add(current.value);

            if (current.left != null) {
                queue.offer(current.left);
            }

            if (current.right != null) {
                queue.offer(current.right);
            }
        }

        result.add(currentLevel);
    }

    return result;
}
```

## 12. Shortest Path in an Unweighted Graph

BFS finds the shortest path by number of edges.

```java
static int shortestPath(
        int start,
        int destination,
        List<List<Integer>> graph) {

    Queue<Integer> queue = new ArrayDeque<>();
    boolean[] visited = new boolean[graph.size()];
    int[] distance = new int[graph.size()];

    queue.offer(start);
    visited[start] = true;
    distance[start] = 0;

    while (!queue.isEmpty()) {

        int current = queue.poll();

        if (current == destination) {
            return distance[current];
        }

        for (int neighbor :
                graph.get(current)) {

            if (!visited[neighbor]) {

                visited[neighbor] = true;

                distance[neighbor] =
                    distance[current] + 1;

                queue.offer(neighbor);
            }
        }
    }

    return -1;
}
```

Why does the first destination found give the shortest path?

```text
BFS explores distance 0,
then distance 1,
then distance 2,
and so on.
```

## 13. Store Distance Inside the Queue

```java
Queue<int[]> queue = new ArrayDeque<>();

// {node, distance}
queue.offer(new int[]{start, 0});

while (!queue.isEmpty()) {

    int[] state = queue.poll();

    int node = state[0];
    int distance = state[1];

    for (int neighbor : graph.get(node)) {

        if (!visited[neighbor]) {
            visited[neighbor] = true;

            queue.offer(
                new int[]{
                    neighbor,
                    distance + 1
                }
            );
        }
    }
}
```

## 14. Grid BFS

Use BFS when moving through a matrix.

```java
int[][] directions = {
    {-1, 0}, // up
    {1, 0},  // down
    {0, -1}, // left
    {0, 1}   // right
};
```

```java
static void bfsGrid(
        int[][] grid,
        int startRow,
        int startColumn) {

    int rows = grid.length;
    int columns = grid[0].length;

    boolean[][] visited =
        new boolean[rows][columns];

    Queue<int[]> queue =
        new ArrayDeque<>();

    queue.offer(
        new int[]{startRow, startColumn}
    );

    visited[startRow][startColumn] = true;

    int[][] directions = {
        {-1, 0},
        {1, 0},
        {0, -1},
        {0, 1}
    };

    while (!queue.isEmpty()) {

        int[] current = queue.poll();

        int row = current[0];
        int column = current[1];

        for (int[] direction : directions) {

            int newRow =
                row + direction[0];

            int newColumn =
                column + direction[1];

            if (newRow < 0 ||
                newRow >= rows ||
                newColumn < 0 ||
                newColumn >= columns) {

                continue;
            }

            if (visited[newRow][newColumn]) {
                continue;
            }

            if (grid[newRow][newColumn] == 0) {
                continue;
            }

            visited[newRow][newColumn] = true;

            queue.offer(
                new int[]{newRow, newColumn}
            );
        }
    }
}
```

## 15. Grid Validation Checklist

For every neighboring cell, check:

```text
1. Is the row inside the grid?
2. Is the column inside the grid?
3. Is the cell allowed?
4. Has the cell already been visited?
```

Typical condition:

```java
if (newRow >= 0 &&
    newRow < rows &&
    newColumn >= 0 &&
    newColumn < columns &&
    grid[newRow][newColumn] != 0 &&
    !visited[newRow][newColumn]) {

    visited[newRow][newColumn] = true;

    queue.offer(
        new int[]{newRow, newColumn}
    );
}
```

## 16. Shortest Path in a Grid

```java
static int shortestPath(
        int[][] grid,
        int startRow,
        int startColumn,
        int targetRow,
        int targetColumn) {

    int rows = grid.length;
    int columns = grid[0].length;

    boolean[][] visited =
        new boolean[rows][columns];

    Queue<int[]> queue =
        new ArrayDeque<>();

    // {row, column, distance}
    queue.offer(
        new int[]{
            startRow,
            startColumn,
            0
        }
    );

    visited[startRow][startColumn] = true;

    int[][] directions = {
        {-1, 0},
        {1, 0},
        {0, -1},
        {0, 1}
    };

    while (!queue.isEmpty()) {

        int[] current = queue.poll();

        int row = current[0];
        int column = current[1];
        int distance = current[2];

        if (row == targetRow &&
            column == targetColumn) {

            return distance;
        }

        for (int[] direction : directions) {

            int newRow =
                row + direction[0];

            int newColumn =
                column + direction[1];

            if (newRow < 0 ||
                newRow >= rows ||
                newColumn < 0 ||
                newColumn >= columns ||
                grid[newRow][newColumn] == 0 ||
                visited[newRow][newColumn]) {

                continue;
            }

            visited[newRow][newColumn] = true;

            queue.offer(
                new int[]{
                    newRow,
                    newColumn,
                    distance + 1
                }
            );
        }
    }

    return -1;
}
```

## 17. Multi-Source BFS

Use multi-source BFS when several starting positions spread simultaneously.

Examples:

- Rotting oranges
- Fire spreading
- Distance to nearest zero
- Multiple gates
- Multiple infection sources

Add **all starting positions** before beginning BFS:

```java
Queue<int[]> queue =
    new ArrayDeque<>();

for (int row = 0;
     row < rows;
     row++) {

    for (int column = 0;
         column < columns;
         column++) {

        if (grid[row][column] == SOURCE) {

            queue.offer(
                new int[]{row, column}
            );

            visited[row][column] = true;
        }
    }
}
```

Then run normal BFS.

```text
All sources begin at distance 0.
```

## 18. Return the Actual Shortest Path

Use a parent map or parent array.

```java
int[] parent = new int[numberOfNodes];
Arrays.fill(parent, -1);
```

When discovering a neighbor:

```java
parent[neighbor] = current;
```

Reconstruct the path:

```java
List<Integer> path = new ArrayList<>();

int current = destination;

while (current != -1) {
    path.add(current);
    current = parent[current];
}

Collections.reverse(path);
```

## 19. Disconnected Graph

Starting BFS from one node visits only its connected component.

To visit the entire graph:

```java
boolean[] visited =
    new boolean[graph.size()];

for (int node = 0;
     node < graph.size();
     node++) {

    if (!visited[node]) {
        bfsComponent(
            node,
            graph,
            visited
        );
    }
}
```

```java
static void bfsComponent(
        int start,
        List<List<Integer>> graph,
        boolean[] visited) {

    Queue<Integer> queue =
        new ArrayDeque<>();

    queue.offer(start);
    visited[start] = true;

    while (!queue.isEmpty()) {

        int current = queue.poll();

        for (int neighbor :
                graph.get(current)) {

            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.offer(neighbor);
            }
        }
    }
}
```

## 20. Time and Space Complexity

### Graph BFS

```text
V = number of vertices
E = number of edges
```

| Measurement | Complexity |
|---|---:|
| Time | `O(V + E)` |
| Queue space | `O(V)` |
| Visited space | `O(V)` |
| Total auxiliary space | `O(V)` |

Each node is visited once, and each edge is examined once.

For an undirected graph, every edge appears twice in the adjacency list, but the total is still:

```text
O(V + E)
```

### Grid BFS

```text
R = rows
C = columns
```

| Measurement | Complexity |
|---|---:|
| Time | `O(R × C)` |
| Space | `O(R × C)` |

Each cell is added to the queue at most once.

## 21. BFS vs DFS

| BFS | DFS |
|---|---|
| Uses a queue | Uses recursion or stack |
| Explores level by level | Explores one path deeply |
| Finds shortest unweighted path | Does not guarantee shortest path |
| Good for minimum steps | Good for exhaustive exploration |
| Space can be wide | Space depends on depth |

## 22. Common Mistakes

### Marking visited too late

```java
// Correct
visited[neighbor] = true;
queue.offer(neighbor);
```

### Forgetting the start node

```java
queue.offer(start);
visited[start] = true;
```

### Using BFS for weighted shortest path

Normal BFS works when every edge has the same cost.

```text
Unweighted/equal weights → BFS
Different positive weights → Dijkstra
Negative weights → Bellman-Ford
```

### Recalculating `queue.size()` during a level

Correct:

```java
int levelSize = queue.size();

for (int count = 0;
     count < levelSize;
     count++) {

    // Process only this level
}
```

### Forgetting grid bounds

Always validate row and column before accessing:

```java
grid[newRow][newColumn]
```

## 23. Interview Explanation

```text
I will use BFS because the problem asks for the minimum
number of steps in an unweighted graph.

I will maintain a queue for nodes waiting to be processed
and a visited set to prevent duplicates and cycles.

I will mark a node visited when I add it to the queue.

Because BFS processes nodes level by level, the first time
I reach the destination gives the shortest path.
```

## Memory Rules

```text
BFS data structure
    → Queue

Add
    → offer()

Remove front
    → poll()

Read front
    → peek()

Prevent duplicates
    → visited set or boolean array

Mark visited
    → When enqueuing, not when polling

Process one level
    → levelSize = queue.size()

Shortest path
    → BFS works for unweighted/equal-weight edges

Grid neighbor
    → Current position + direction

Multiple starting points
    → Add every source before starting BFS

Graph complexity
    → O(V + E)

Grid complexity
    → O(rows × columns)
```
