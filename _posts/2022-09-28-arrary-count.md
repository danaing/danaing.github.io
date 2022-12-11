---
layout: post
title:  "Array의 요소 개수 세는 방법 3가지"
subtitle: value_counts, Counter, count 매서드 정리
date:   2022-09-28
author: danahkim
categories: Data-Science
tags: Python
---

>  파이썬에서 데이터를 분석하면서 마주쳤던 곤란한 상황과 그 해결 방법에 대해 정리하고자 한다.

DataFrame의 컬럼은 `value_counts()`를 이용해서 숫자를 셀 수 있다. 데이터 분석을 하면서 편리하기 때문에 자주 이용하는 메서드이다. 그런데 여기서 문제는, **Scikit-learn**을 이용하여 classification한 label은 **numpy의 array형으로 반환**되기 때문에 `value_counts()`를 사용하면 아래처럼 오류가 난다는 것이다.

```
>> AttributeError: 'numpy.ndarray' object has no attribute 'value_counts'
```

## Array의 요소 개수 세기

먼저 array에 있는 요소의 수를 세는 방법 3가지를 정리했다.

* `value_counts()`: pandas의 **series**형에 사용 가능한 메서드로 요소 별 개수를 테이블로 반환한다.  normalize = True를 옵션으로 넣으면 퍼센티지로 보여준다.
* `collections.Counter()`: **array**를 괄호 안에 넣으면 요소 별 개수를 딕셔너리 형으로 반환한다.
* `count()`: **문자열**, **리스트**에서 괄호 안에 찾고자 하는 값을 입력하면 해당 값의 개수를 숫자로 반환하는 메서드이다.

## Scikit-learn의 label 세기

따라서 scikit-learn의 kmeans모델로 classification이 된 label의 요소 개수를 셀 때는 아래처럼 3가지 방법이 가능하다.

### 1. value_counts() 사용하는 방법

```python
import pandas as pd
pd.Series(kmeans.labels_).value_counts()
>> 0    2726
   2    1068
   1     499
   dtype: int64
```

### 2. Counter() 사용하는 방법

```python
from collections import Counter
Counter(kmeans.labels_)
>> Counter({2: 1068, 1: 499, 0: 2726})
```

### 3. count() 사용하는 방법

```python
kmeans.labels_.tolist().count(0)
>> 2726
kmeans.labels_.tolist().count(1)
>> 499
kmeans.labels_.tolist().count(2)
>> 1068
```

