# 스택, 큐

<details>
    <summary>스택의 푸쉬와 팝</summary>
    
```python
class Stack:
    def __init__(self):
        self.ArrayForStack = []
        self.top = 0

    def push(self, data):
        self.ArrayForStack.append(data)
        self.top += 1

    def pop(self):
        if self.top == 0:
            return "Stack is empty!"
        self.top -= 1
        return self.ArrayForStack.pop()
```
</details>

<details>
    <summary>괄호 짝 맞추기</summary>
    
```python
def is_valid_parentheses(expression : str) -> bool:  # type hint
    stack = list()
    for letter in expression:
        if letter == "(":
            stack.append(letter)
        if letter == ")":
            if len(stack) == 0:
                return False
            else:
                stack.pop()
    return len(stack) == 0 
```

</details>

<details>
    <summary>배열과 두개의 포인터로 큐 만들기</summary>
    
```python
class Queue:
    def __init__(self):
        self.queue = [] 
        self.front = 0
        self.back = 0

    def push(self, data):
        self.queue.append(data)
        self.back += 1

    def pop(self):
        if self.front == self.back:
            return "Queue is empty!"
        data = self.queue[self.front]
        self.front += 1
        return data
```

</details>

