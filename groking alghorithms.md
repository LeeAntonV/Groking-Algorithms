# **Chapter 1 (Introduction to algorithms)**

## Time Complexity
Time Complexity is a number of *iterations* that we need to solve the problem using given algorithm. 

*Worst Case Scenario* is a case where we get the maximum number of iterations for given algorithm.

*Best Case Scenario* is a case where we get the minimum number of iterations for given algorithm.

Usually when we talk about complexity of algorithm we talk about *Worst Case Scenario*.

• <font size=5>O(log n), also known as log time. Example: Binary search.</font>
• <font size=5>O(n), also known as linear time. Example: Simple search.</font>
• <font size=5>O(n * log n). Example: A fast sorting algorithm, like  quicksort.</font>
• <font size=5>O(n2 ), also known as quadratic time. Example: A slow sorting algorithm, like selection sort.</font>
• <font size=5>O(n!), also known as factorial time. Example: A really slow algorithm, like the traveling
salesperson.</font>

==Time complexity grows with problem size, therefore in some cases more simple algorithm may seem as better approach, however the true power of algorithm reveals when problem size starts growing.== 

## Simple search
Simple search is easiest way to solve array problems, however it is pretty slow
algorithm as it has time complexity of ==**O(n)**==. 

It is an algorithm when we are iterating through each element in the array starting from first(zero-indexed) value.

If we found our target in array then we return index of this value, otherwise we return -1.

Assume we have a problem where we need to find **target** value in array of ints.

```
func simpleSearch(array []int, target int) int {
    target := 2
    for i := 0; i < len(array); i++{
        if array[i] == target{
			return i
        } 
    }
	 return -1
}

```
Here is golang code example of solving this problem using .

## Binary search
Binary search is a way to make things faster than simple search in problems where
you need to find target values in array. ==**It only works for sorted arrays problems.**== and it has time complexity of ==**O(log n).

The approach consists of two ==pointers==:  **left** which equals to 0(the first element of array) and **right** which equals `len(array) - 1`(the last element of array). We iterate through array until
left pointer is *not bigger* than right pointer. 

In loop we create **mid** variable to find a mid value in array. 

We check if `array[mid]` is equal to target, if so we return mid. 

If **mid value** is less than target we cut left half of array and iterate again, as all value that are left to current int will also be less than target value as array is sorted.

If **mid value** is bigger than target we cut right side of array, because all values will be bigger than current value.

Finally if we found no matches, function returns -1 as the answer.

```
func binarySearch(array []int, target int) int {
    left := 0
    right := len(array) - 1

    for (left <= right){
        mid := (left + right)/2
        if array[mid] == target{
            return mid
        } else if array[mid] > target{
            left = mid + 1
        } else {
            right = mid - 1
        }
    }


    return -1
    }
```

Here is golang example for this problem using binary search.

## Overall
In conclusion binary search algorithm is much faster than simple search in terms of sorted array problems. In some literature it may be found that binary search is 15x faster than simple search. However this is untrue as time complexity growth with amount of data wea are working with.


# Chapter 2 (Selection sort)
## How memory works

Memory is dived for many parts that can contain one elements at a time.

Each part has it own id. To store elements in memory, one part of memory should be 
allocated for this item. To store and read elements from memory, array and linked lists 
are used.

## Arrays

Arrays are data structures that are storing elements in memory next to each other, so
that means that if we insert into array, we will need to place it next to others, if this 
can not happen because memory part next to other elements is allocated for another 
element that does not belong to this array, we will need to find another place to put all 
elements next to each other, including new-added element.

Arrays are using random access for elements memory, that means we can take any element,
without traversing through all elements in array.

## Linked Lists

Linked Lists are data structures that are storing elements in memory in different places.
Each element contains it own index and index of previous element;.

Linked Lists are using sequential access for elements, that belong to them. That mean, that 
we need to iterate through all elements before desired one.

## Pros and Cons

Arrays are better to use if you need to use only several elements from the whole array. However, if you need to access each element in your container, than it is more memory efficient to use Linked Lists.

Therefore, Arrays are better for reading elements, however Linked Lists are better 
for insertion. Because for reading we will need to read only one element at a time
and we are not interested about others. 

However for insertions of elements it is better to use Linked Lists, as we will not spend our 
time to find place where all elements can be stored next to each other, but we can put element in any place in our memory and store it's id in previous element.

For deletion, Linked Lists are better because we can delete element from memory and we 
will not need to shift elements next to each other, unlike in arrays.

Thus, the table of time complexity for insertion, reading and deletion operations will be:

![[Pasted image 20240711030404.png]]




## Selection Sort

Selection sort is a sorting algorithm where we take 0-indexed value as minimum value, 
than we iterate through other elements and seek for minimum value inside of this 
scope and if that minimum is less than the minimal-indexed value.  After that we swap 
minimal indexed value and minimal value inside this scope if it is less than current value.

```
func selectSort(arr []int) []int{
    for i:=0; i<len(arr) - 1; i++{

        minIdx := i

        for j:=i+1; j < len(arr); j++{
            if arr[minIdx] > arr[j]{
                minIdx = j
            }
        }
        arr[minIdx], arr[i] = arr[i], arr[minIdx]
    }

    return arr
}

```

Here is golang code representation.

# Chapter 3 (Recursion)

## Stack

Stack is a basic data structure, that is used for scheduling function calls.

It is used in ==recursive functions==. The main principle is that you put each function call 
on top of a stack and executing happens from the most top function call that is stored 
in stack.

![[Pasted image 20240713035531.png]]

Each program has limited amount of memory allocated for stack, therefore when program exceeds this limit, it leads to ==Stack Overflow== error.

## Recursion

Recursion is a algorithm, that recalls itself, until the final condition is satisfied or when memory allocated for stack is exceeded.

Recursion consists of two part:

*Basic case* - final condition where function return the value and it's work ends.

*Recursive case* - condition where function calls itself and this process in repeated until base case is satisfied or program run out of memory.


Recursion usually does not give any performance benefits. Sometimes in even works less 
efficient than basic loops. This approach is used not to improve program's efficiency, but to 
improve performance of programmer as it proposes more readable code solution.


# Chapter 4 (Quick Sort && Merge Sort)

## Quick Sort

Quick sort is one of the fastest algorithms to sort a list. It requires pivot number, that would be a value that all other values would be compared to, through out this iteration.
Whole list is divided into two section: numbers that are less than pivot and numbers that are
bigger than pivot. This process continues until length of list is less than 2, because array
with length one is already sorted. After program reaches to base case, all numbers are taken from stack and putted into right place.

Quick sort is usually being recursive, to make things more easy to read.

![[QuickSort2.png]]

Graphical representation of Quick sort.

```
package main

import "fmt"

func main() {
    arr := []int{5, 6, 2, 4, 3}

    fmt.Println(quickSortStart(arr))
}

func partition(arr []int, left,right int) ([]int, int) {
    pivot := arr[right]
    i := left

    for j:=i; j < right; j++{
        if arr[j] < pivot{
            arr[i], arr[j] = arr[j], arr[i]
            i++
        }
    }

    arr[i], arr[right] = arr[right], arr[i]
    return arr, i
}

func quickSort(arr []int, left, right int) []int{
    if left < right{
        var p int

        arr, p = partition(arr, left, right)
        arr = quickSort(arr, left, p - 1)
        arr = quickSort(arr, p + 1, right)
    }
    return arr
}

func quickSortStart(arr []int) []int {
    return quickSort(arr, 0, len(arr) - 1)
}
```
Example of Quick sort code in golang.

![[quicksort.jpg]]

Best Case and Average case are O(n * log n), however Worst Case is O(n^2), 
because Quick Sort highly relies on how good is pivot number is and worst case 
scenario for this algorithm would be already sorted array.

## Merge sort

Merge sort is divide and conquer sorting algorithm. It works by dividing array into two halves
until length of this array will be 1(so it means that it is sorted). Than results are merged into
one piece and this process continues until all array is merged.

![[Pasted image 20240727164600.png]]
This is graphical representation of merge sort.

```
package main

import (
    "fmt"
)

func main() {
    arr := []int{2, 1, 15, 100, 13}

    fmt.Println(mergeSort(arr))
}

func mergeSort(arr []int) []int{
    if len(arr) < 2{
        return arr
    }

    left := mergeSort(arr[:(len(arr)/2)])
    right := mergeSort(arr[(len(arr)/2):])

    return merge(left, right)
}

func merge(left, right []int) []int{
    res := []int{}
    i := 0
    j := 0

    for i < len(left) && j < len(right){
        if left[i] < right[j]{
            res = append(res, left[i])
            i++
        } else {
            res = append(res, right[j])
            j++
        }
    }

    for ; i < len(left); i++{
        res = append(res, left[i])
    }

    for ; j < len(right); j++{
        res = append(res, right[j])
    }

    return res
}

```

This is golang code representation of merge sort.

Best Case, Average Case and Worst Case are the same: ==O(n * logn)==. That however does not
imply that merge sort is fastest and most useful algorithm, as sometimes time for one
iteration of merge sort can be much bigger than in other approaches.

# Chapter 5 (Hash tables)

## Hash table

Hash table is a very useful data structure that was created for faster data search.
Hash table allows you to assign key value to a actual value in memory and access
it in ==O(1)== time complexity.

**Requirements for Hash Table:**
- Key values should be unique for each memory part, otherwise you want get access to value due to collision of key names
- Hash Table(Hash map) structure should be assigned before its creation. That means
   that  assigning of pair (1, 1) is not allowed for (string, int ) map.

![[Pasted image 20240723162527.png]]

```
package main

import "fmt"

func main() {
    hashmap := make(map[string]int)

    hashmap["Anton"] = 1

    fmt.Println(hashmap)
    fmt.Println(hashmap["Anton"])
}

```
Here is golang code representation of hasmap.

# Chapter 6 (Graphs)

## Graphs
Graphs are physical representation of problem where we have queue of objects.
We use enqueue to add object to end of queue and dequeue to delete first 
element of queue. 

**Graphs are using FIFO method(First In, First Out)**. For example stacks are using 
**LIFO**(Last In, Last Out).

![[Pasted image 20240725181306.png]]

![[Pasted image 20240725181506.png]]

==Graphs can be weighted and unweighted==. 

**Weighted graph** is graph where each node has numerical value of distance(weight)
between nodes.

**Unweighted** graph is graph where each node does not have weight.

## Breadth For Search 

**BFS** answers two questions: Can we get from point A to point B?,
What is a shortest path from A to B?

In **BFS** we traverse with level-by-level manner, which means we are trying to find 
value from upper nodes and ending in down nodes.

```
package main

import (
    "fmt"
)

type Person struct {
    Name     string
    IsSeller bool
}

func main() {
    hashmap := make(map[string][]Person)

    hashmap["Anton"] = []Person{Person{"Alice", false}, Person{"Bob", false}, Person{"Greg", false}}
    hashmap["Alice"] = []Person{Person{"Kate", false}, Person{"Clark", false}}
    hashmap["Bob"] = []Person{Person{"Brad", true}}
    hashmap["Greg"] = []Person{}

    searchQueue := hashmap["Anton"]
    searched := []Person{}

    for len(searchQueue) > 0 {
        person := searchQueue[0]
        searchQueue = searchQueue[1:]

        if !contains(person, searched) {
            if person.IsSeller {
                fmt.Println(person.Name + " is Seller")
                return
            } else {
                add(&searchQueue, hashmap[person.Name])
                searched = append(searched, person)
            }
        }
    }
}

func contains(p Person, arr []Person) bool {
    for _, person := range arr {
        if person == p {
            return true
        }
    }
    return false
}

func add(arr1 *[]Person, arr2 []Person) {
    *arr1 = append(*arr1, arr2...)
}
```

Here is golang code representation.

Time complexity for BFS is ==O(V + E)==. Where V is number of vertices and E is number of 
edges. Required space is also O(V).

## Depth For Search

==DFS== algorithm is a search algorithm for graphs. Unlike in BFS, in DFS we search in to deep 
of the graph, until we hit the last node in current branch and backtrack.

```
package main

import (
    "fmt"
)

type Person struct {
    Name     string
    IsSeller bool
}

func main() {
    hashmap := make(map[string][]Person)

    hashmap["Anton"] = []Person{Person{"Alice", false}, Person{"Bob", false}, Person{"Greg", false}}
    hashmap["Alice"] = []Person{Person{"Kate", false}, Person{"Clark", false}}
    hashmap["Bob"] = []Person{Person{"Brad", true}}
    hashmap["Greg"] = []Person{}

    searchQueue := hashmap["Anton"]
    searched := []Person{}

    for len(searchQueue) > 0 {
        person := searchQueue[len(searchQueue) - 1]
        searchQueue = searchQueue[:len(searchQueue) - 1]
        if !contains(person, searched){
            if person.IsSeller{
                fmt.Println(person.Name + "is seller!")
                return 
            } else {
                add(&searchQueue, hashmap[person.Name])
                searched = append(searched, person)
            }
        }
    }
}

func contains(p Person, arr []Person) bool {
    for _, person := range arr {
        if person == p {
            return true
        }
    }
    return false
}

func add(arr1 *[]Person, arr2 []Person) {
    *arr1 = append(*arr1, arr2...)
}
```

Time complexity for DFS is O(V + E). Where V is number of vertices and E is number of 
edges. Required space is O(V + E).
# Chapter 7 (Dijkstra's && Bellman-Ford algorithm)

## Dijkstra's algorithm
**Dijkstra's algorithm** is an algorithm for weighted graphs.

It search for more efficient path not by shortest amount of edges, but 
by shortest amount of weight of the graph.

This algorithm search for minimal weight for current node and for it's neighbors. We keep track of reversed nodes, to not repeat ourselves. It continues until we hit the final node, than we revert the path and return the shortest(with less weight) pass.

Dijkstra's algorithm only works for non-negative weighted edges in graph.

![[Pasted image 20240730005656.png]]

In this problem we can pick most efficient path as according to algorithm, we can not
process one node more than one time.

Current graph problem:

![[Pasted image 20240730004136.png]]

```
package main

import (
	"fmt"
	"math"
    "strings"
)

type Node struct {
	name      string
	neighbors map[string]int
}

type Graph struct {
	nodes map[string]*Node
}

func NewGraph() *Graph {
	return &Graph{nodes: make(map[string]*Node)}
}

func (g *Graph) AddEdge(from, to string, cost int) {
	if _, ok := g.nodes[from]; !ok {
		g.nodes[from] = &Node{name: from, neighbors: make(map[string]int)}
	}

	g.nodes[from].neighbors[to] = cost
	if _, ok := g.nodes[to]; !ok {
		g.nodes[to] = &Node{name: to, neighbors: make(map[string]int)}
	}
}

func findLowestCostNode(costs map[string]float64, processed map[string]bool) string {
	lowestCost := math.Inf(1)
	var lowestCostNode string
	for node, cost := range costs {
		if cost < lowestCost && !processed[node] {
			lowestCost = cost
			lowestCostNode = node
		}
	}
	return lowestCostNode
}

func GetOptimalPath(parents map[string]string, start, end string) string {
	var path []string
	node := end

	for node != start {
		path = append([]string{node}, path...)
		node = parents[node]
	}
	path = append([]string{start}, path...)

	return strings.Join(path, " -> ")
}

func main() {
	graph := NewGraph()
	graph.AddEdge("start", "a", 6)
	graph.AddEdge("start", "b", 2)
	graph.AddEdge("a", "fin", 1)
	graph.AddEdge("b", "a", 7)
	graph.AddEdge("b", "fin", 6)

	infinity := math.Inf(1)
	costs := map[string]float64{
		"a":   6,
		"b":   2,
		"fin": infinity,
	}

	parents := map[string]string{
		"a":   "start",
		"b":   "start",
		"fin": "",
	}

	processed := make(map[string]bool)

	node := findLowestCostNode(costs, processed)
	for node != "" {
		cost := costs[node]
		neighbors := graph.nodes[node].neighbors
		for n, neighborCost := range neighbors {
			newCost := cost + float64(neighborCost)
			if costs[n] > newCost {
				costs[n] = newCost
				parents[n] = node
			}
		}
		processed[node] = true
		node = findLowestCostNode(costs, processed)
	}

    startNode := "start"
	endNode := "fin"
	optimalPath := GetOptimalPath(parents, startNode, endNode)
	fmt.Println("Optimal Path:", optimalPath)
}

```

This is golang code representation for Dijkstra's problem.


## Bellman-Ford algorithm

==Bellman-Ford== algorithm is one-sourced algorithm for weighted, directed graphs with 
negative weights for edges. Bellman-Ford algorithm is way much slower than **Dijkstra's**
algorithm, but allows us to solve problems with negative weights. 

**Main Principle:**
We first create pair array that will represent table with distances to each node. Starting
node distance would be 0.  To find negative cycle we need to ==relax== edges |V| - 1 times,
where **V** is amount of vertices in graph. 

==Relaxing Edge== in context of this algorithm means putting current edge through following
statement: ==distance[curr. vertice] + weight to next vertice < dist[next vertice]==
If statement is satisfied, than we change next vertice's weight to sum of distance for
current vertice and weight between those two.

**Time Complexity** for this algorithm is O(E) for Best Case and O(E+V) for Worst And Average
Cases.
**Auxiliary Space**: O(V).

```
package main

import (
	"fmt"
	"math"
)

var infinity = math.Inf(1)

type Graph struct {
    v int
	graph [][]int
}

func NewGraph(v int) *Graph {
    return &Graph{v: v, graph: [][]int{}}
}

func (g *Graph) addEdge(u, v, w int) {
    g.graph = append(g.graph, []int{u, v, w})
}

func (g *Graph) BF (src int){
    dist := make([]float64, g.v)

    for i := range dist {
		dist[i] = math.Inf(1)
	}

    dist[src] = 0

    for i := 0; i < g.v - 1; i++{
        u, v, w := g.graph[i][0], g.graph[i][1], g.graph[i][2]
        if dist[u] != infinity && dist[u] + float64(w) < dist[v]{
            dist[v] = dist[u] + float64(w)
        }
    }

    for i := 0; i < g.v; i++{
        u, v, w := g.graph[i][0], g.graph[i][1], g.graph[i][2]

        if dist[u] != infinity && dist[u] + float64(w) < dist[v]{
            fmt.Println("Negative cycle found")
            return
        }
    }

}

func main() {
	g := NewGraph(5)
    g.addEdge(0, 1, -1)
    g.addEdge(0, 2, 4)
    g.addEdge(1, 2, 3)
    g.addEdge(1, 3, 2)
    g.addEdge(1, 4, 2)
    g.addEdge(3, 2, 5)
    g.addEdge(3, 1, 1)
    g.addEdge(4, 3, -3)

    g.BF(0)
}
```

Here is golang code representation of Bellman-Ford algorithm.

# Chapter 8 (Greedy algorithms)

## Philosophy
Philosophy of greedy algorithms is that your do not have to create algorithm that is
100% efficient. It can be slower and do not return best solution possible, but it is
still valid algorithm as this differences are not important for the current problem

```
package main

import "fmt"

func main() {
    s := []string{"mt", "wa", "or", "id", "nv", "ut", "ca", "az"}
    
    statesNeeded := NewSet()
    for _, st := range s {
        statesNeeded.Add(st)
    }

    stations := make(map[string]*Set)
    stations["kone"] = NewSet().Add("id", "nv", "ut")
    stations["ktwo"] = NewSet().Add("wa", "id", "mt")
    stations["kthree"] = NewSet().Add("or", "nv", "ca")
    stations["kfour"] = NewSet().Add("nv", "ut")
    stations["kfive"] = NewSet().Add("ca", "az")

    final := []string{}

    for len(statesNeeded.elements) > 0 {
        bestStation := ""
        statesCovered := NewSet()

        for station, states := range stations {
            covered := NewSet()

            for state := range states.elements {
                if statesNeeded.Contains(state) {
                    covered.Add(state)
                }
            }

            if len(covered.elements) > len(statesCovered.elements) {
                bestStation = station
                statesCovered = covered
            }
        }

        final = append(final, bestStation)

        for state := range statesCovered.elements {
            statesNeeded.Remove(state)
        }
    }

    fmt.Println(final)
}

type Set struct {
    elements map[string]bool
}

func NewSet() *Set {
    return &Set{elements: make(map[string]bool)}
}

func (s *Set) Add(elements ...string) *Set {
    for _, e := range elements {
        s.elements[e] = true
    }
    return s
}

func (s *Set) Remove(elements ...string) {
    for _, e := range elements {
        delete(s.elements, e)
    }
}

func (s *Set) Contains(element string) bool {
    return s.elements[element]
}

```

This is greedy solution for problem where we need to find stations that cover biggest amount of states written in golang.




