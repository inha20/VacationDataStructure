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

