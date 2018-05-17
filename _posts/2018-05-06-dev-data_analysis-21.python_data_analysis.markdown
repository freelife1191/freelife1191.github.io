---
layout: post
title: "[Python Data Analysis]21.여러 개의 DataFrame 합치기"
subtitle: "여러 개의 DataFrame 합치기"
categories: dev
tags: data_analysis
comments: true
---

## 여러 개의 DataFrame 합치기

서로 다른 두 개의 DataFrame을 하나로 합치는 작업은 두 가지 방식으로 구분할 수 있습니다.

- **concatenating(연결)**: 단순히 하나의 DataFrame에 다른 DataFrame을 연속적으로 붙이는 방식

- **merging(병합)**: 두 DataFrame에 공통적으로 포함되어 있는 하나의 열을 기준으로 삼아, 해당 열의 값이 동일한 두 개의 행들을 하나의 행으로 합치는 방식

#### Merging DataFrame

##### 열 기준 merging

두 개의 DataFrame을 다음과 같이 생성합니다.

```python
df1 = pd.DataFrame({d "key": list("bbacaab"),
                    "data1": range(7)})
df2 = pd.DataFrame({"key": list("abd"),
                    "data2": range(3)})
```

`df1`과 `df2`는 각각 **"key"**라는 열을 공통적으로 포함하고 있습니다. `pd.merge()` 함수를 사용하여, **"key"** 열을 기준으로 하여 두 DataFrame에 대한 merging을 수행합니다.

```python
pd.p merge(df1, df2, on="key")
```

**"key"** 열의 값이 'b'인 경우를 예로 들면, `df1`에서 **"key"** 열의 값이 'b'인 행을 찾고, `df2`에서 **"key"** 열의 값이 'b'인 행을 찾습니다. 이렇게 찾은 행들이 `df1`에서 3개, `df2`에서 1개 있으므로, 이들을 조합하여 새로운 행을 만들면 총 3가지 조합이 발생하므로 merging 결과 3개의 행이 추가되었습니다. **"key"** 열의 값이 'c'나 'd'인 행은 한 쪽 DataFrame에만 존재하므로 merging 결과에는 추가되지 않았습니다.

관계형 데이터베이스(RDBMS)를 다뤄보신 분이라면, 위에서 `pd.merge(df1, df2, on="key")`를 실행한 결과가 'inner join' 연산을 수행한 결과임을 확인하실 수 있습니다.

한편 `pd.merge()` 함수의 how 인자의 값을 달리 입럭하면, 방금 전과는 다른 조합 방식에 따라 새로운 행들을 생성합니다.

```python
pd.p merge(df1, df2, on="key", how="outer")
```

위를 실행하면 **"key"** 열의 값이 'a'와 'b'인 행들의 경우 앞선 결과에서와 동일한데, 'c'를 가지는 행과 'd'를 가지는 행이 새로 추가되었습니다. 이렇게 `how="outer"` 인자를 넣는 경우, 한 쪽 DataFrame에만 존재하는 **"key"** 열의 값에 대해서도 새로운 행을 생성하되, 해당 **"key"** 값이 존재하지 않는 DataFrame의 열에 해당하는 부분은 NaN이 들어갑니다. 이는 곧 관계형 데이터베이스에서 'outer join' 연산을 수행한 결과입니다.

```python
pd.p merge(df1, df2, on="key", how="left")
```

한편 `how="left"` 인자를 넣는 경우, `pd.merge()` 함수의 첫 번째 인자에 해당하는 DataFrame을 기준으로 삼아 merging을 수행합니다. 이 경우 기준이 되는 `df1`의 **"key"** 값이 'b'일 때, `df2`에서 **"key"** 값이 'b'인 행을 `df1`의 행에 붙이는 식으로 새로운 행을 구성합니다. 이 때 `df1`에는 **"key"** 값이 'c'인 경우도 존재하나 이는 `df2`에 존재하지 않으므로, `df2`의 열인 "data2"에는 NaN이 들어갑니다. 관계형 데이터베이스에서는 'left join' 연산을 수행한 결과입니다.

`how="right"` 인자를 넣고 실행할 수도 있는데, 이 경우 `pd.merge()` 함수의 두 번째 인자에 해당하는 DataFrame을 기준으로 삼아 merging을 수행합니다.

한편, merging하고자 하는 기준 열의 이름이 다르더라도 merging을 수행할 수 있습니다. 두 DataFrame을 생성합니다.

```python
df3 = pd.DataFrame({d "lkey": list("bbacaab"),
                    "data1": range(7)})
df4 = pd.DataFrame({"rkey": list("abd"),
                    "data2": range(3)})
```

`pd.merge()` 함수를 사용할 때, `left_on="lkey"`, `right_on="rkey"`를 명시하여 첫 번째 DataFrame의 기준 열과 두 번째 DataFrame의 기준 열을 직접 명시하면 됩니다.

```python
pd.p merge(df3, df4, left_on="lkey", right_on="rkey")
```

#### 인덱스 기준 merging

merging의 대상이 되는 DataFrame 상에서 인덱스를 기준으로 삼고자 하는 경우에도 앞에서 설명한 방법과 크게 다르지 않습니다. 새로운 두 DataFrame을 생성합니다.

```python
left1l  = pd.DataFrame({'key': ['a', 'b', 'a', 'a', 'b', 'c'], 'value': range(6)})
right1 = pd.DataFrame({'group_val': [3.5, 7]}, index=['a', 'b'])
```

`left1`에서는 **"key"** 열을, `right1`에서는 인덱스를 기준으로 merging을 수행하고자 할 경우, 다음과 같이 실행하면 됩니다.

```python
pd.merge(left1, right1, left_on=p "key", right_index=True)
```

첫 번째 인자로 명시된 `left1`의 경우 **"key"** 열을 기준으로, 두 번째 인자로 명시된 `right1`의 경우 인덱스를 기준으로 merging을 하라는 것입니다. 만약 두 DataFrame의 순서가 뒤바뀌는 경우, `right_index=True` 대신 `left_index=True`, `left_on="key"` 대신 `right_on="key"` 인자를 넣어주시면 됩니다.

두 DataFrame 모두 인덱스 기준으로 mergingdmf 수행하고자 할 경우, 다음과 같이 하면 됩니다.

```python
left2 = pd.l DataFrame([[1., 2.], [3., 4.], [5., 6.]], 
                     index=['a', 'c', 'e'], columns=['Seoul', 'Incheon'])
right2 = pd.DataFrame([[7., 8.], [9., 10.], [11., 12.], [13, 14]],
                      index=['b', 'c', 'd', 'e'], columns=['Daegu', 'Ulsan'])
pd.merge(left2, right2, how="outer", left_index=True, right_index=True)
```

#### Concatenating DataFrame

Concatenating은 쉽게 말해서 하나의 DataFrame에 다른 DataFrame을 행 방향 또는 열 방향으로 단순 연결하는 것입니다. 다음과 같은 3개의 Series를 생성합니다.

```python
s1s  = pd.Series([0, 1], index=["a", "b"])
s2 = pd.Series([2, 3, 4], index=["c", "d", "e"])
s3 = pd.Series([5, 6], index=["f", "g"])
```

`pd.concat()` 함수를 사용하여 3개의 Series를 연결하면, 단순히 1차원적으로 순서대로 연결된 새로운 Series가 생성됩니다.

```python
pd.concatp ([s1, s2, s3])
```

`pd.concat()` 함수의 axis=1 인자를 명시하면, Series가 2차원적으로 연결되면서 DataFrame이 생성됩니다.

```python
pd.concatp ([s1, s2, s3], axis=1)
```

`s1`의 인덱스를 일부 포함하는 새로운 `s4` Series를 하나 생성하고, 다시 concatenating을 진행하면, `s4`와 `s1`이 공유하는 인덱스인 'a'와 'b'의 경우 같은 행 상에서 연결된 것을 확인할 수 있습니다.

```python
s4s  = pd.concat([s1 * 5, s3])
pd.concat([s1, s4], axis=1)
```

concatenating을 진행할 때, 연결된 DataFrame에 컬럼을 다음과 같이 명시해줄 수도 있습니다.

```python
pd.concatp ([s1, s2, s3], axis=1, keys=["one", "two", "three"])
```

두 개의 DataFrame에 대해서도 완전히 동일한 방식으로 concatenating이 가능합니다.

```python
df1 = pd.d DataFrame(np.arange(6).reshape(3, 2), 
                   index=['a', 'b', 'c'], columns=['one', 'two'])
df2 = pd.DataFrame(5 + np.arange(4).reshape(2, 2), 
                   index=['a', 'c'], columns=['three', 'four'])
pd.concat([df1, df2], axis=1)
```

행 방향으로 concatenating을 수행할 때 기존 DataFrame의 인덱스가 유지되었는데, `pd.concat()` 함수에서 `ignore_index=True` 인자를 넣어주면 기존의 인덱스를 무시하고 새로운 인덱스를 붙여줍니다.

```python
df3 = pd.DataFrame(npd .random.randn(3, 4), columns=['a', 'b', 'c', 'd'])
df4 = pd.DataFrame(np.random.randn(2, 3), columns=['b', 'd', 'a'])
pd.concat([df3, df4], ignore_index=True)
pd.concat([df3, df4])
```