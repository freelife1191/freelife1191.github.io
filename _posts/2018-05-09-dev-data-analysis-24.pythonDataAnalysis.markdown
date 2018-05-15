---
layout: post
title: "[Python Data Analysis]24.데이터 그룹화 함수 이해하기"
subtitle: "데이터 그룹화 함수 이해하기"
categories: dev
tags: data-analysis
comments: true
---

## 데이터 그룹화 함수 이해하기

### 그룹화의 개념 이해하기

#### split-apply-combine
```python
df = pd.DataFrame({'key1' : ['a', 'a', 'b', 'b', 'a'],
                   'key2' : ['one', 'two', 'one', 'two', 'one'],
                   'data1': np.random.randn(5),
                   'data2': np.random.randn(5)})
```
예를 들어 여러분이 df 상에서 "key1" 열의 값이 'a'인 행에 대해서만, 그리고 'b'인 행에 대해서만 "data1" 열 값의 평균을 각각 계산하고자 한다고 합시다. 데이터 그룹화는 이런 작업을 쉽고 빠르게 할 수 있도록 하는 기능입니다. 데이터 그룹화를 하기 위해서 Series 혹은 DataFrame에 대하여 `.groupby()`함수를 사용합니다.

```python
grouped = df["data1"].groupby(df["key1"])
```
위 코드를 해석하자면, `df`의 "data1" 열을 사용하여 통계량을 계산할 것인데, 이 때 "key1" 열의 값을 기준으로 데이터를 먼저 그룹화한 뒤, 이들 각각의 그룹에 대하여 "data1" 열의 통계량을 계산한다는 의미입니다.


이렇게 생성된 `grouped` 변수를 확인해보면, `SeriesGroupBy` 객체라는 것만 표시되며 그 내용은 확인할 수가 없습니다. 왜냐하면, 현재 "key1" 열의 값을 기준으로 그룹화까지만 진행했을 뿐, 어떤 통계 연산을 수행할지를 명시해주지 않은 상태이기 때문입니다. `grouped` 변수에 `.mean()` 함수를 적용하면, 비로소 "key1" 열의 값을 기준으로 그룹화된 각각의 그룹에 대하여 "data1" 열 값의 평균을 산출한 결과를 얻을 수 있습니다.

```python
grouped.mean()
```
pandas에서의 모든 그룹화의 흐름은 이렇게 흘러가는데, 이를 **"split-apply-combine"**이라는 키워드로 표현하기도 합니다. 그룹화하고자 하는 열의 값을 기준으로 데이터를 나누고(split), 각 그룹에 대한 통계 함수를 적용하여(apply), 최종적인 통계량을 산출한 결과를 하나로 통합하여 표시하는(combine) 과정을 거치기 때문입니다.


"data1" 열에 대한 통계량을 산출하는데, 이 때 그룹화의 기준으로 "key1"과 "key2" 열의 값을 동시에 사용하고, 여기에 `.mean()` 함수를 적용하여 각 그룹에 대하여 평균을 계산한 결과를 얻을 수 있습니다.

```python
means = df["data1"].groupby([df["key1"], df["key2"]]).mean()
means.unstack()
```
지금까지의 `.groupby()` 함수의 호출 방식은, 해당 함수를 호출하는 대상과 해당 함수의 인자로 들어가는 대상이 `df["data1"]`과 같이 모두 Series인 경우의 방식이라고 할 수 있습니다. `.groupby()` 함수를 DataFrame에 대해서도 적용할 수 있는데, 위에서 했던 것과 방식이 약간은 달라집니다.

```python
df.groupby("key1").mean()
df.groupby("key1").count()
```

DataFrame에 대한 그룹화 결과, 그룹화 기준이 되는 열을 제외한 나머지 모든 열에 대한 통계량이 계산되었습니다. "key1"과 "key2" 열을 동시에 기준으로 삼아 그룹화하는 경우에도, 동일한 방식으로 하면 됩니다.

```python
df.groupby(["key1", "key2"]).mean()
df.groupby(["key1", "key2"]).count()
```

만약 그룹화 후 특정한 열 값에 대해서만 통계량을 산출하고 싶다면, 다음과 같이 하면 됩니다.

```python
df.groupby(["key1", "key2"])["data2"].mean()
```

그룹에 대해 반복문 사용하기

위에서는 그룹화를 수행한 직후의 결과물을 직접 확인할 수 없었는데, 그룹에 대해 반복문을 수행하면 그룹화된 결과물에 대한 확인이 가능합니다.

```python
for name, group in df.groupby("key1"):
    print(name)
    print(group)
```

`df.groupby("key1")`을 실행한 결과를 반복문에서 순회할 대상으로 명시한 뒤, name과 group 변수에서 값을 받도록 한 뒤 이들 값을 출력하면, 그룹화 기준 열의 값과 그룹화된 결과물을 직접 확인할 수 있습니다. 그룹화 기준 열이 2개인 경우에도 방식은 유사합니다.

```python
for (k1, k2), group in df.groupby(["key1", "key2"]):
    print(k1, k2)
    print(group)
```

그룹화 결과물을 반복문으로 보기 불편한 경우, 아예 딕셔너리 형태로 얻을 수도 있습니다.

```python
pieces = dict(list(df.groupby("key1")))
```

#### 딕셔너리 혹은 Series 기준으로 그룹화하기

그룹화를 수행하기 위한 기준으로, 별도로 정의된 딕셔너리 혹은 Series를 사용할 수 있습니다.

```python
df2 = pd.DataFrame(np.random.randn(5, 5), 
                   columns=['a', 'b', 'c', 'd', 'e'],
                   index=['Joe', 'Steve', 'Wes', 'Jim', 'Travis'])
map_dict = {'a': 'red', 'b': 'red', 'c': 'blue', 
            'd': 'blue', 'e': 'red', 'f' : 'orange'}
```

`df2`를 생성할 때 `map_dict`라는 딕셔너리도 함께 생성하였는데, 이는 컬럼을 다른 문자열로 매핑하는 역할을 합니다. 해당 딕셔너리를 `df.groupby()` 함수의 인자로 넣게 되면, 해당 딕셔너리에 명시된 내용을 기준으로 인덱스 혹은 컬럼을 그룹화합니다.

```python
df2.groupby(map_dict, axis=1).sum()
```

위와 같이 실행하면, 'a'부터 'e'까지의 열을 `map_dict`에 명시된 내용대로 'red'와 'blue'로 그룹화한 뒤, 이들 내에서의 합계를 산출하여 보여줍니다. 딕셔너리 대신 Series를 사용하여 동일한 작업을 수행할 수도 있습니다.

```python
map_s = pd.Series(map_dict)
df2.groupby(map_dict, axis=1).count()
```

그룹화 결과 얻어진 그룹들에 대하여 적용할 수 있는 통계 함수들을 다음과 같이 정리하였습니다.


##### 그룹에 적용할 수 있는 주요 통계 함수

| 함수        | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| count       | 각 그룹 내의 (NaN이 아닌) 값들의 갯수를 계산                 |
| sum         | 각 그룹 내의 (NaN이 아닌) 값들의 합을 계산                   |
| mean        | 각 그룹 내의 (NaN이 아닌) 값들의 평균을 계산                 |
| median      | 각 그룹 내의 (NaN이 아닌) 값들 중 중간값을 반환              |
| std, var    | 각 그룹 내의 값들의 표준편차, 분산을 계산                    |
| min, max    | 각 그룹 내의 값들 중 최솟값, 최댓값을 반환                   |
| prod        | 각 그룹 내의 (NaN이 아닌) 값들 전체의 곱을 계산              |
| first, last | 각 그룹 내의 (NaN이 아닌) 값들 중 맨 첫번째, 맨 마지막 값을 반환 |

#### 그룹에 사용자 정의 함수 사용하기

그룹화 결과 얻어진 그룹에 대하여 사용자가 정의한 집계 함수를 사용할 수도 있습니다.

```python
grouped = df.groupby("key1")
```

"key1" 열의 값을 기준으로 그룹화한 뒤, 이를 `grouped` 변수에 저장합니다. 그리고 다음과 같은 함수를 정의합니다.

```python
def peak_to_peak(arr):
    return arr.max() - arr.min()
```

`peak_to_peak()` 함수는 그룹 내 각 열의 최댓값에서 최솟값을 뺀 값을 계산합니다. `.agg()` 함수를 사용하면, 그룹에 대하여 사용자가 정의한 집계 함수를 적용할 수 있습니다.

```python
grouped.agg(peak_to_peak)
```

`.agg()` 함수를 사용할 때 위에서 언급했던 일반적인 통계 함수들도 사용할 수 있습니다. 이 경우 문자열의 형태로 통계 함수 이름을 넣습니다.

```python
grouped.agg("std")
```

한편 `.describe()` 함수를 사용하면 그룹에 대한 기본 통계량 계산 결과를 모두 보여주므로 높은 편의성을 제공합니다.

```python
grouped.describe()
```