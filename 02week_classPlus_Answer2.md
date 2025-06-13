```C

#include <stdio.h>
#include <math.h>
#include <stdbool.h>

#define MAX_RESULTS 5000      // 저장 가능한 최대 결과 수
#define EPSILON 0.1           // 실수 비교 허용 오차

/**
 * 구조체: (a, b, c, d) 조합을 저장하기 위한 자료형
 */
typedef struct {
    int a, b, c, d;
} Result;

Result computedResults[MAX_RESULTS];  // 중복 없이 저장할 결과 배열
int resultCount = 0;                  // 현재까지 저장된 결과 수

/**
 * 예시 힌트:
 * 주어진 (a, b, c, d)가 이미 저장된 조합인지 검사합니다.
 * 중복이면 true, 아니면 false를 반환합니다.
 */
bool isDuplicate(int a, int b, int c, int d) {
    for (int i = 0; i < resultCount; i++) {
        if (computedResults[i].a == a &&
            computedResults[i].b == b &&
            computedResults[i].c == c &&
            computedResults[i].d == d) {
            return true;
        }
    }
    return false;
}

/**
 * 예시 힌트:
 * 현재 k 값 범위 내에서 조건을 만족하는 고유 (a, b, c, d) 조합의 수를 구합니다.
 * - 조건: (a^(5d)) * (c^(5b)) == 24^(bd)
 * - 계산 시 오차를 고려해 실수로 비교합니다.
 * - resultCount는 호출될 때마다 초기화됩니다.
 */
int countMatchesForK(int k, int target) {
    resultCount = 0;
    for (int a = 2; a <= k; a++) {
        for (int b = 2; b <= k; b++) {
            for (int c = 2; c <= k; c++) {
                for (int d = 2; d <= k; d++) {
                    if (isDuplicate(a, b, c, d)) continue;

                    double left = pow(a, 5 * d) * pow(c, 5 * b);
                    double right = pow(24, b * d);

                    if (fabs(left - right) < EPSILON) {
                        if (resultCount < MAX_RESULTS) {
                            computedResults[resultCount++] = (Result){a, b, c, d};
                        }
                    }
                }
            }
        }
    }
    return resultCount;
}

/**
 * 예시 힌트:
 * 프로그램 시작 지점입니다.
 * - 사용자로부터 목표 만족 개수를 입력받습니다.
 * - 먼저 10 단위로 k 값을 증가시키며 조건 초과 여부를 탐색합니다.
 * - 조건을 초과하는 k가 발견되면, 그 전후 범위를 세밀하게 다시 탐색합니다.
 * - 조건을 정확히 만족하는 최초의 k를 출력합니다.
 */
int main() {
    int TARGET_MATCH_COUNT;  // 목표 만족 개수 입력 받기
    printf("목표 만족 개수를 입력하세요 (예: 59): ");
    scanf("%d", &TARGET_MATCH_COUNT);

    int preliminaryK = 0;
    int firstValidK = 0;

    // 1단계: 10 단위로 빠르게 탐색
    for (int k = 10; k <= 500; k += 10) {
        int matches = countMatchesForK(k, TARGET_MATCH_COUNT);
        if (matches > TARGET_MATCH_COUNT) {
            preliminaryK = k;
            break;
        }
    }

    if (preliminaryK == 0) {
        printf("조건을 초과하는 k 값을 찾지 못했습니다.\n");
        return 0;
    }

    // 2단계: 초과 시점 근처에서 정밀 탐색
    for (int k = preliminaryK - 10; k <= preliminaryK; k++) {
        int matches = countMatchesForK(k, TARGET_MATCH_COUNT);
        if (matches == TARGET_MATCH_COUNT) {
            if (firstValidK == 0) firstValidK = k;
            printf("k = %d ➝ 만족 개수: %d (조건 정확히 만족)\n", k, matches);
        }
    }

    if (firstValidK > 0) {
        printf("\n🔎 최종 결과: 조건을 정확히 만족하는 k는 %d입니다.\n", firstValidK);
    } else {
        printf("\n⚠️ 조건을 만족하는 k 값을 찾지 못했습니다.\n");
    }

    return 0;
}

```
