
[문제 보기](https://github.com/inha20/VacationDataStructure/blob/main/02week_classPlus.md)

```python
ComputedResults = set()
MatchingKValues = []
MaxOfFor = 500

target_count = int(input("몇 개가 수식을 만족한 시점을 찾으시나요? (예: 59) >> "))

def FiveLoop(ForInMax):
    global KOnTargetKey
    for k in range(2, ForInMax):
        for a in range(2, k + 1):
            for b in range(2, k + 1):
                for c in range(2, k + 1):
                    for d in range(2, k + 1):
                        key = (a, b, c, d)
                        if key in ComputedResults:
                            continue
                        if (a ** (5 * d)) * (c ** (5 * b)) == (24 ** (b * d)):
                            ComputedResults.add(key)

                            if len(ComputedResults) == target_count and KOnTargetKey is None:
                                KOnTargetKey = k
                                print(f"[🎯] {target_count}번째 조합에 도달! k = {KOnTargetKey}")

        if len(ComputedResults) == target_count:
            MatchingKValues.append(k)
        elif len(ComputedResults) > target_count:
            return "STOP"

KOnTargetKey = None

for i in range(2, MaxOfFor):
    result = FiveLoop(i + 1)
    if result == "STOP":
        break

print("\n Matching k 값 리스트:", MatchingKValues)
print(f"{target_count}번째 조합이 처음으로 만들어진 k 값: {KOnTargetKey}")

if MatchingKValues:
    Answer = MatchingKValues[0] + MatchingKValues[-1]
    print("답은:", Answer)
else:
    print("리스트가 비어 있어 답을 계산할 수 없습니다.")

```
