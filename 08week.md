#  이진 탐색 트리 BST
<details>
    <summary>정의와  insert</summary>
    
```python
class TreeNode:
	def __init__(self):
		self.left = None
		self.data = None
		self.right = None


def insert(root, value):
    node = TreeNode()
    node.data = value

    if root is None:
        return node

    current = root
    while True:
        if value < current.data:
            if current.left is None:
                current.left = node
                break
            current = current.left  # 이동
        else:
            if current.right is None:
                current.right = node
                break
            current = current.right  # 이동
    return root
```

하나의 데이터가 양쪽으로 가리키는 구조로, 이중 링크드 리스트와는 달리 비선형구조이다. root와 value를 받아 기존 BST의 밖에서 Treenode를 생성하고 데이터를 받은 후, value가 current.data보다 작으면 왼쪽으로 이동하고 current=current.left로 이동한다. else문부터는 value>=current.data인 경우이다.
</details>




<details>
    <summary>search</summary>
    
```python
def search(find_number):
    current = root
    while True:
        if find_number == current.data:
            return True
        elif find_number < current.data:
            if current.left is None:
                return False
            current = current.left
        else:
            if current.right is None:
                return False
            current = current.right
```

찾는 숫자가 current.data보다 작을 경우, current=current.left로 가기 전에 current.left가 none일 경우 false를 리턴하는 코드를 먼저 실행한다. 이를 right의 경우까지 실행하고 나면 해당 진행 전체를 while True로 묶는다. current가 자리이동할 수 있도록 current=root도 빼먹지 말자.
</details>





<details>
    <summary>delete</summary>
    
```python
def delete(node, value):
    if node is None:
        return None

    if value < node.data:
        node.left = delete(node.left, value)
    elif value > node.data:
        node.right = delete(node.right, value)
    else:  # 같은 경우. 삭제할 노드를 찾음
        if node.left is None:
            return node.right
        elif node.right is None:
            return node.left
        # 자식이 2개인 노드를 삭제
        max_smaller_node = node.left
        while max_smaller_node.right:
            max_smaller_node = max_smaller_node.right  # move
        node.data = max_smaller_node.data
        node.left = delete(node.left, max_smaller_node.data)
    return node
```

else 앞에는 재귀호출이다. 그 이후는 자식이 비어있다면 남은 반대쪽 자식 (또는 False) 을 반환한다. 이는 else문이 node로 들어가 그 노드의 자식 노드로 나오는 것을 통해 알 수 있다. 그렇다면 자식이 둘 다 있는 경우는 어떻게 될까? 왼쪽 서브트리의 가장 큰값을 찾아 node.data에 넣고 이렇게 값이 복사된 기존의 노드를 삭제한다. 그렇다면 이렇게 해도 트리의 정보는 원하는 단 한 가지(또는 0가지)만 삭제되는 것일까?
</details>





<details>
    <summary>delete 의문점에 대한 답</summary>

이진트리에서 자식 노드들이 올 수 있는 숫자의 범위는 부모 노드, 부모 노드의 부모 노드, ... 를 따른다. 이처럼 자식 노드에서 부모 노드로 데이터가 올라가도 범위는 넓어지거나 경우에 따라 같아지기만 할 뿐, 더 줄어들지 않아 노드 데이터 범위의 축소가 일어나지 않는다. 이는 위 delete의 이러한 알고리즘이 알맞은 알고리즘임을 시사한다.
</details>
