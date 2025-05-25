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
        index += 1
    else :
        OutputList3[FakeIndexFromBack] = 0
        FakeIndexFronBack-=1
print(OutputList3)
```
세 경우 모두 시간복잡도와 공간복잡도가 모두 선형 ( 선형시간, 선형공간 ) 이며 T(n) 및 실제 과정은 크게 차이남. <br>
첫 번째는 두 번 순회하고,
세 번째는 음수 인덱스 연산과정이 들어가며, <br>
세 경우 모두 원본이 아닌 복사본을 다루는 방식이라 데이터의 크기가 커질 때 굳이 덮어쓰는 방식으로 원본을 변경하고 싶지 않음. 위험하고 불필요함.
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
if IndexZero != Index: 란 "0이 있기로 했던(IndexZero+=1이 아래쪽에 있음) 인덱스와 리스트의 인덱스가 다르다면"이라는 뜻으로, 이 과정을 통해  
</details>



