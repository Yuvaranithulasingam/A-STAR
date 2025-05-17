<h1>Exp No 4: Implement A* Search Algorithm for a Graph</h1>

<h3>Name: Yuvarani T</h3>
<h3>Register Number: 212222110057</h3>

<h3>Aim:</h3>
<p>To implement the A* Search algorithm for a graph using Python 3.</p>

<h3>Algorithm:</h3>
<p>
<b>A* Search Algorithm</b><br><br>
1. Initialize the open list.<br>
2. Initialize the closed list. Put the starting node on the open list (you can leave its f at zero).<br>
3. While the open list is not empty:<br>
&nbsp;&nbsp;&nbsp;a) Find the node with the least f on the open list, call it "q".<br>
&nbsp;&nbsp;&nbsp;b) Pop q off the open list.<br>
&nbsp;&nbsp;&nbsp;c) Generate q's successors and set their parents to q.<br>
&nbsp;&nbsp;&nbsp;d) For each successor:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;i) If the successor is the goal, stop the search.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ii) Else, compute both g and h for the successor:<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• g = q.g + distance between successor and q<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• h = heuristic estimated cost from successor to goal<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;• f = g + h<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;iii) If a node with the same position as the successor is in the OPEN list with a lower f, skip this successor.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;iv) If a node with the same position as the successor is in the CLOSED list with a lower f, skip this successor.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;v) Otherwise, add the node to the open list.<br>
&nbsp;&nbsp;&nbsp;e) Push q onto the closed list.<br>
</p>

<hr>
<h2>Program:</h2>
<pre>
from collections import defaultdict
H_dist = {}
def aStarAlgo(start_node, stop_node):
    open_set = set()
    open_set.add(start_node)
    closed_set = set()
    g = {}
    parents = {}
    g[start_node] = 0
    parents[start_node] = start_node
    while open_set:
        n = None
        for v in open_set:
            if n is None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v
        if n is None:
            print("Path does not exist!")
            return None
        if n == stop_node:
            path = []
            while parents[n] != n:
                path.append(n)
                n = parents[n]
            path.append(start_node)
            path.reverse()
            print('Path found:', path)
            return path
        for (m, weight) in get_neighbors(n):
            if m not in open_set and m not in closed_set:
                open_set.add(m)
                parents[m] = n
                g[m] = g[n] + weight
            else:
                if g[m] > g[n] + weight:
                    g[m] = g[n] + weight
                    parents[m] = n
                    if m in closed_set:
                        closed_set.remove(m)
                        open_set.add(m)
        open_set.remove(n)
        closed_set.add(n)
    print("Path does not exist!")
    return None
def get_neighbors(v):
    return Graph_nodes.get(v, [])
def heuristic(n):
    return H_dist.get(n, float('inf'))
graph = defaultdict(list)
n, e = map(int, input().split())
for _ in range(e):
    u, v, cost = map(str, input().split())
    cost = int(cost)
    graph[u].append((v, cost))
    graph[v].append((u, cost))  # Assuming undirected graph
for _ in range(n):
    node, h = map(str, input().split())
    H_dist[node] = int(h)
Graph_nodes = graph
start = input().strip()
goal = input().strip()
aStarAlgo(start, goal)
</pre>

<hr>
<h2>Sample Graph I</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<h2>Sample Input</h2>
<pre>
10 14
A B 6
A F 3
B D 2
B C 3
C D 1
C E 5
D E 8
E I 5
E J 5
F G 1
G I 3
I J 3
F H 7
I H 2
A 10
B 8
C 5
D 7
E 3
F 6
G 5
H 3
I 1
J 0
A
J
</pre>

<h2>Sample Output</h2>
<pre>
Path found: ['A', 'F', 'G', 'I', 'J']
</pre>

<h2>Output Screenshot</h2>

![{058BF2E7-4E3F-46E6-9D03-81BA6770FCCB}](https://github.com/user-attachments/assets/5cef0c10-0d39-4699-9f6f-570006acf360)

<hr>
<h2>Sample Graph II</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)

<h2>Sample Input</h2>
<pre>
6 6
A B 2
B C 1
A E 3
B G 9
E D 6
D G 1
A 11
B 6
C 99
E 7
D 1
G 0
A
G
</pre>

<h2>Sample Output</h2>
<pre>
Path found: ['A', 'E', 'D', 'G']
</pre>

<h2>Output Screenshot</h2>

![{17BE88ED-6E72-4DB5-99C6-AB50DA89B03C}](https://github.com/user-attachments/assets/17de1de1-ba1a-40ea-a59d-a16ab65cd4e4)

<hr>
<h2>Result:</h2>
<p>The A* Search algorithm was implemented successfully using Python 3. The program computes the optimal path based on cost and heuristic estimates.</p>
<hr>
