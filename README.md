# Clone a Graph
## https://leetcode.com/problems/clone-graph

Given a reference of a node in a connected undirected graph.

Return a deep copy (clone) of the graph.

Each node in the graph contains a val (int) and a list (List[Node]) of its neighbors.
```
class Node {
    public int val;
    public List<Node> neighbors;
}
``` 

**Test case format:**

For simplicity sake, each node's value is the same as the node's index (1-indexed). For example, the first node with val = 1, the second node with val = 2, and so on. The graph is represented in the test case using an adjacency list.

Adjacency list is a collection of unordered lists used to represent a finite graph. Each list describes the set of neighbors of a node in the graph.

The given node will always be the first node with val = 1. You must return the copy of the given node as a reference to the cloned graph.

**Constraints:**

1. 1 <= Node.val <= 100
2. Node.val is unique for each node.
3. Number of Nodes will not exceed 100.
4. There is no repeated edges and no self-loops in the graph.
5. The Graph is connected and all nodes can be visited starting from the given node.

## Implementation : BFS

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> neighbors;
    
    public Node() {
        val = 0;
        neighbors = new ArrayList<Node>();
    }
    
    public Node(int _val) {
        val = _val;
        neighbors = new ArrayList<Node>();
    }
    
    public Node(int _val, ArrayList<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

class Solution {
    public Node cloneGraph(Node node) {
        if(node == null)
            return node;
        Map<Node,Node> map = new HashMap<>();
        Queue<Node> queue = new LinkedList<>();
        queue.add(node);
        while(!queue.isEmpty()){
            Node currentVertex = queue.remove();
            if(!map.containsKey(currentVertex))
                map.put(currentVertex, new Node(currentVertex.val));
            for(Node neighbor : currentVertex.neighbors){
                if(!map.containsKey(neighbor)){
                    map.put(neighbor, new Node(neighbor.val));
                    queue.add(neighbor);
                }
                map.get(currentVertex).neighbors.add(map.get(neighbor));
                
            }
        }
        return map.get(node);
    }
}
```

## Some Improvements :
```java
class Solution {
    public Node cloneGraph(Node start) {
        if (start == null) {
             return null;
        }
        
        Map<Node, Node> vertexMap = new HashMap<>();
        Queue<Node> queue = new LinkedList<>();
        queue.add(start);
        vertexMap.put(start, new Node(start.val));
        
        while(!queue.isEmpty()){
            Node currVertex = queue.remove();
            for (Node neighbor: currVertex.neighbors) {
                if (!vertexMap.containsKey(neighbor)) {
                    vertexMap.put(neighbor, new Node(neighbor.val));
                    queue.add(neighbor);
                }
                vertexMap.get(currVertex).neighbors.add(vertexMap.get(neighbor));
            }    
        }
        
       return vertexMap.get(start); 
    }
}
```

# Key Points :
1. map.containsKey() to check if we already have the node in the map
2. Execute `queue.add(neighbor)` only if its not found in the map, otherwise it will result in infinite execution

# References :
1. https://www.youtube.com/watch?v=vma9tCQUXk8
2. https://github.com/bephrem1/backtobackswe/blob/master/Graphs/CloneAGraph/CloneAGraph.java
