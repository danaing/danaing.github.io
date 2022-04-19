---
layout: post
title:  파이썬 자료형 정리
subtitle: 맨날 검색하던 파이썬 자료구조 한방에 정리
date:   2022-03-19
author: danahkim
categories: Python
tags: Data-type
---


프로그래밍의 기본은 사용하는 언어의 자료형을 아는 것이다. 매번 필요할 때 마다 검색하며 찾아봤던 파이썬 자료형의 특징과 메소드에 대해 한번에 정리해보려 한다. 숫자형(Number), 문자형(String), 불(Bool) 자료형을 제외하고 아래 4가지 자료형을 하나씩 살펴본다.

1. 딕셔너리(Dictionary)
1. 집합(Set)
1. 튜플(Tuple)
1. 리스트(List)

- Container객체
    - 순서 정보를 포함하지 않는 Container객체
        - 특징: 컨테이너 안에 어떤 요소가 있는지 확인 가능(in)
    - 딕셔너리, 집합
- Sequence객체
    - 순서를 가진 Container객체
        - 특징: 인덱싱, 슬라이싱, 연산 가능
    - 리스트, 튜플

## 딕셔너리(Dictionary)

딕셔너리는 이름에서 알 수 있듯 사전과 같다. 특정 단어의 뜻을 가지고 있는 사전처럼 특정 key에 특정 value를 가지고 있다.


💡 **{key1: value1, key2: value2, key3: value3, ...}**

- key: 값을 찾기 위해 넣어주는 데이터
- value: 찾고자 하는 데이터


이 때 리스트는 key가 될 수 없다. 변할 수없는 값만이 key가 될 수 있다. 만약 key를 수정하려면 수정이 안되기 때문에 원래 있는 값을 지우고 새로운 값을 넣어준다.

```python
my_dict = {
 'apple': '사과',
 'book': '책',
 'human': '사람'
}
print(my_dict)
# {'apple': '사과', 'book': '책', 'human': '사람'}
```

- `dict.keys()`: Key 리스트 반환
- `dict.values()`: value 리스트 반환
- `dict.items()`: key, value 쌍으로 된 튜플 리스트 반환

```python
my_dict.keys()
# dict_keys(['apple', 'book', 'human'])

my_dict.values()
# dict_values(['사과', '책', '사람'])

my_dict.items()
# dict_items([('apple', '사과'), ('book', '책'), ('human', '사람')])
```

딕셔너리의 장점은 원하는 데이터(key)에 맞는 값(value)를 빠르게 찾을 수 있다는 점이다. 만약 리스트였다면 아래처럼 for문을 사용해서 하나 하나씩 다 조회해야하므로 엄청 오래걸린다.

```python
# 딕셔너리에서 조회하기
print(my_dict['apple'])
# '사과'

# 리스트에서 조회하기
eng_kor = [
    ('apple', '사과'), 
    ('book', '책'), 
    ('human', '사람')
]
for eng, kor in eng_kor:
    if eng == 'apple':
        print(kor)
# '사과'
```

### 해당 키가 안에 있는지 조사

- `'key' in dict` : dict 안에 key가 있는지 True, False(bool값) 리턴
- `dict.get('key')`: dict 안에 key에 매칭되는 값이 없다면 None을 리턴, 매칭되는 값이 있다면 해당 value을 리턴

```python
'book' in my_dict
# True

'cat' in my_dict
# False

my_dict.get('book')
# '책'

my_dict.get('cat')
# (아무것도 리턴하지 않음)
```

### 딕셔너리 메소드

- `dict['추가할 key'] = '추가할 value'`: 딕셔너리 추가
- `del dict[’삭제할 key’]`: 딕셔너리 삭제
- `a.update(b)`: a의 딕셔너리에 b의 딕셔너리를 뒤에 붙여줌
- `dict.clear()`: 딕셔너리 초기화
- `dict.copy()`: 딕셔너리 복제

## 집합(Set)

집합에 관련된 것을 쉽게 처리하기 위해 만든 자료형이다.

💡 **{요소1, 요소2, 요소3, 요소4, ...}**

- 특징
    - **중복을 허용하지 않는다.**
    - 순서가 없다. 따라서 인덱싱을 지원하지 않는다.
        - 인덱싱을 원한다면 튜플이나 리스트형으로 변환하여 사용해야한다.

```python
s1 = set([1,2,3])
print(s1)
# {1, 2, 3}

s2 = set([1,1,2,3])
print(s2)
# {1, 2, 3}

s3 = set('Hello, world!')
print(s3)
# {'o', 'd', 'r', 'l', ',', 'e', 'H', '!', 'w', ' '}

l1 = list(s3)
print(l1[0])
# 1
```

### 집합 연산

set1 집합과 set2 집합의 연산이다.

- 교집합: `set1 & set2` , `set1.intersection(set2)`
- 합집합: `set1 | set2` , `set1.union(set2)`
- 차집합: `set1 - set2` , `set1.difference(set2)`
- 대칭차집합: `set1 ^ set2` , `set1.symmetric_difference(set2)`

### 원소 추가/삭제

- `set.add(원소)`: 원소 하나 추가
- `set.update([원소1, 원소2, 원소3])`: 여러 원소 추가
- `set.remove(원소)`: (반드시 존재하는) 원소 삭제 (존재하지 않으면 오류)
- `set.pop()`: 맨 마지막 값 제거
- `set.discard()`: 원소 삭제

## 튜플(Tuple)

여러 값을 모아 저장할 수 있으며, 순서 정보를 가지고 있는 자료형 중 가장 기본적인 타입은 튜플이다. 리스트와는 다르게 한번 생성한 튜플은 **그 값을 변경하거나 삭제하는 것이 불가능하다.**

튜플을 생성하는 방법은 괄호()를 이용한다.


💡 **(요소1, 요소2, 요소3, 요소4, ...), tuple()**



### 인덱싱과 슬라이싱

```python
t = (1, 2, 'a', 'b')
t[0]
# 1
t[1:]
# (2, 'a', 'b')
t[-1]
# 'b'
```

### 튜플 연산

```python
t1 = (1, 2, 'a', 'b')
t2 = (3, 4)
t1 + t2
# (1, 2, 'a', 'b', 3, 4)
t1 * 2
# (1, 2, 'a', 'b', 1, 2, 'a', 'b')
```

### 튜플 메소드

- `tuple.index()`: 특정 값의 인덱스 반환
- `tuple.count()`: 특정 값의 갯수 반환
- `len(tuple)`: 튜플 개수 반환

## 리스트(List)

튜플은 유용하고 빠르지만, 한번 생성하면 값을 추가하거나, 삭제할 수 없기 때문에 자유롭게 사용할 수 없다. 리스트는 인덱싱이 가능한 튜플과 비슷하지만 값의 변경이 가능하다. 리스트 생성은 대괄호[]를 이용한다.


💡 **[요소1, 요소2, 요소3, 요소4, ...], list()**

### 리스트 수정

- `list.append(추가할 요소)`: 맨 뒤에 순서대로 추가
- `list.insert(인덱스, 요소)`: 인덱스에 요소를 삽입
- `del list[인덱스]`: 인덱스 위치의 요소 삭제
- `list.remove(삭제할 요소)`: 요소 삭제
- `list.pop()`: 마지막 요소 반환 및 삭제
- `list1.extend(list2)`: list1과 list2 병합

```python
a = [1, 2, 3, 4]
a.append(5)
a
# [1, 2, 3, 4, 5]
a[2] = 'three'
a
# [1, 2, 'three', 4, 5]
```

### 리스트 메소드

- `요소 in list`: 요소가 리스트 안에 있는지 조회
- `list.index(요소)`: 요소의 인덱스 반환
- `list.count(요소)`: 요소의 개수 확인
- `‘, ‘.join(list)`: 쉼표(,)를 기준으로 리스트 안에 요소를 1개의 문자열로 만들어 반환
- `sorted(list)`: 정렬한 리스트 반환
- `list.sort()`: 리스트 자체를 정렬
- `len(list)`: 리스트 개수 반환

## References

- [https://wikidocs.net/book/1](https://wikidocs.net/book/1)
- [https://wikidocs.net/book/2067](https://wikidocs.net/book/2067)