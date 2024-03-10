---
layout: post
title:  "Data Structure | Stack, Queue"
subtitle: 스택과 큐의 자료구조를 이해하고 C로 함수 구현하기
date:   2022-07-18
author: danahkim
tags: Data-Structure
categories: Programming
---

>  Stack과 Queue라는 자료구조에 대해 알아보고 C로 함수를 직접 구현해본다.



## Stack

스택은 바닥에 일렬로 쌓는 상자를 생각하면 이해가 쉽다. 스택은 LIFO(last in first out) 혹은 FILO(First in Last out)이라고 하는데, 즉, 가장 나중에 들어간 자료가 가장 먼저 나오는 구조이다. 예를 들어 택배 상자를 화물차에 쌓는다면, 아래부터 차곡차곡 쌓아서 나중에 뺄때는 가장 위의 상자를 들게 되는 것, 혹은 편의점 냉장고 음료수를 맨 앞부터 빼가고, 다시 맨 앞부터 채워지는 것과 같은 구조이다.

(그림 추가)

Push Pop empty라는 함수를 많이 쓴다.

- Push: 맨 뒤로 자료를 넣어주는 것

- Pop: 가장 마지막에 들어온 구조를 하나 빼주는 것

- empty: 자료가 더이상 없을 때 

### Stack 함수 구현하기

```c
#include <stdio.h>
 
#define MAX 4
 
int Stack[MAX];
int Sp = MAX;//FD스택
int N;
int A[20 + 10];
 
int Push(int d) {
    // 여기서부터 작성
    if (Sp == 0) return -1;//Full이면 -1리턴
    Sp--;
    Stack[Sp] = d;
    return Sp;
}
 
int Pop(int *p) {
        if (Sp == MAX) return -1;//Empty이면 -1 리턴
        *p = Stack[Sp];
        Sp++;
        return Sp;
}
 
void InputData(void) {
    scanf("%d", &N);
    for (int i = 0; i < N; i++) scanf("%d", &A[i]);
}
 
void Solve(void) {
    for (int i = 0; i < N; i++) {
        if (A[i] > 0) {
            int r = Push(A[i]);
            if (r == -1) printf("-1 ");
        }
        else {
            //int r = Pop();
            int r, t;
            r = Pop(&t);
            if (r == -1) printf("-1 ");
            else printf("%d ", t);
        }
    }
}
 
int main(void) {
    InputData();
    Solve();
    return 0;
}
```

### Stack 함수 사용하기

```c
#include <stdio.h>

int stack[100000 + 10];
int sp = 0;//[0]번은 미사용, Empty로 판단
void push(int n) {
    sp++;
    stack[sp] = n; //1부터 쌓는다
}
int top(void) { return stack[sp]; }
void pop(void) { sp--; }
int empty(void) { return sp == 0; }
int size(void) { return sp; }
```



## Queue

큐는 선착순 대기 번호라 생각하면 이해가 쉽다. FIFO(first in first out)이라고 하는데, 가장 먼저 들어간 자료가 가장 먼저 나오는 구조이다. 예를 들어, 어떤 식당에 대기 순번을 예약하고 기다리면, 가장 먼저 기다린 사람 순서대로 빠지는 것과 같다.

(그림 추가)

### Queue 함수 구현하기

```c
#include <stdio.h>
 
#define MAX 5
// 큐 배열
int Queue[MAX];
// Write point
int Wp = 0;
// Read point
int Rp = 0;
 
int N;
int a[20 + 10];
 
int In_Queue(int d)
{
    if (Wp == MAX) return 0; // 큐가 Full이면 0을 리턴
    Queue[Wp] = d; // 큐의 Wp에 d를 입력
    Wp++;
    return 1;
}
 
int Out_Queue(void)
{
    if (Rp == Wp) return 0; //큐가 Empty이면 0을 리턴
    int p;
    p = Queue[Rp]; // 큐의 Rp에 있는 값을 리턴
    Rp++;
    return p;
}

int main(void)
{
    int i, r, d;
 
    scanf("%d", &N);
    for (i = 0; i < N; i++) scanf("%d", &a[i]);
 
    for (i = 0; i < N; i++)
    {
        if (a[i] > 0)
        {
            r = In_Queue(a[i]);
            if (r == 0) printf("-1 ");
        }
        else
        {
            r = Out_Queue();
            if (r == 0) printf("-1 ");
            else printf("%d ", r);
        }
    }
 
    return 0;
}
```

### Queue 함수 사용하기

```c
#include <stdio.h>

//큐
typedef struct {
    int r, c;//위치정보
}QUE;
 
QUE que[100 * 100 + 10];
int wp, rp;
 
QUE front(void) { return que[rp]; }
void pop(void) { rp++;}
int empty(void) { return rp == wp; }
void push(int r, int c) {
    que[wp].r = r; que[wp].c = c; wp++;
}
```

