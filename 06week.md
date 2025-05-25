# 스택, 큐

<details>
    <summary>스택의 푸쉬와 팝</summary>
    
```python
class Node:
    def __init__(self, data, link=None):
        self.data = data
        self.link = link

class Stack:
    def __init__(self):
        self.top = None

    def push(self, data):
        node = Node(data)
        if self.top is None:
            self.top = node
        else:
            node.link = self.top
            self.top = node

    def pop(self):
        if self.top is None:
            return "Stack is empty!"
        popped_node = self.top
        self.top = self.top.link
        popped_node.link = None
        return popped_node.data
```
</details>

<details>
    <summary>괄호 짝 맞추기</summary>
    
```python
# print(1+2))
def is_valid_parentheses(expression : str) -> bool:  # type hint
    stack = list()
    for letter in expression:
        if letter == "(":
            stack.append(letter)
        if letter == ")":
            if len(stack) == 0:
                return False  # )1+2(), (1+2))
            else:
                stack.pop()
    return len(stack) == 0  # (1+2), ((3*2)/2), ((3*2/2)

print(is_valid_parentheses(")1+2()"))
print(is_valid_parentheses("(1+2))"))
print(is_valid_parentheses("(1+2)"))
print(is_valid_parentheses("((3*2)/2)"))
print(is_valid_parentheses("((3*2/2)"))
```
------
</details>

<details>
    <summary>배열과 두개의 포인터로 큐 만들기</summary>
    
```python
--------
```
------
</details>

<details>
    <summary>두 개의 스택으로 큐 만들기</summary>
    
```python
--------
```
------
</details>
