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
