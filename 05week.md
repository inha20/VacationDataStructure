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
노드는 링크와 데이터로 구성된다. 데이터는 필수 입력값, link는 기본값 None이다. 링크드리스트는 자신 헤드의 데이터를 None으로 입력하는 것으로 자기 자신을 정의하고 생성한다.
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
자신의 헤드를 current가 가리킨다. 결과 문자열은 파이썬 문법에 따라 덧셈 부호로 문자열을 붙인다. current가 None일때까지, result에 현재 데이터를 서식에 따라 추가한 후 current에 currnnt.link가 대입되며 계속해서 노드를 가리킨다. 이러한 반복문이 끝난 후 "END"가 붙여지는 부가기능도 있다.
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
head부터 시작된 current가 있을 동안, 다시 말해 current가 가리키는 노드가 정의되어 있을 동안, current(노드)의 자식 관계인 current.data와 찾을 값(targer)을 비교한다. 틀릴 경우 current는 link에 연결된 가 다음 노드로 넘어가 같은 작업을 반복한다. 반복문 전체를 다 돌을 동안 찾지 못한 채 반복문이 끝난다면, 찾지 못했다는 안내 메세지를 띄어준다.
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






<details>
    <summary>이중 링크드 리스트로 변경하기</summary>
    
```python
-------
```
이중 링크드 리스트의 기능 구현은 다음 주차에서 계속.
</details>
