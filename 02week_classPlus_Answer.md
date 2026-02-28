
[문제 보기](https://github.com/inha20/VacationDataStructure/blob/main/02week_classPlus.md)

```python
MaxOfFor = 500  # k의 최대 탐색 범위

# 사용자로부터 목표 조합 개수 입력
target_count = int(input("몇 개가 수식을 만족한 시점을 찾으시나요? (예: 59) >> "))

#/**함수설명*/ 
def solve(max_k, target_count):
    """
    max_k까지 k를 증가시키며
    조건을 만족하는 (a,b,c,d) 조합을 찾는다.
    target_count번째 조합이 처음 등장하는 k를 반환한다.
    """

    # 성공한 조합 저장 (중복 방지용)
    ComputedResults = set()

    # 실패한 조합 저장 (중복 재계산 방지용)
    RestResults = set()

    # target_count 이상이 되는 k들을 저장
    MatchingKValues = []

    # target_count번째 조합이 처음 등장한 k
    KOnTargetKey = None

    # k를 2부터 max_k까지 증가시키며 탐색
    for k in range(2, max_k + 1):

        # a,b,c,d는 모두 2 이상 k 이하
        for a in range(2, k + 1):
            for b in range(2, k + 1):
                for c in range(2, k + 1):
                    for d in range(2, k + 1):

                        # 현재 조합을 튜플로 구성 (set에 저장하기 위함)
                        key = (a, b, c, d)

                        # 이미 계산했던 조합이면 건너뜀 (O(1) 평균시간)
                        if key in ComputedResults or key in RestResults:
                            continue

                        # 문제의 핵심 조건 검사
                        # a^(5d) * c^(5b) == 24^(bd)
                        if (a ** (5 * d)) * (c ** (5 * b)) == (24 ** (b * d)):
                            ComputedResults.add(key)

                            # target_count번째 조합이 처음 만들어진 순간 기록
                            if len(ComputedResults) == target_count and KOnTargetKey is None:
                                KOnTargetKey = k
                                print(f"{target_count}번째 조합에 도달! k = {k}")

                        else:
                            # 조건 불만족 조합은 저장해두어 재검사 방지
                            RestResults.add(key)

                        # target_count를 초과하면 즉시 종료 (조기 종료)
                        if len(ComputedResults) > target_count:
                            return KOnTargetKey, k, MatchingKValues

        # 현재 k에서 target_count 이상이면 기록
        if len(ComputedResults) >= target_count:
            MatchingKValues.append(k)

    # 끝까지 탐색했을 경우 반환
    return KOnTargetKey, None, MatchingKValues


# 함수 실행
KOnTargetKey, stop_k, MatchingKValues = solve(MaxOfFor, target_count)

print(f"{target_count}번째 조합이 처음으로 만들어진 k 값: {KOnTargetKey}")

# 문제에서 요구한 계산 (첫 k + 마지막 k)
if MatchingKValues:
    answer = MatchingKValues[0] + MatchingKValues[-1]
    print("답은:", answer)
else:
    print("리스트가 비어 있어 답을 계산할 수 없습니다.")
```
