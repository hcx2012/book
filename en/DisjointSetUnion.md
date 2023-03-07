# Disjoint Set Union (DSU)

## 1. Principle

### Storage

Generally, an array is used to store the parent node of a node. If this node is the root node, it is stored as the node number.

### Merge Collection

Time complexity: O(1)

Target: Merge set x into set y

Implementation: Set the parent node of the root node of collection x as the root node of collection y

### Find root node

Time complexity: O(n) (n is the depth of the tree)

Target: Find the root node of node node

Implementation: Always find the parent node of the node until the parent node of the node is itself, then the node is the root node of the node node.

### Optimization

The main optimization methods include path compression,~merging by rank (deprecated)~, etc

The most common optimization is path compression, which can effectively reduce time complexity.

Path compression is generally performed during lookup. The parent node of the node is directly pointed to the root node of the node during each lookup.

> [!TIP]
> After the path is compressed, each set of the set [not always *](DisjointSetUnion?id=Note) is queried as a daisy chart (commonly known as a two-layer tree)

## 2. Code implementation

```cpp

const int SIZE = 1000 + 10;// You can change it to your own parameter (and query the maximum value of the set node)
int fa[SIZE];
void init(){
  for (int i = 0; i < SIZE; i++ ){
    fa[i] = i;
  }
}
int get_fa(int node){
  if (fa[node] == node){
    return node; // If the parent node is itself, this node is the root node
  }
  return fa[node] = get_fa(node); // Path compression
  // return get_fa(node); // Uncompressed
}
void merge(int x,int y){
  fa[get_fa(x)]=get_fa(y);
}

```

#### Note

\*: Most of the time is not daisy chart
