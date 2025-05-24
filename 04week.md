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
FakeIndexFronBack = -1
for i in ExampleInputList:
    if i != 0:
        OutputList3[FakeIndex] = i
        index += 1
    else :
        OutputList3[FakeIndexFronBack] = 0
        FakeIndexFronBack-=1
print(OutputList3)
```
세 경우 모두 시간복잡도와 공간복잡도가 모두 선형 ( 선형시간, 선형공간 ) 이며 T(n) 및 실제 과정은 크게 차이남.
</details>




<details>
    <summary>투 포인터 활용</summary>
    
```python
ExampleInputList = [0, 1, 0, 2, 3, 0, 0]
OutputList = [0] * len(ExampleInputList)
FakeIndex = 0
for num in ExampleInputList:
    if num != 0:
        OutputList[FakeIndex] = 0
        FakeIndex += 1
print(OutputList)
```
설명 대규모
</details>



