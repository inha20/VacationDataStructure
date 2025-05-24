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
index = 0
for i in ExampleInputList:
    if i != 0:
        OutputList2[index] = i
        index += 1
print(OutputList2)

OutputList3 = [None] * len(ExampleInputList)
index = 0
indexFronBack = -1
for i in ExampleInputList:
    if i != 0:
        OutputList3[index] = i
        index += 1
    else :
        OutputList3[indexFronBack] = 0
        indexFronBack-=1
print(OutputList3)
```
</details>



