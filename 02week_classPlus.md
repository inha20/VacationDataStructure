# 문제 제시
## 문항 정보
<br>
이미지 출처 안내 : [2020학년도0630 고2]. [20190630 고2]. <br> 코딩 시험이 아닌 2019년 06월에 치뤄진 수학과목 가형 30번 문제로, <br>
당시 공식적으로 제공되었던 해설지에서 감안하지 않은 예외적인 특수한 경우가 발견되어 해설지 오답 처리되었다. <br>
평가원이 아닌 교육청 주관이고, 고2였던 만큼, 공식적인 입장 발표는 보이지 않았으나,<br>
정답은 당시 교육청이 발표한 59가 아닌 152 또는 148 정도로 알려져 있다.<br>
<br>
풀이 개시 url 안내 : https://m.blog.naver.com/chjh55897/221556149083<br>
152개라는 입장이며, 확실하다는 문체로 작성되었다.<br>

## 문항 자료 제시
<br>
![문항 캡쳐본](https://github.com/inha20/VacationDataStructure/issues/1#issue-3087734743)


```python
# Define the range for k
k_min = 2
k_max = 500

# Initialize variables to store the maximum and minimum values of k
max_k = None
min_k = None

# Iterate over the range of k
for k in range(k_min, k_max):
    count = 0
    # Iterate over the range of a, b, c, d
    for a in range(2, k + 1):
        for b in range(2, k + 1):
            for c in range(2, k + 1):
                for d in range(2, k + 1):
                    # Check if the condition is satisfied
                    if ((a**5d)*(c**5b)) == (24**(bd)) :
                        count += 1
    # Check if the count is 59
    if count == 59:
        if max_k is None or k > max_k:
            max_k = k
        if min_k is None or k < min_k:
            min_k = k

# Calculate the sum of the maximum and minimum values of k
result = max_k + min_k

print(f"The sum of the maximum and minimum values of k is {result}.")

```


## 질문
이와 같이 이미지의 문제를 풀은 코딩에 대해,<br>
/** Example Hint*/가 코딩 프로그램에서 함수 또는 메서드의 사용 부분에서 코딩의 힌트가 될 수 있도록 구현하여 <br>
순서도, 자료구조, 파일관리, 중복코드 관리, 주석의 부분에서 <br>
좋은 코드를 작성하시오. <br>

## 결론
학과내용 다 배운 후 도전할 능력이 되었으면 좋겠다.
