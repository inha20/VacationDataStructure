# 길찾기

<details>
    <summary>전체 코드</summary>
   
```python
class Graph:
	def __init__ (self, size):
		self.graph = [[0 for _ in range(size)] for _ in range(size)]


class DisjointSet:  # 크루스칼 알고리즘을 위한 유틸리티 클래스
    def __init__(self, n):
        self.parent = [i for i in range(n)]


    def find(self, z):
        if self.parent[z] != z:
            self.parent[z] = self.find(self.parent[z])  # 경로 압축
        return self.parent[z]


    def merge(self, x, y):  # union
        x_root = self.find(x)
        y_root = self.find(y)
        if x_root != y_root:
            self.parent[y_root] = x_root
            return True
        return False


def print_graph(g) :
	print(' ', end = ' ')
	for v in range(len(g.graph)) :
		print(cities[v], end =' ')
	print()
	for row in range(len(g.graph)) :
		print(cities[row], end =' ')
		for col in range(len(g.graph)) :
			print(f"{g.graph[row][col]:2d}", end=' ')
		print()
	print()


g1 = None
cities = ['인천', '서울', '강릉', '대전', '광주', '부산']
incheon, seoul, gangneung, daejeon, gwangju, busan = 0, 1, 2, 3, 4, 5

graph_size = 6
g1 = Graph(graph_size)
g1.graph[incheon][seoul] = 10; g1.graph[incheon][gangneung] = 15
g1.graph[seoul][incheon] = 10; g1.graph[seoul][gangneung] = 40; g1.graph[seoul][daejeon] = 11; g1.graph[seoul][gwangju] = 55
g1.graph[gangneung][incheon] = 15; g1.graph[gangneung][seoul] = 40; g1.graph[gangneung][daejeon] = 12
g1.graph[daejeon][seoul] = 11; g1.graph[daejeon][gangneung] = 12; g1.graph[daejeon][gwangju] = 20; g1.graph[daejeon][busan] = 30
g1.graph[gwangju][seoul] = 55; g1.graph[gwangju][daejeon] = 20; g1.graph[gwangju][busan] = 28
g1.graph[busan][daejeon] = 30; g1.graph[busan][gwangju] = 28

print('도시 간 도로 건설을 위한 전체 연결도')
print_graph(g1)

edges = list()
for i in range(graph_size) :
	for j in range(graph_size) :
		if g1.graph[i][j] != 0 :
			edges.append([g1.graph[i][j], i, j])
print(edges)

edges.sort()  # 오름차순
print(edges)

ds = DisjointSet(graph_size)
mst_edges = list()
mst_cost = 0

for c, s, e in edges:
    if ds.merge(s, e):
        mst_edges.append([c, s, e])
        mst_cost = mst_cost + c
print(mst_edges)

mst_graph = Graph(graph_size)
for c, s, e in mst_edges:
    mst_graph.graph[s][e] = c
    mst_graph.graph[e][s] = c

print('MST 도로 연결도')
print_graph(mst_graph)
print(f"최소 비용 :  {mst_cost}")

print('\nMST 도로 상황')
for c, s, e in mst_edges:
    print(f"{cities[s]} --- {cities[e]} : {c}")
```
</details>









<details>
    <summary>edges = list()</summary>
	
```python
edges = list()
for i in range(graph_size):
    for j in range(graph_size):
        if g1.graph[i][j] != 0:
            edges.append([g1.graph[i][j], i, j])
edges.sort()
```

edges list에 간선을 등록한 후 비용 순으로 정렬하고 있다.
 </details>








<details>
    <summary>DisjointSet</summary>
	
```python
class DisjointSet:  # 크루스칼 알고리즘을 위한 유틸리티 클래스
    def __init__(self, n):
        self.parent = [i for i in range(n)]


    def find(self, z):
        if self.parent[z] != z:
            self.parent[z] = self.find(self.parent[z])  # 경로 압축
        return self.parent[z]


    def merge(self, x, y):  # union
        x_root = self.find(x)
        y_root = self.find(y)
        if x_root != y_root:
            self.parent[y_root] = x_root
            return True
        return False

for c, s, e in edges:
    if ds.merge(s, e):
        mst_edges.append([c, s, e])
        mst_cost = mst_cost + c
```
초기에는 모든 노드가 자기 자신을 대표(parent)로 가진다. 이후 경로 압축을 통해 두 노드를 하나의 집합으로 묶고 경로를 압축한다. 이 과정은 노드의 부모 노드가 그래프 안에 관계되어있기에 이루어 질 수 있다. 이후 merge를 통해 서로 다른 두 도시를 연결한다. 이제 제일 밑의 for문을 보자. 정렬된 간선 리스트를 반복하며 가장 저렴한 간선부터 순서대로 연결을 시도한다. 연결이 새롭게 될 때 마다 mst에 추가한다. 이렇게 비용을 최소로 하는 최소신장트리가 완성된다.
 </details> 
