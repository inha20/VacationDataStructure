# 이론  
<br>
순서도, 코딩에서의 문서관리와 파일관리, 메서드와 함수에 대해 알면 좋습니다.  
<br><br>

>알고리즘 얘기

<details><summary>입론</summary>  
➜ 정의 ; 입력을 기반으로 출력을 생성하는 명확하고 효율적이며 유한한 프로세스.<br>
➜ 명확함, 효율성, 유한함, (정확성).<br>
➜ 실행 시간 ; 평가 기준이지만 CPU의 자원, 컴퓨터 성능, 프로그래밍 언어 등에 따라 달라짐.<br>
&nbsp;&nbsp;&nbsp;&nbsp;⤷ 효과적 평가를 위해 단계를 살펴보기로 결정, 수식의 등장이 필요.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;⤷ 같은 문장은 다른 언어라도 대체로 같은 알고리즘임을 묵시적으로 전제함.<br>
</details>
<details>
<summary>T(n)</summary>
➜ 데이터의 크기 n에 따른 필요 단계를 T(n)으로 사용중.<br>
&nbsp;&nbsp;&nbsp;&nbsp; ⤷ 자연수 n은 통상적으로 실수 전체로 편의상 그림.<br>
&nbsp;&nbsp;&nbsp;&nbsp; ⤷ range(1,6)안에 i=6이 있는지 검사하는 과정이 단계에서 빠져있는 등 더 복잡한 이야기들이 남아있음.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ⤷ time의 약자 T(n)은 작은 부분까지 명확히 알기 힘들고, 알 필요도 없음.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ⤷ 수학에서의 "근사"와 같이, 대략적인 경향성 파악이 중요하다.<br>
</details>
<details>
<summary>O(n)</summary>
➜ 가장 큰 하나의 항만 표현<br>
&nbsp;&nbsp;&nbsp;&nbsp; ⤷ 차수는 남기고, 계수는 보통 떼지만 남겨두기도 함.<br>
&nbsp;&nbsp;&nbsp;&nbsp; ⤷ 예를 들어, 다항함수의 경우 최고차항만 표시. 계수를 뗄 수도, 붙일 수도 있음.<br>
➜ O(1)은 상수시간을 가지는 경우이고, O(n)은 선형시간을 가지는 경우이다.<br>
➜ 이진탐색의 경우 O(log n)을 가진다. <br>
&nbsp;&nbsp;&nbsp;&nbsp; ⤷ 예를 들어, n개의 자연수로 Up & Down 놀이를 하는 횟수는 이상적으로 최대 log n의 내림한 자연수.<br>
&nbsp;&nbsp;&nbsp;&nbsp; ⤷ 이쪽 업계에서 log의 밑은 기본적으로 2임. <br>
</details>
<details>
<summary>공간복잡도</summary>
➜ 선형공간복잡도, 상수공간복잡도<br>
➜ 자료구조 특성상 공간 적게 쓰기 훈련을 하지만, 실무에선 안전성과 가독성 위주의 코딩을 하자.<br>
➜ 학습목적 : 효율적 코딩, 코딩 이해 등. 실무에서 필요성을 느끼게 될 수 있음.<br>
</details>
<br>
