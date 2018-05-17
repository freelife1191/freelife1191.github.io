---
layout: post
title: "[Python Data Analysis]15.DataFrame 데이터 분석용 함수 사용하기"
subtitle: "DataFrame 데이터 분석용 함수 사용하기"
categories: dev
tags: data_analysis
comments: true
---
## DataFrame 데이터 분석용 함수 사용하기

### 통계 함수

pandas의 DataFrame에서는 다양한 통계 함수를 지원합니다. DataFrame을 사용하여 데이터 분석을 할 때 가장 중요한 기능이라고 할 수 있겠습니다.

```python
data = [[d 1.4, np.nan],
           [7.1, -4.5],
        [np.nan, np.nan],
        [0.75, -1.3]]
df = pd.DataFrame(data, columns=["one", "two"], index=["a", "b", "c", "d"])
```

`df`라는 DataFrame을 정의하여, **'행 방향'** 또는 **'열 방향'**의 합을 구하도록 할 수 있습니다. `df.sum(axis=0)`을 실행하면 '행 방향'으로 성분들의 합을 구하게 되며, `df.sum(axis=1)`을 실행하면 **'열 방향'**으로 성분들의 합을 구하게 됩니다. 이렇게 별다른 옵션 지정 없이 `.sum()` 함수를 그냥 호출할 경우, 기본적으로 NaN은 배제하고 합을 계산합니다.

특정 행 또는 특정 열에 대해서만 합을 계산할 수도 있습니다. `df["one"].sum()`을 실행하면 **'one' **열의 합만을 얻을 수 있으며, `df.loc["b"].sum()`을 실행하면 **'b'** 행의 합만을 얻을 수 있습니다.

평균이나 분산 등의 경우 사용하는 함수만 달라질 뿐, 방식은 완전히 동일합니다. 각각 `.mean()`과 `.var()` 함수를 사용하면 됩니다.

만약 NaN을 모두 감안해서 통계량을 산출하고 싶다면, 통계 함수에 `skipna=False`라는 인자를 추가로 입력하면 됩니다. 예를 들어 `df.mean(axis=1, skipna=False)`를 실행하고 그 결과를 관찰해 보면, NaN이 포함된 행은 평균값이 제대로 계산되지 않고 NaN이라고 표시되어 있는 것을 확인할 수 있습니다.

#### pandas의 DataFrame에 적용되는 통계 함수 정리

| 함수           | 설명                                                         |
| -------------- | ------------------------------------------------------------ |
| count          | 전체 성분의 (NaN이 아닌) 값의 갯수를 계산                    |
| min, max       | 전체 성분의 최솟, 최댓값을 계산                              |
| argmin, argmax | 전체 성분의 최솟값, 최댓값이 위치한 (정수)인덱스를 반환      |
| idxmin, idxmax | 전체 인덱스 중 최솟값, 최댓값을 반환                         |
| quantile       | 전체 성분의 특정 사분위수에 해당하는 값을 반환 (0~1 사이)    |
| sum            | 전체 성분의 합을 계산                                        |
| mean           | 전체 성분의 평균을 계산                                      |
| median         | 전체 성분의 중간값을 반환                                    |
| mad            | 전체 성분의 평균값으로부터의 절대 편차(absolute deviation)의 평균을 계산 |
| std, var       | 전체 성분의 표준편차, 분산을 계산                            |
| cumsum         | 맨 첫 번째 성분부터 각 성분까지의 누적합을 계산 (0에서부터 계속 더해짐) |
| cumprod        | 맨 첫번째 성분부터 각 성분까지의 누적곱을 계산 (1에서부터 계속 곱해짐) |

이들 통계 함수를 사용하여 DataFrame의 결측값을 채울 수도 있습니다. 예를 들어 **'one'** 열의 NaN은 나머지 값들의 평균값으로, **'two'** 열의 NaN은 해당 열의 최솟값으로 대체하고자 한다고 가정합시다. 다음과 같이 실행하면, **'one'** 열과 **'two'** 열의 결측값들이 각각 의도했던 대로 채워질 것입니다.

```python
one_mean = df.mean(axis=o 0)["one"]
two_min = df.min(axis=0)["two"]
df["one"] = df["one"].fillna(value=one_mean)
df["two"] = df["two"].fillna(value=two_min)
```

DataFrame에서 특히 유용한 통계 함수 중 하나가, **상관 계수(correlation coefficient)** 혹은 **공분산(covariance)**을 계산하는 함수입니다. 새로운 `df2` DataFrame을 정의합니다.

```python
df2 = pd.DataFrame(npd .random.randn(6, 4),
      columns=["A", "B", "C", "D"],
      index=pd.date_range("20160701", periods=6))
```

`df2`에서 'A' 열의 데이터와 'B' 열의 데이터 간의 상관계수를 산출하고자 할 경우, `df2["A"].corr(df2["B"])`을 실행하면 됩니다. 같은 방식으로, 'B'열 데이터와 'C'열 데이터 간의 공분산을 산출하고자 할 경우 `df2["B"].cov(df2["C"])`을 실행하면 됩니다.

혹은 특정한 두 개의 열을 명시할 필요 없이, `df2.corr()` 또는 `df2.cov()`를 실행하면 `df2`의 모든 열들 간의 상관계수 및 공분산을 한 번에 계산해 줍니다. 데이터 분석 시 어느 한 변수가 다른 변수에 미치는 영향 등을 알고자 할 때, 이러한 상관 분석이 대단히 유용할 수 있습니다.

### 정렬 함수 및 기타 함수

#### 정렬 함수

pandas의 DataFrame에서는 인덱스 기준 정렬과 값 기준 정렬을 지원합니다. 기존 `df2`의 인덱스와 컬럼 순서를 무작위로 섞어보도록 하겠습니다.

```python
datesd  = df2.index
random_dates = np.random.permutation(dates)
df2 = df2.reindex(index=random_dates, columns=["D", "B", "C", "A"])
```

`df2`를 확인하면, 인덱스와 컬럼의 순서가 불규칙하게 변화한 것을 확인할 수 있습니다. 실제로 시계열 데이터같은 경우에도 이렇게 시간에 따라 제대로 정렬되어 있지 않은 데이터셋을 얻을 가능성이 존재합니다.

이 때 인덱스가 오름차순이 되도록 행들을 정렬하고 싶은 경우, `df2.sort_index(axis=0)`을 실행하여 '행 방향'으로의 정렬을 수행합니다. 만약 컬럼이 오름차순이 되도록 열들을 정렬하고 싶은 경우, `df2.sort_index(axis=1)`을 실행하여 '열 방향'으로의 정렬을 수행합니다.

만약 인덱스가 내림차순이 되도록 행들을 정렬하고 싶은 경우, `df2.sort_index(axis=0, ascending=False)`와 같이 `ascending=False` 인자를 추가로 입력해 주면 됩니다.

다음으로 값 기준 정렬입니다. 예를 들어 'D'열의 값이 오름차순이 되도록 행들을 정렬하고 싶은 경우, `df2.sort_values(by="D")`를 실행합니다. 만약 'B'열의 값이 내림차순이 되도록 행들을 정렬하고 싶은 경우, `df2.sort_values(by="B", ascending=False)`를 실행하면 됩니다.

```python
df2[d "E"] = np.random.randint(0, 6, size=6)
df2["F"] = ["alpha", "beta", "gamma", "gamma", "alpha", "gamma"]
```

`df2`에 'E'열과 'F'열을 추가한 뒤, 'E' 열과 'F' 열의 값을 동시에 기준으로 삼아 각각 오름차순이 되도록 행들을 정렬하고 싶은 경우, `df2.sort_values(by=["E", "F"])`와 같이 여러 개의 컬럼을 리스트 형태로 명시해 주면 됩니다.

#### 기타 함수

`df.unique()` 함수는 지정한 행 또는 열에서 중복을 제거한 유니크한 값들만을 제시하는 함수입니다.

```python
uniquesu  = df2["F"].unique()
```

`df.value_counts()` 함수는 특정한 행 또는 열에서 값에 따른 갯수를 제시하는 함수입니다.

```python
dfd 2["F"].value_counts()
```

`df.isin()` 함수를 사용하면, 특정한 행 또는 열의 각 성분이 특정한 값들을 포함되어 있는지 확인할 수 있으며, 불리언 마스크를 반환합니다. 그래서 이렇게 얻은 불리언 마스크를 사용하여, 원하는 행만을 선택할 수도 있습니다.

```python
df2[d "F"].isin(["alpha", "beta"])
df2.loc[df2["F"].isin(["alpha", "beta"]), :]
```

#### 사용자 정의 함수

사용자가 직접 정의한 함수를 DataFrame의 행 또는 열에 적용하는 방법에 대해 알아보도록 하겠습니다. 새로운 `df3` DataFrame을 먼저 정의합니다.

```python
df3 = pd.DataFrame(npd .random.randn(4, 3), columns=["b", "d", "e"],
                   index=["Seoul", "Incheon", "Busan", "Daegu"])
```

lambda 함수를 정의한 뒤, 이를 `func` 변수에 저장합니다. 이 때 `func` 함수는, 해당 행 또는 열에서의 최댓값 - 최솟값을 계산하는 함수입니다.

```python
funcf  = lambda x: x.max() - x.min()
```

`df.apply()` 함수를 사용하여 해당 함수 인자로 `func`를 명시하면, 해당 DataFrame의 각 행 또는 열에 대하여 `func` 함수를 적용하고 그 결과값을 얻을 수 있습니다. 예를 들어 `df3.apply(func, axis=0)`을 실행하면 이를 '행 방향'으로 진행한 결과를, `df3.apply(func, axis=1)`을 실행하면 이를 '열 방향'으로 진행한 결과를 얻습니다.