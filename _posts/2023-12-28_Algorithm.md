---
title: 정글 11주차 / Algorithm
author: cotes
date: 2023-12-28 14:30:00 +0800
categories: [크래프톤 정글]
tags: [Algorithm]
pin: true
math: true
mermaid: true
---

# 2023.12.28 / Algorithm

### 1182 부분수열의 합

- 문제
  N개의 정수로 이루어진 수열이 있을 때, 크기가 양수인 부분수열 중에서 그 수열의 원소를 다 더한 값이 S가 되는 경우의 수를 구하는 프로그램을 작성하시오.

- 입력
  첫째 줄에 정수의 개수를 나타내는 N과 정수 S가 주어진다. (1 ≤ N ≤ 20, |S| ≤ 1,000,000) 둘째 줄에 N개의 정수가 빈 칸을 사이에 두고 주어진다. 주어지는 정수의 절댓값은 100,000을 넘지 않는다.

- 예제를 통한 분석
  예제 입력 예제 출력
  5 0 1
  -7 -3 -2 5 8

---

5개의 인자 / 0이라는 목표  
주어진 숫자 -7, -3, -2, 5, 8 /// 0이라는 목표는 1개 가능 {(-3)+(-2)+(5)}

출력은 count로 해야한다.

- think 1
  밑의 줄을 2중 for문으로 돌면서 각 인자의 합이 '0'이라는 목표에 도달하면 count +1되고, 그것을 출력하는 방식으로 진행?
  -> 2개의 인자만 돌게 되는데, 우리가 위에서 봤듯이 3개의 인자를 받을 때도 있다. 아니, 그냥 여러개의 인자를 받아서 목표를 도달할 수 있도록 진행해야한다.

- think 2

sum을 이용해서 진행하자. sum == S가 목표이니 , if sum(seuqence) == S 라면 count += 1 하는 방식으로 진행하는게 옳지않나?
하지만 sum에 대한 괄호 값은 어떻게 구하지?

- 답지 참고

재귀 함수와 백트래킹을 이용한다.

```python
N,S = map(int,input().split())
num = list(map(int,input().split()))
cnt = 0
ans = []

def solve(start):
    global cnt
    if sum(ans) == S and len(ans) > 0:  #여기에서 sum(ans) == S 까진 생각 가능했겠으나 len(ans) > 0:이 생각 안났을듯
    cnt += 1

    for i in range(start, N):           #재귀 및 백트래킹에서 항상 나오는 부분
    ans.append(num[i])
    solve(i+1)
    ans.pop()

solve(S)
print(cnt)
```

- 재귀 & 백트래킹 부분 짚고 넘어가기
  for i in range (start,N) -> solve의 인자 start(0)부터 N까지 진행
  ans.append(num[i])는 빈 리스트에 input받은 list를 더하는 작업이다.
  solve 함수를 재귀호출하며 +1에 대한 값을 진행한다.
  아닐 경우, pop 진행하면서 백트래킹을 진행한다. (즉, if 구문에 대한것이 실패하면 ans.pop으로 돌아간다.)

if 구문이 성공하면 count+1 , 아니면 backtracking을 통해 맨 앞 부분을 pop하면서 계속 순회하는 구조

- 깨달은 점

1. Input 받을 때 2가지이면 map이고, int,input().split()
2. 백트래킹에 대한 기본 구조를 암기하고 활용해보자 (def , for, pop)
