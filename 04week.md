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
    <br>
    
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
WriteIndex = 0
for ReadIndex, Value in enumerate(ExampleInputList):
    if Value != 0:
        ExampleInputList[WriteIndex] = Value
        if WriteIndex != ReadIndex:
            ExampleInputList[ReadIndex] = 0
        WriteIndex += 1
print(ExampleInputList)
```
선형시간과 상수공간을 만족시킨다는 점에서 기존보다 개선된 알고리즘이다. <br>
Value가 0일 때 작동되는 코드 없이, 0이지 않을 때만 위와 같은 코드가 작동한다. 그럼에도 불구하고 0이 뒤쪽으로 옮겨지는 것은 어떻게 한 것일까? temp=a; a=b; b=temp 또는 파이썬의 a,b=b,a와 같은 교환(Swap)을 사용한 것일까? 실제로는 그렇지 않다. 이 알고리즘은 값을 교환하지 않고 앞으로 복사한 뒤 기존 위치를 0으로 덮어쓰는 방식으로 동작한다. Value가 0이지 않을 경우에만 리스트 앞쪽으로 값을 가져오고(if Value != 0: ; ExampleInputList[WriteIndex] = Value), 이후 기존 자리에 0을 대입 연산하는 조건으로 (if WriteIndex != ReadIndex:)를 배치시킨 후 그 다음 숫자를 받을 준비를 위해 (WriteIndex += 1)를 둔 것이다. 들여쓰기를 적절히 조절하는 것도 잊지 말자.

<details>
    <summary>AI의 한마디와 추가설명</summary>
    <br>
    
> **투 포인터 알고리즘의 핵심은 데이터를 '교환'하는 것이 아니라 '덮어쓰는 순서'를 설계하는 것이다.** <br>
앞쪽은 항상 완성된 영역으로 유지하고, 뒤쪽은 아직 처리되지 않은 영역으로 남겨 둔다. 이렇게 처리 순서를 설계하면 별도의 임시 변수나 추가 리스트 없이도 원하는 결과를 얻을 수 있다.

- ReadIndex는 현재 읽고 있는 위치를 의미하고, WriteIndex는 다음으로 0이 아닌 값을 저장할 위치를 의미한다.
- 두 포인터는 항상 WriteIndex <= ReadIndex 를 만족하므로, 아직 읽지 않은 데이터를 덮어쓰는 일이 발생하지 않는다.
- if WriteIndex != ReadIndex: 조건은 자기 자신에게 0을 덮어쓰는 불필요한 연산을 방지한다.
이 알고리즘은 원본 리스트를 직접 수정(In-place) 하기 때문에 추가 리스트를 생성하지 않아 공간복잡도는 O(1) 이다.
- 이러한 "읽는 위치(Read Pointer)"와 "쓰는 위치(Write Pointer)"를 분리하는 사고방식은 배열 압축, 중복 제거, 문자열 처리 등 다양한 알고리즘에서 반복적으로 등장한다.

알고리즘과 들여쓰기를 보자. 리스트에서 인덱스와 값을 ReadIndex, Value의 변수명으로 받아 사전에 WriteIndex = 0으로 초기화된 또 다른 변수를 인덱스값으로 사용하여 현재까지 완성된 영역의 다음 위치(WriteIndex)에 0이 아닌 데이터를 기록한다. 그 후 두 인덱스가 차이날 때 ReadIndex의 인덱스값에 있는 리스트의 값에 0을 넣고, 마지막으로 WriteIndex를 다음칸으로 옮겨 다음 for문의 작동을 대기한다. 이러한 for문이 끝난 후 print문을 통해 정렬결과를 출력한다.
</details>    
</details>






