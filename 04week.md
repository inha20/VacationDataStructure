# 리스트

> 0을 뒤로 옮기기

<details>
    <summary>개론</summary>
    
```python
ExampleInputList = [0, 1, 0, 2, 3, 0, 0]

OutputList1 = []
OutputList1 += [i for i in ExampleInputList if i != 0]
OutputList1 += [i for i in ExampleInputList if i == 0]
print(OutputList1)

OutputList2 = [0] * len(ExampleInputList)
FakeIndex = 0
for i in ExampleInputList:
    if i != 0:
        OutputList2[FakeIndex] = i
        FakeIndex += 1
print(OutputList2)

OutputList3 = [None] * len(ExampleInputList)
FakeIndex = 0
FakeIndexFromBack = -1
for i in ExampleInputList:
    if i != 0:
        OutputList3[FakeIndex] = i
        FakeIndex += 1
    else :
        OutputList3[FakeIndexFromBack] = 0
        FakeIndexFromBack-=1
print(OutputList3)
```
세 경우 모두 시간복잡도와 공간복잡도가 모두 선형 ( 선형시간, 선형공간 ) 이며 T(n) 및 실제 과정은 크게 차이남. <br>
첫 번째는 두 번 순회하고,
세 번째는 음수 인덱스 연산과정이 들어가며, <br>
세 경우 모두 원본이 아닌 복사본을 다루는 방식이라 데이터의 크기가 커질 때 굳이 덮어쓰는 방식으로 원본을 변경하고 싶지 않음. 위험하고 불필요함.

<details>
    <summary>AI의 한마디와 추가설명</summary>
    
> **시간복잡도가 같다고 해서 항상 같은 속도로 동작하는 것은 아니다.** <br>
세 방법 모두 O(n)이지만 순회 횟수, 메모리 접근 방식, 파이썬 내부 구현에 따라 실제 실행 시간은 달라질 수 있다. 알고리즘을 비교할 때는 빅오뿐 아니라 상수 시간(constant factor)도 함께 고려하는 습관을 들이자.

- 첫 번째 방법은 리스트를 두 번 순회하지만 코드가 가장 간결하고 읽기 쉽다.
- 두 번째 방법은 결과 리스트를 미리 생성한 뒤 앞에서부터 값을 채우는 방식으로, 데이터가 어떻게 배치되는지 이해하기 좋다.
- 세 번째 방법은 앞과 뒤를 동시에 채우는 아이디어를 보여 준다. 음수 인덱스를 이용해 뒤에서부터 값을 넣을 수 있다는 파이썬의 특징을 학습하기에 좋은 예제이다.
- 세 방법 모두 원본 리스트를 수정하지 않고 새로운 리스트를 생성한다. 원본 데이터를 보존해야 하는 프로그램에서는 이러한 방식이 더 안전하며, 예상하지 못한 부작용(side effect)을 줄일 수 있다.
- 만약 추가 메모리를 거의 사용하지 않는 것이 중요하다면, 기존 리스트를 직접 수정하는 투 포인터(Two Pointer) 알고리즘도 사용할 수 있다. 이 방법은 공간복잡도를 O(1)까지 줄일 수 있지만 구현이 조금 더 복잡해진다.
</details>
</details>




<details>
    <summary>투 포인터 활용</summary>
    
```python
ExampleInputList = [0, 1, 0, 2, 3, 0, 0]
IndexZero = 0
for Index, Value in enumerate(ExampleInputList):
    if Value != 0:
        ExampleInputList[IndexZero] = Value
        if IndexZero != Index:
            ExampleInputList[Index] = 0
        IndexZero += 1
print(ExampleInputList)
```
선형시간과 상수공간을 만족시킨다는 점에서 기존보다 개선된 알고리즘이다. <br>
Value가 0일 때 작동되는 코드 없이, 0이지 않을 때만 위와 같은 코드가 작동한다. 그럼에도 불구하고 0이 뒤쪽으로 옮겨지는 것은 어떻게 한 것일까? temp=a; a=b; b=temp 또는 이를 파이썬 문법에 맞춘 a,b=b,a를 메서드로 쓰기라도 했단 말인가? 이를 사용하는 매우 비효율적인 코드 대신에, 더 간단한 0이 뒤로 밀려나는 방법을 사용하였다. Value가 0이지 않을 경우에만 리스트 앞쪽으로 값을 가져오고(if Value != 0: ; ExampleInputList[IndexZero] = Value), 이후 기존 자리에 0을 대입 연산하는 조건으로 (if IndexZero != Index: )를 배치시킨 후 그 다음 숫자를 받을 준비를 위해 (IndexZero += 1)를 둔 것이다. 들여쓰기를 적절히 조절하는 것도 잊지 말자.

<details>
    <summary>AI의 한마디와 추가설명</summary>
> [!투 포인터 알고리즘의 핵심은 데이터를 '교환'하는 것이 아니라 '덮어쓰는 순서'를 설계하는 것이다.]
앞쪽은 항상 완성된 영역으로 유지하고, 뒤쪽은 아직 처리되지 않은 영역으로 남겨 둔다. 이렇게 처리 순서를 설계하면 별도의 임시 변수나 추가 리스트 없이도 원하는 결과를 얻을 수 있다.
</details>    
</details>






