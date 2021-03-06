---
title: "[프로그래머스] 삼각달팽이 & 역삼각달팽이"
categories: programmers
tags: programmers python DFS BFS
published: true
---

## [프로그래머스] 삼각달팽이 & 역삼각달팽이

---

### 문제

<br>

링크 : [프로그래머스](https://programmers.co.kr/learn/courses/30/lessons/68645)

---

<br/><br/>

---

### 풀이

삼각 달팽이와 역삼각 달팽이를 구하는 로직을 짜는 것이다.  
문제는 정수 n이 주어졌을 때, 달팽이의 꼴로 수가 증가하면서  
가운데까지 수를 채웠을 때 피라미드 형태의 배열이 된다.

이 때 윗층부터 차례대로 출력한 결과를 나타내는 것이다.

ex) n = 4, `[1,2,9,3,10,8,4,5,6,7]`

풀이에서 가장 중요하게 생각해야할 점은..  
방향이었다!  
첫번째 나열에서 숫자가 n에 도달한다. -> 방향 변환  
두번째 나열에서 숫자가 n-1에 도달한다. -> 방향 변환  
세번째 나열에서 숫자가 n-2에 도달한다. -> 방향 변환

이렇게 나아간다. 따라서 이 로직을 이용해서 result 배열을 만들어주고  
answer 배열에 처음부터 넣어준다.

역삼각 달팽이도 같은 방식으로 해준다.

```python
# 삼각배열
def solution(n):
    answer = []
    res = [[0] * n for _ in range(n)]
    num = 1
    x, y = -1, 0
    for i in range(n):
        for _ in range(i, n):

            #down
            if i%3 == 0:
                x += 1
            #right
            elif i%3 == 1:
                y += 1
            #up
            elif i%3 == 2:
                x -= 1
                y -= 1

            res[x][y] = num
            num += 1

    for i in res:
        for j in i:
            if j != 0:
                answer.append(j)
    return answer
```

```python
# 역삼각 달팽이
def solution(n):
    answer = []
    res = [[0] * n for _ in range(n)]
    num = 1
    x, y = 0, -1
    for i in range(n):
        for _ in range(i, n):

            #right
            if i%3 == 0:
                y += 1
            #down
            elif i%3 == 1:
                x += 1
                y -= 1
            #up
            elif i%3 == 2:
                x -= 1

            res[x][y] = num
            num += 1

    for i in res:
        for j in i:
            if j != 0:
                answer.append(j)
    return answer

```

---

### 실수했던 점

0으로 이루어진 전체 배열과 방향을 생각하지 못했다.  
삼각형이어야 한다는 고정관념 때문에 접근조차 어려웠다.  
그리고 규칙이 있다는 점을 파악하지 못했기에 풀지 못했다.
