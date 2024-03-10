---
layout: post
title:  "Data Structure | Priority Queue(Heap)"
subtitle: Heap 구조를 이해하고 Python 구현 방법 살펴보기
date: 2024-03-09
author: danahkim
categories: Programming
tags: Data-Structure Python

---



> 기초를 C로 배우다가 언어를 Python으로 바꾸게 되면서, 구현 기준이 Python으로 바뀌었다..! 그래도 본질은 같으니까, 배운 것을 정리해보는 포스팅

## Priority Queue

Priority Queue는 우선순위가 높은 데이터가 먼저 나오는 구조이다.

- Stack: 나중에 들어온 데이터가 먼저 나감(FILO)
- Queue: 먼저 들어온 데이터가 먼저 나감(FIFO)
- <mark style='background-color: #fff5b1'>Priority Queue</mark>: 우선순위가 높은 데이터가 먼저 나감



우선순위가 필요한 자료구조의 예시를 들자면, 

- 우선순위를 **시험점수가 높은 순**이라고 했을 때, **점수가 가장 높은 학생을 추출**하는 경우이다.
- 우선순위를 **비용이 낮은 순**이라고 하면, **비용이 가장 낮은 장비의 조합**을 선택하는 경우이다.

이런 구조를 구현하는 방법은 2가지인데, 그냥 배열로 구현해서 max 혹은 min으로 모든 경우의 수를 하나씩 다 찾는다면.. 얼핏 상상만 해보아도 시간복잡도가 엄청 커져서 웬만하면 TLE가 날 것이다.

이 때문에 Heap이라는 방법을 가지고 우선순위 순으로 효율적으로 자료를 저장하여 구현해야한다!

| 구현        | 내용     | 설명     |
| ----------- | -------- | -------- |
| Array(배열) | O(1)     | O(n)     |
| Heap(힙)    | O(log n) | O(log n) |



## Heap

### Heap 구조

Heap 구조는 기본적으로 두가지 특성을 만족해야한다.

1. 완전 이진 트리
2. 부모 노드(Parent)의 우선순위가 자식 노드(Child)의 우선순위보다 높아야한다.



<img src="/assets/images/2024-03-09-heap-priority-queue_images/heap-priority-queue-01.png"/>

<img src="/assets/images/2024-03-09-heap-priority-queue_images/heap-priority-queue-02.png"/>



최대값을 기준으로 우선순위를 주었을 때, 이 두가지 조건을 만족하게 되면 최우선순위 노드에 13이 루트 노드로 존재하게 된다.



### Heap 시간복잡도

그러면 왜 시간복잡도가 O(log n)으로 줄어드는지 push와 pop할 때의 예시로 살펴보자.

먼저 17이라는 값을 heap에 넣는 경우는 가장 맨 마지막 위치에 push를 해주고, parent노드와 비교해서 swap을 한다. 즉 (1) 맨 마지막 위치 push (2) swap (3) swap이 진행된다. 총 3번 수행이 됐는데, 결국 이진트리의 높이만큼 진행된 것과 같아 O(log n)의 시간복잡도를 가진다. 

<img src="/assets/images/2024-03-09-heap-priority-queue_images/heap-priority-queue-03.png"/>

다음으로 heap의 최우선순위에 있는 루트 노드를 pop할 때를 살펴보자. 먼저 루트 노드를 pop를 해주고, 맨 마지막에 있는 값 5를 루트 노드에 가져온 다음 parent노드와 비교해서 swap을 한다. 즉 (1) 최상단노드 pop (2) 맨 마지막 위치 pop (2) 최상단노드 push (4) swap (5) swap 이 진행된다. 총 5번 수행이 됐는데, 결국 이진트리의 높이에 2를 더한 값만큼 진행된 것과 같아 O(log n)의 시간복잡도를 가진다.

<img src="/assets/images/2024-03-09-heap-priority-queue_images/heap-priority-queue-04.png"/>

### Lazy Update

배열에 값을 삭제하면 Heap 구조가 깨져버리기 때문에 불가능하다! 따라서 일단 PQ(Priority Queue를 줄여 말함)에 추가해주고, 나중에 검사해서 데이터를 확인하는 방법이다.



1. Pop을 해서 Top을 뽑는다. Top이 실제의 데이터와 같은지 **유효성을 체크**한다.
   1. 삭제가 진행되는 경우에는 **값의 존재 여부**
   2. 업데이트가 진행되는 경우에는 **최근 값과 같은 값인지**를 체크한다
2. 직전에 동일한 값을 뽑았는지 **중복성을 체크**한다.
   1. 예를들어 Top3개를 추출할 때, 같은 값이 여러번 나올 수 있다.
      1. 앞서서 뽑힌 리스트에 속해있는지 체크하거나
      2. 뒤에 뽑을 데이터가 지금의 데이터와 같지 않도록 while문을 통해 걸러준다
3. 필요시 뽑아낸 Top 리스트를 다시 pq에 push해준다.



이때 만약 pop하지 않아도 되는 경우라면, pq[0]으로 비교하고 유효하지 않은 값을 pop으로 버려주면 된다.



예를 들어, id: score를 가지고 있는 info dictionary가 있고, score가 높은 순으로 우선순위로 가지는 PQ에서 우선순위가 높은 3개를 뽑는 psudo 코드로 구현해보면 아래와 같다. (id 별로 score값은 1개로 가정)

```python
while pq and len(tmp) < 3:
    score, idx = map(abs, heappop(pq))
    # (1) 유효성 체크
    if idx not in info: continue
    if info[idx] != score: continue
    # (2) 중복 체크
  	if idx in tmp: continue
    tmp.append((score, idx))

# 다시 넣어줘야한다면 아래 로직 진행
for idx, score in tmp:
  heappush(pq, (-score, idx))

# 결과 출력
if len(tmp) < 3:
    return -1
else:
    return tmp
```

