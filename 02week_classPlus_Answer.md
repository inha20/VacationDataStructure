
[문제 보기](https://github.com/inha20/VacationDataStructure/blob/main/02week_classPlus.md)

```python
ComputedResults = set()
MatchingKValues = [] 
MaxOfFor=500

/**5중첩 for문*/
def FiveLoop(ForInMax):
    for k in range(2, ForInMax):
        for a in range(2, k + 1):
            for b in range(2, k + 1):
                for c in range(2, k + 1):
                    for d in range(2, k + 1):
                        key = (a, b, c, d)
                        if key in ComputedResults:
                            continue
                        elif ((a ** (5 * d)) * (c ** (5 * b))) == (24 ** (b * d)):
                            ComputedResults.add(key)
                            #print(f"만족: a={a}, b={b}, c={c}, d={d}")       

        if len(ComputedResults) == 59:
            #print(f"k 값: {k}, 만족 개수: {len(ComputedResults)}")
            MatchingKValues.append(k)
        elif len(ComputedResults) > 59:  # 변수명 수정
            #print(f"k 값: {k}, 만족 개수: {len(ComputedResults)}")
            return "STOP"

for i in range(2, MaxOfFor):
    result = FiveLoop(i + 1)
    if result == "STOP":
        break
    
print(MatchingKValues)

if MatchingKValues:
    Answer = MatchingKValues[0] + MatchingKValues[-1]
    print("완료되었습니다. 답은:", Answer)
else:
    print("리스트가 비어 있어 답을 계산할 수 없습니다.")
```

모든 상황을 중복 없이 검토하는지 알고리즘을 순서도로 점검하기, 문제 조건에 맞춰 업그레이드하기. <br>
