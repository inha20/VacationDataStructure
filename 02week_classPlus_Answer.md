
[문제 보기](https://github.com/inha20/VacationDataStructure/blob/main/02week_classPlus.md)

```python
MaxOfFor = 500

target_count = int(input("몇 개가 수식을 만족한 시점을 찾으시나요? (예: 59) >> "))


def solve_exact_range(max_k, target_count):
    ComputedResults = set()
    RestResults = set()

    exact_k_values = []   # 정확히 target_count를 만족하는 k들
    reached = False       # target_count에 도달했는지 여부

    for k in range(2, max_k + 1):

        for a in range(2, k + 1):
            for b in range(2, k + 1):
                for c in range(2, k + 1):
                    for d in range(2, k + 1):

                        key = (a, b, c, d)

                        if key in ComputedResults or key in RestResults:
                            continue

                        if (a ** (5 * d)) * (c ** (5 * b)) == (24 ** (b * d)):
                            ComputedResults.add(key)
                        else:
                            RestResults.add(key)

        current_count = len(ComputedResults)

        # 정확히 target_count일 때만 기록
        if current_count == target_count:
            exact_k_values.append(k)
            reached = True

        # 한 번이라도 도달했고, 초과하면 종료
        elif current_count > target_count:
            break

    return exact_k_values


# 실행
exact_range = solve_exact_range(MaxOfFor, target_count)

if exact_range:
    print("정확히 유지되는 k 구간:")
    print(f"시작 k = {exact_range[0]}")
    print(f"끝 k = {exact_range[-1]}")
    print("답:", exact_range[0] + exact_range[-1])
else:
    print("정확히 target_count가 유지되는 구간이 없습니다.")
```
