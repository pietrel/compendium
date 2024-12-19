# Bread-First Search

*What is the shrotest path to go to X?*

Breadth-first search (BFS) is an algorithm used for traversing tree or graph data structures. It starts at the tree root (or some arbitrary node of a graph, sometimes referred to as a 'search key') and explores the neighbor nodes first, before moving to the next level neighbors.

BFS explores the nodes one level at a time, following a breadthward motion. It uses a queue data structure to keep track of all the nodes that need to be explored. The algorithm is implemented using a queue data structure to store intermediate results.

```rust
use std::collections::VecDeque;

fn bfs(graph: &Vec<Vec<usize>>, start: usize, end: usize) -> Option<Vec<usize>> {
    let mut queue = VecDeque::new();
    let mut visited = vec![false; graph.len()];
    let mut parent = vec![0; graph.len()];

    queue.push_back(start);
    visited[start] = true;

    while !queue.is_empty() {
        let node = queue.pop_front().unwrap();

        if node == end {
            let mut path = vec![];
            let mut at = end;

            while at != start {
                path.push(at);
                at = parent[at];
            }

            path.push(start);
            path.reverse();
            return Some(path);
        }

        for &neighbour in &graph[node] {
            if !visited[neighbour] {
                visited[neighbour] = true;
                parent[neighbour] = node;
                queue.push_back(neighbour);
            }
        }
    }

    None
}

```

