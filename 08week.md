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

하나의 데이터가 최대 두 개의 자식 노드를 가리키는 비선형 자료구조이다. 연결 리스트처럼 순차적으로 이어지는 선형 구조가 아니라 계층적인 형태를 가진다. insert(root, value) 함수는 root와 value를 입력받아 새로운 TreeNode를 생성한 뒤, 기존 이진 탐색 트리(BST)의 적절한 위치에 삽입한다. 먼저 root가 None이면 트리가 비어 있는 상태이므로 새 노드를 루트로 반환한다. 트리가 존재하면 current를 root로 설정한 뒤 반복문을 수행한다.
- value < current.data이면 BST의 규칙에 따라 왼쪽 서브트리로 이동한다.
	- 왼쪽 자식이 없으면 그 위치에 새 노드를 연결한다.
	- 자식이 있으면 current = current.left로 이동하여 탐색을 계속한다.
- 그렇지 않은 경우(value >= current.data)에는 오른쪽 서브트리로 이동한다.
	- 오른쪽 자식이 없으면 새 노드를 연결한다.
	- 자식이 있으면 current = current.right로 이동하여 탐색을 계속한다.
   
삽입이 완료되면 기존 트리의 루트(root)를 반환한다. 이 알고리즘은 BST의 왼쪽에는 더 작은 값, 오른쪽에는 같거나 큰 값이라는 성질을 유지하면서 새로운 노드를 삽입한다.
<details>
    <summary>AI의 한마디와 추가설명</summary>  <br>  
이 코드에서는 중복값을 허용하며, 중복값은 모두 오른쪽 서브트리에 삽입됩니다(else 때문). 삽입 과정은 루트에서 시작하여 리프 노드까지 한 경로만 따라가므로 **시간 복잡도는 트리의 높이 h에 비례하여 O(h)** 입니다. <br><br>
균형 잡힌 BST: O(log n) <br><br>
한쪽으로 치우친 BST: O(n)
</details>	
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

하나의 값을 입력받아 BST에서 해당 값이 존재하는지 탐색하는 함수이다. 먼저 current = root로 루트 노드부터 탐색을 시작한다. 이후 while True를 통해 값을 찾거나 더 이상 이동할 수 없을 때까지 반복한다.
- find_number == current.data이면 원하는 값을 찾은 것이므로 True를 반환한다.
- find_number < current.data이면 BST의 규칙에 따라 왼쪽 서브트리로 이동한다.
	- 이동하기 전에 current.left가 None이면 더 이상 탐색할 노드가 없으므로 False를 반환한다.
	- 그렇지 않으면 current = current.left로 이동하여 탐색을 계속한다.
- find_number > current.data이면 오른쪽 서브트리로 이동한다.
	- current.right가 None이면 값을 찾을 수 없으므로 False를 반환한다.
	- 그렇지 않으면 current = current.right로 이동하여 탐색을 계속한다.

BST는 왼쪽에는 더 작은 값, 오른쪽에는 더 큰(또는 같은) 값이 저장되는 성질을 이용하여 불필요한 탐색을 줄인다.

<details>
    <summary>AI의 한마디와 추가설명</summary>  <br>  
	
- current = root가 없으면 탐색을 시작할 위치를 알 수 없으므로 함수가 동작하지 않습니다.
- 이 코드는 값을 찾는 즉시 True, 더 이상 이동할 수 없는 순간 False를 반환하므로 끝까지 모든 노드를 탐색하지 않습니다. 이것이 BST 탐색이 효율적인 이유입니다.
- **시간 복잡도는 트리의 높이 h에 비례하여 O(h)** 입니다.
	- 균형 잡힌 BST: O(log n)
	- 한쪽으로 치우친 BST: O(n)
- 이 코드에서는 root가 None인 빈 트리를 처리하지 않습니다. 실제 프로그램에서는 함수의 처음에 if root is None: return False를 추가하면 빈 트리에서도 안전하게 동작합니다.
</details>	
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

<details>
    <summary>delete 의문점에 대한 답</summary>

이진트리에서 자식 노드들이 올 수 있는 숫자의 범위는 부모 노드, 부모 노드의 부모 노드, ... 를 따른다. 이처럼 자식 노드에서 부모 노드로 데이터가 올라가도 범위는 넓어지거나 경우에 따라 같아지기만 할 뿐, 더 줄어들지 않아 노드 데이터 범위의 축소가 일어나지 않는다. 이는 위 delete의 이러한 알고리즘이 알맞은 알고리즘임을 시사한다.


<details>
    <summary>AI의 한마디와 추가설명</summary>  <br>  
삭제할 값을 입력받아 BST에서 해당 노드를 제거하는 함수이다.

먼저 node가 None이면 삭제할 값이 존재하지 않으므로 None을 반환한다.

삭제할 값을 찾기 전까지는 BST의 성질을 이용하여 재귀적으로 탐색한다.

- value < node.data이면 왼쪽 서브트리에서 삭제를 수행하고, 결과를 node.left에 연결한다.
- value > node.data이면 오른쪽 서브트리에서 삭제를 수행하고, 결과를 node.right에 연결한다.
- value == node.data이면 삭제할 노드를 찾은 것이다.

삭제할 노드를 찾으면 세 가지 경우로 나뉜다.

1. 왼쪽 자식이 없는 경우
	- 오른쪽 자식을 반환하여 현재 노드를 대체한다.
2. 오른쪽 자식이 없는 경우
	- 왼쪽 자식을 반환하여 현재 노드를 대체한다.
3. 자식이 두 개인 경우
	- 왼쪽 서브트리에서 가장 큰 값(중위 순회의 바로 이전 값)을 찾는다.
	- 그 값을 현재 노드의 데이터에 복사한다.
	- 복사한 값이 원래 있던 노드를 왼쪽 서브트리에서 다시 삭제한다.

마지막에 현재 노드(node)를 반환하여 부모 노드와의 연결을 유지한다.

------------
delete 의문점에 대한 답

> "값을 복사하고 원래 노드를 삭제하면 정말 하나의 데이터만 삭제되는 것일까?"

그렇다.

처음에는 동일한 값이 두 개 존재하는 것처럼 보이지만, 복사는 임시 상태일 뿐이다. 왼쪽 서브트리의 최댓값은 현재 노드보다 작은 값들 중 가장 큰 값이다. 따라서 현재 노드의 값을 이 값으로 바꾸어도 왼쪽 서브트리의 모든 값은 여전히 작거나 같고, 오른쪽 서브트리의 모든 값은 여전히 크거나 같으므로 BST의 정렬 규칙이 유지된다. 즉, 노드의 허용 범위가 넓어져서가 아니라, 선택한 노드 자체가 BST의 정렬 조건을 만족하는 '경계값(boundary value)'이기 때문에 구조가 깨지지 않는 것이다.


</details>	
</details>
</details>
