# 링크드 리스트


<details>
    <summary>결과물 미리보기</summary>
    
```python
class Node:
    def __init__(self, data, link=None):
        self.data = data
        self.link = link

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        if not self.head:
            self.head = Node(data)
            return
        current = self.head
        while current.link:
            current = current.link  # move current
        current.link = Node(data)

    def remove(self, target):
        current = self.head
        if self.head.data == target:
            self.head = self.head.link
            current.link = None
            return

        previous = None
        while current:
            if target == current.data:
                previous.link = current.link
                current.link = None
            previous = current
            current = current.link

    def search(self, target):
        current = self.head
        while current:  # bug fix
            if target == current.data:
                return f"{target}을(를) 찾았습니다!"
            else:
                current = current.link
        return  f"{target}은(는) 링크드 리스트 안에 존재하지 않습니다."

    def __str__(self):
        current = self.head
        result = ""
        while current is not None:
            result = result + f"{current.data} -> "
            current = current.link
        return result + "END"

    def reverse(self):
        PrevNode = None
        CurNode = self.head
        while CurNode:
            NextLink = CurNode.link 
            CurNode.link = PrevNode  
            PrevNode = CurNode  
            CurNode = NextLink 
        self.head = PrevNode

    def has_cycle(self):
        slow = self.head
        fast = self.head
        while fast.link and fast:
            slow = slow.link  
            fast = fast.link.link  
            if slow == fast:
                return True  
        return False 
```
부분부분 나눠서 이해해보자.
</details>






<details>
    <summary>클래스 노드, 클래스 링크드리스트</summary>
    
```python
class Node:
    def __init__(self, data, link=None):
        self.data = data
        self.link = link

class LinkedList:
    def __init__(self):
        self.head = None
```
노드는 데이터(data)와 다음 노드를 가리키는 링크(link)로 구성된다. data는 필수 입력값이며, link는 기본값으로 None을 가진다. 따라서 노드를 생성할 때 다음 노드를 지정하지 않으면 마지막 노드로 생성된다.

링크드 리스트는 생성될 때 self.head = None으로 초기화된다. 이는 첫 번째 노드를 아직 가리키고 있지 않은 빈(Empty) 링크드 리스트임을 의미한다. 이후 첫 번째 노드가 삽입되면 self.head는 그 노드를 가리키게 된다.

<details>
    <summary>AI의 한마디와 추가설명</summary>  <br>  

> **링크드 리스트의 시작점은 첫 번째 노드가 아니라 head이다.** <br>
head는 데이터를 저장하는 노드가 아니라 첫 번째 노드를 가리키는 참조 변수이다. 따라서 head가 None이라는 것은 데이터가 없는 것이 아니라, 리스트 자체가 비어 있음을 의미한다.

- Node 클래스는 하나의 노드를 표현하는 클래스이다.
- LinkedList 클래스는 여러 노드를 관리하는 클래스이다.
- 하나의 노드는 자신의 데이터와 다음 노드만 알고 있으며, 리스트 전체의 시작 위치는 head가 관리한다.
- link=None을 기본값으로 둔 이유는 새로운 노드를 만들 때 다음 노드가 없는 상태를 기본으로 하기 위해서이다.

여기서 가장 중요한 개념은 "Node와 LinkedList는 역할이 다르다"는 점이다.
- Node는 데이터를 담는 객체
- LinkedList는 노드들을 관리하는 객체
</details>
</details>





<details>
    <summary>링크드리스트 프린트문</summary>
    
```python
    def __str__(self):
        current = self.head
        result = ""
        while current is not None:
            result = result + f"{current.data} -> "
            current = current.link
        return result + "END"
```
자신의 헤드 노드를 current가 가리키도록 한다. 결과를 저장할 문자열 result는 빈 문자열("")로 초기화한다. current가 None이 될 때까지 반복하며, 현재 노드의 데이터를 문자열에 "데이터 -> " 형식으로 이어 붙인다. 이후 current = current.link를 수행하여 현재 노드가 가리키는 다음 노드로 이동한다. 이 과정을 반복하면 링크드 리스트의 모든 노드를 처음부터 끝까지 순회하게 된다. 반복문이 종료되면 마지막에 "END"를 덧붙여 리스트의 끝임을 나타낸 문자열을 반환한다.

<details>
    <summary>AI의 한마디</summary>
    <br>

> **링크드 리스트는 배열처럼 인덱스로 이동하지 않는다.** <br>
각 노드가 다음 노드의 주소(참조)를 가지고 있기 때문에, current = current.link를 반복하며 한 노드씩 순차적으로 이동한다. 이것이 링크드 리스트 순회의 기본 원리이다.

- self.head는 첫 번째 노드를 가리키는 시작점이다.
- current는 순회 과정에서만 사용하는 임시 참조 변수이므로, current를 이동시켜도 self.head는 변하지 않는다.
- current가 None이 되었다는 것은 더 이상 연결된 다음 노드가 없다는 뜻이며, 리스트의 끝에 도달했음을 의미한다.
- 마지막에 "END"를 붙이는 것은 사용자가 출력 결과만 보고도 리스트가 어디서 끝나는지 쉽게 확인할 수 있도록 하기 위한 표현이다.

> **성능 관점에서 볼만한 점** <br>
result = result + f"{current.data} -> "
는 문자열을 계속 새로 생성하기 때문에 노드가 많아질수록 비효율적일 수 있다. 교육용으로는 이해하기 쉽지만, 실제 파이썬에서는 문자열을 리스트에 모은 뒤 "".join(...)을 사용하는 방식이 더 효율적이다. 
</details>
</details>








<details>
    <summary>search() 메서드</summary>
    
```python
    def search(self, target):
        current = self.head
        while current: 
            if target == current.data:
                return f"{target}을(를) 찾았습니다!"
            else:
                current = current.link
        return  f"{target}은(는) 링크드 리스트 안에 존재하지 않습니다."
```
head부터 시작한 current가 존재하는 동안(current가 None이 아닐 동안), 현재 노드의 데이터(current.data)와 찾고자 하는 값(target)을 비교한다. 값이 일치하면 즉시 찾았다는 메시지를 반환하며 메서드를 종료한다. 일치하지 않으면 current = current.link를 수행하여 다음 노드로 이동한 뒤 같은 과정을 반복한다. 모든 노드를 순회할 때까지 원하는 값을 찾지 못하면 반복문이 종료되고, 링크드 리스트에 해당 값이 존재하지 않는다는 안내 메시지를 반환한다.
<details>
    <summary>AI의 한마디와 추가설명</summary>  <br>  
    
> **링크드 리스트는 원하는 데이터를 찾기 위해 처음부터 차례대로 확인해야 한다.** <br>
> 배열처럼 인덱스로 바로 접근할 수 없기 때문에, 특정 데이터를 찾는 과정은 최악의 경우 마지막 노드까지 모두 확인해야 한다.

- current는 항상 현재 검사 중인 노드를 가리키는 참조 변수이다.
- 원하는 데이터를 찾는 즉시 return이 실행되므로, 이후의 노드는 더 이상 검사하지 않는다.
- while current:는 while current is not None:과 같은 의미로 사용할 수 있는 파이썬의 축약 표현이다.
- 이 메서드의 시간복잡도는 O(n) 이다. 찾는 데이터가 마지막에 있거나 존재하지 않는 경우 모든 노드를 순회해야 하기 때문이다.
- 배열은 인덱스를 이용한 직접 접근(Random Access)이 가능하지만, 링크드 리스트는 노드를 하나씩 따라가야 하는 순차 접근(Sequential Access)만 가능하다.
</details>
</details>








<details>
    <summary>append() 메서드</summary>
    
```python
    def append(self, data):
        if not self.head:
            self.head = Node(data)
            return
        current = self.head
        while current.link:
            current = current.link  
        current.link = Node(data)
```
self.head가 없으면 붙이고, 있을 경우 다음에 따른다 : current.link가 있을 동안 current=current.link로 한 칸 씩 넘어가며 current를 제일 마지막으로 몰은 후, 그러한 current의 link에 data를 입력받아 생성된 Node를 연결한다.
</details>










<details>
    <summary>remove() 메서드</summary>
    
```python
    def remove(self, target):
        current = self.head
        if self.head.data == target:
            self.head = self.head.link
            current.link = None
            return

        previous = None
        while current:
            if target == current.data:
                previous.link = current.link
                current.link = None
            previous = current
            current = current.link
```
head에 target이 있을 경우, 먼저 head를 기존 head의 link로 옮겨준 후 여전히 그 앞을 가리키고 있는 current가 가리키는 연결을 끊는다. current 변수는 garvage collecter에 의해 자동으로 사라진다. 다음 변수 하나를 while문 밖에 선언 후, current가 있을 동안 다음을 수행한다 : previous를 current와 같은 대상을 가리키게 한 후 current가 한 칸 앞으로 가는 (링크를 타는) 행위를 target != current.data일 동안 반복하며, 만약 그렇지 않다면 current의 연결을 모두 끊어 삭제하기 위해 current의 link를 previous의 것으로 넘겨줘 기존의 previous.lonk에게 가리킴 받고 있던 것을 본인의 link로 대체하여 가리킴 받는 것을 끊은 후 본인이 가르키는 것을 None으로 하여 링크드리스트에 이상 없이 잘 제외되어있는 상황에서 가비지 컬렉터에 의해 target이 삭제됨. 
</details>






<details>
    <summary>링크드 리스트 뒤집기</summary>
    
```python
def reverse(self):
    PrevNode = None
    CurNode = self.head
    while CurNode:
        NextLink = CurNode.link 
        CurNode.link = PrevNode  
        PrevNode = CurNode  
        CurNode = NextLink 
    self.head = PrevNode
```
개인적으로 어려웠던 구간이다. link의 대입이란 목적지까지의 끝으로 향하는 화살표의 종점을 유지하며 화살표의 시점을 대입하는 방향으로 덮어쓰는 과정이다. 따라서 NextLink=CurNode.link는 기존의 현재 노드가 가리키는 종점 정보를 유지한 상태에서 새로운 변수에 시점을 임시저장하는 형태로, 추후 지금의 CurNode에 대해 CurNode.link.link = NextLink 가 CurNode의 이동 등과 연관지어져서 이루어짐을 암시한다. 이처럼 CurNode.link를 임시저장한 상태에서, 그 위를 PrevNode로 덮어쓰게 되면 이는 CurNode의 link 방향이 정반대로 바뀐 것이다. 그렇다면 기존의 CurNode.link가 가리키는 오브젝트(종점)의 정보에는 어떻게 접근 할 수 있을까? 그렇다. NextLink=CurNode.link로 백업을 이미 해놓았지 않은가. 이러한 과정을 그 다음, 그 다다음의 노드에서도 계속하기 위해선 기존의 CurNode.link에 해당하는 NextLink를 CurNode에 덮어쓰면 된다, 그리고 당연히 그 사이엔 PrevNode를 CurNode로 끌어오는 과정이 순서에 맞게 들어가야 한다. 다시 말해, NextLink=CurNode.link; 와 CurNode=NextLink; 사이에는 현재 노드가 화살표의 방향을 반대로 돌리는 CurNode.link=PrevNode; 와 그러한 PrevNode를 PrevNode=CurNode;로 끌어오는 과정이 필연적으로 필요하며, 예를 들어가며 작동시켜보면 잘 작동된다는 것을 알 수 있게 된다. 이러한 과정이 끝난 후에 새로운 head를 알맞게 지정하면 끝이다.
</details>





<details>
    <summary>링크드 리스트 사이클 찾기</summary>
    
```python
def has_cycle(self):
    slow = self.head
    fast = self.head
    while fast.link and fast:
        slow = slow.link  
        fast = fast.link.link  
        if slow == fast:
            return True  
    return False 
```
이 메서드의 정확도를 고등학교까지의 수학적으로 따져볼 필요성이 있어보인다. slow와 fast의 이동 칸 수 차이가 1임으로 사이클의 끝에 None 대신 사이클의 원소가 들어있지 않은지를 판별할 수 있다는 명제의 참거짓을 밝히기 위해, 사이클의 끝에 사이클의 원소 잘못 대입을 가정한 후 slow와 fast의 칸 수 차이가 2 이상이지 못함을 보이자. 이 때 칸수가 2일때만 보이면 충분하며, 예시로 1-2-3-4-2 와 1-2-3-4-5-2 의 두 가지 예시가 모두 만족함으로 전제하는 근본 논리가 참임을 보일 수 있다. 
</details>


