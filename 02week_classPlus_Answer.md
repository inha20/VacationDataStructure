
[문제 보기](https://github.com/inha20/VacationDataStructure/blob/main/02week_classPlus.md)

```python
MAX_K = 500


def is_valid_combination(a, b, c, d):
    """주어진 (a, b, c, d)가 조건을 만족하는지 확인"""
    return (a ** (5 * d)) * (c ** (5 * b)) == (24 ** (b * d))


def solve_exact_range(max_k, target_count):
    valid_combinations = set()
    exact_k_values = []

    for k in range(2, max_k + 1):
        for a in range(2, k + 1):
            for b in range(2, k + 1):
                for c in range(2, k + 1):
                    for d in range(2, k + 1):

                        key = (a, b, c, d)

                        # 이미 확인한 조합은 스킵
                        if key in valid_combinations:
                            continue

                        if is_valid_combination(a, b, c, d):
                            valid_combinations.add(key)

        current_count = len(valid_combinations)

        if current_count == target_count:
            exact_k_values.append(k)

        elif current_count > target_count:
            break

    return exact_k_values


def main():
    target_count = int(input("몇 개가 수식을 만족한 시점을 찾으시나요? >> "))

    result = solve_exact_range(MAX_K, target_count)

    if result:
        print("정확히 유지되는 k 구간:")
        print(f"시작 k = {result[0]}")
        print(f"끝 k = {result[-1]}")
        print("답:", result[0] + result[-1])
    else:
        print("해당 조건을 만족하는 구간이 없습니다.")


if __name__ == "__main__":
    main()
```
