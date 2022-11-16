---
layout: post
title:  "DataFrame의 중복 행 제거하기"
subtitle: drop_duplicates를 이용하여 중복행 제거하기
date:   2022-09-28
author: danahkim
categories: Data-Science
tags: Python pandas
---

>  파이썬에서 데이터를 분석하면서 마주쳤던 곤란한 상황과 그 해결 방법에 대해 정리하고자 한다.

사실 실무에서 데이터를 추출하고 전처리하는 많은 과정은 SQL 쿼리문을 통해 한다. 이 때 많은 테이블에서 여러 테이블을 join하여 분석할 데이터의 모습이 갖춰지곤 한다.

단순화시킨 예를 들어보자면 아래 테이블을 가지고 2개의 데이터프레임을 만들고 이를 join하고 싶은 것이다.

<img src="/assets/images/2022-09-28-python.asset/datatable.png" alt="datatable" style="zoom:50%;" />

```SQL
SELECT ID, COUNT(amt) AS amt_sum
FROM SALES
GROUP BY ID
```

```SQL
SELECT DISTINCT ID, country
FROM SALES
```

동일한 작업을 Python으로 만들어 merge하려는데, 중복을 제거한 unique한 행으로 추출이 안되어 join할 때 안되어 애를 먹은 적이 있다. SQL문의 distinct와 동일한 함수가 필요했던 것이다.



## DataFrame의 중복 행 제거

DataFrame의 중복 행을 제거하는 방법을 아래 메서드를 이용한다.

`df.drop_duplicates(subset=None, keep='first', inplace=False, ignore_index=False)`

- `subset` : 중복값을 검사할 열을 지정한다. default는 모든 열을 검사한다.
- `keep` : {first, last} 중복 제거를 할 때 남길 행의 위치이다.
- `inplace` : 원본 변경 여부이다.
- `ignore_index` : 원래 index를 무시할지 여부이다. `True`일 경우 index가 0,1,2, ... , n으로 새로 설정된다.



Python 코드로는 아래와 같은 모습이 된다.

```python
t_amt = df.groupby('ID')['amt'].sum()
t_cnty = df[['ID', 'country']].drop_dulicates()

df_m = pd.merge(t_amt, t_cnty, on='ID', how='inner')
```
