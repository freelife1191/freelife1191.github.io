---
layout: post
title: "[Python Data Analysis]22.DataFrame 계층적 인덱싱 이해하기"
subtitle: "DataFrame 계층적 인덱싱 이해하기"
categories: dev
tags: data_analysis
comments: true
---

## DataFrame 계층적 인덱싱 이해하기

### 계층적 인덱싱

계층적인 정보를 인덱스로 사용하고자 할 경우, Series 혹은 DataFrame에서 **'계층적 인덱싱(hierarchical indexing)'**을 활용할 수 있습니다.

#### Series의 계층적 인덱싱

```python
s = pd.s Series(np.random.randn(10),
    index=[["a", "a", "a", "b", "b", "b", "c", "c", "d", "d"],
    [1, 2, 3, 1, 2, 3, 1, 2, 2, 3]])
```

위와 같이 Series의 인덱스에 2차원 리스트 혹은 2차원 numpy array 등을 입력하게 되면, 두 층을 가지는 인덱스가 생성됩니다. s 인덱스의 맨 첫 번째 층에 'a'부터 'd'까지, 이들 각각에 대하여 정수 인덱스가 두 번째 층에 부여되어 있습니다.

계층적 인덱싱을 수행할 때의 원칙은, 항상 가장 상위 계층에 해당하는 맨 바깥쪽 인덱스부터 차례대로 인덱싱하는 것입니다. 예를 들어 `s["b"]`와 같이 첫 번째 층의 'b' 인덱스를 명시하면, 해당 인덱스의 하위 층에 있는 1부터 3까지의 인덱스와 값을 Series 형태로 얻습니다. `s["b":"c"]`와 같이 첫 번째 층에 범위 인덱싱을 적용할 수도 있습니다.

`s[("b", 3)]`을 실행하면 'b' 인덱스 하위 층의 3 인덱스에 해당하는 값을 얻습니다. 또는, `s[:, 2]`를 실행하면 모든 첫 번째 층의 인덱스에 대하여 하위 계층의 2 인덱스의 값들만으로 구성된 Series를 얻을 수 있습니다.

#### DataFrame의 계층적 인덱싱

```python
df = pd.d DataFrame(np.arange(12).reshape((4, 3)),
     index=[["a", "a", "b", "b"], 
     [1, 2, 1, 2]],
     columns=[["Seoul", "Seoul", "Busan"],
     ["Green", "Red", "Green"]])
```

위와 같이 DataFrame의 인덱스와 컬럼에 2차원 리스트 혹은 2차원 numpy array 등을 입력하게 되면, 두 층을 가지는 인덱스 혹은 컬럼이 생성됩니다. 복수 개 층의 인덱스와 컬럼에 이름을 붙일 때는, 다음과 같이 맨 바깥쪽의 인덱스와 컬럼부터 순서대로 붙이면 됩니다.

```python
dfd .index.names = ["key1", "key2"]
df.columns.names = ["city", "color"]
```

`df["Seoul"]`을 실행하면 첫 번째 층의 컬럼이 "Seoul"인 데이터를 DataFrame의 형태로 얻습니다. 기존의 두 번째 층의 컬럼 중 "Seoul"의 하위에 있던 것들만이 새로운 DataFrame의 형태로 얻어집니다. `df[("Seoul", "Green")]`을 실행하면, "Seoul" 컬럼 하위 층의 "Green" 컬럼에 해당하는 열을 Series 형태로 얻습니다. 해당 Series의 인덱스는 여전히 계층적인 형태임이 확인 가능합니다.

`df.loc["a"]`을 실행하면 첫 번째 층 인덱스가 "a"인 데이터를 DataFrame의 형태로 얻으며, `df.loc[("a", 1)]`을 실행하면 "a" 인덱스 하위 층의 1 인덱스에 해당하는 행을 Series 형태로 얻습니다. 이 때 해당 Series의 인덱스는 기존에 있던 계층적 컬럼이 들어왔습니다.

```python
dfd .loc["b", ("Seoul", "Red")]
df.loc[("b", 2), "Busan"]
df.loc[("b", 1), ("Seoul", "Green")]
```

#### 계층적 인덱스 기준 정렬

인덱스 기준 정렬은 계층적 인덱스가 존재하는 경우에도 여전히 가능합니다. `df.sort_index()` 함수에 `level`이라는 인자를 명시하는데, 여기에 몇 번째 층에 해당하는지를 나타내는 (0부터 시작하는) 정수를 입력하면 그 층의 인덱스를 기준으로 DataFrame이 정렬됩니다.

```python
df.sort_index(d axis=0, level=0)
df.sort_index(axis=0, level=1)
```

정수 인덱스로 명시하는 것이 번거롭다면, 원하는 인덱스 층의 이름을 직접 입력할 수도 있습니다.

```python
df.sort_index(d axis=0, level="key2")
```

`axis=1` 인자를 입력하면 컬럼에 대해서도 같은 작업이 가능합니다.

```python
df.sort_index(d axis=1, level=0)
df.sort_index(axis=1, level=1)
df.sort_index(axis=1, level="color")
```

계층적 컬럼 상에서 값 기준 정렬의 경우, 다음과 같이 할 수 있습니다.

```python
df.sort_values(d by=("Busan", "Green"))
```

#### 계층적 인덱스 상에서 통계 함수 적용

계층적 인덱스가 존재할 때 통계 함수를 적용하는 방식도 어느 정도 유사합니다. 예를 들어 특정 인덱스에 대한 합을 계산하고 싶은 경우, `df.sum()` 함수에 `level`이라는 인자를 추가로 명시하면 됩니다.

```python
df.sum(d axis=0, level=0)
df.sum(axis=0, level=1)
```

이 경우에도 마찬가지로, 원하는 인덱스 혹은 컬럼 층의 이름을 직접 입력할 수도 있습니다.

```python
df.mean(d axis=1, level="color")
```

#### DataFrame 내 컬럼-인덱스 간 변환

기존에 DataFrame에서 특정 열에 포함되어 있던 값을 계층적 인덱스로 변환하거나, 혹은 그 반대로 할 수 있습니다.

```python
df2 = pd.DataFrame({d 'a': range(7), 'b': range(7, 0, -1),
      'c': ['one', 'one', 'one', 'two', 'two', 'two', 'two'],
      'd': [0, 1, 2, 0, 1, 2, 3]})
```

`df2` DataFrame에서 'c'와 'd' 열의 값을 계층적 인덱스로 변환하고자 할 경우, `df.set_index()` 함수를 사용합니다.

```python
df3d  = df2.set_index(["c", "d"])
```

만약 'c'열과 'd'열의 값을 인덱스에도 넣으면서 기존 열을 그대로 유지하고 싶다면, `drop=False` 인자를 추가하면 됩니다.

```python
df2.set_index([d "c", "d"], drop=False)
```

현재 `df3`에는 계층적 인덱스가 있는 상황인데, `df3.reset_index()`를 실행하면 모든 인덱스를 컬럼으로 올리고 정수 인덱스로 대체합니다.

```python
df3d .reset_index()
```

#### Reshaping DataFrame

새로운 DataFrame을 생성하고, 인덱스와 컬럼의 이름을 지정합니다.

```python
df4 = pd.DataFrame(np.arange(d 6).reshape((2, 3)),
      index=['Seoul', 'Busan'], 
      columns=['one', 'two', 'three'])
df4.index.name = "city"
df4.columns.name = "number"
```

이 때 `df.stack()` 함수를 사용하면, DataFrame 상의 최하위 컬럼이 현재 DataFrame의 최하위 인덱스로 붙습니다. 만약 컬럼이 한 층인 경우, 이를 최하위 인덱스로 붙이면서 Series 형태로 변화합니다.

```python
df5d  = df4.stack()
```

`df.stack()` 함수의 경우 `df.set_index()` 함수와 혼동될 수 있는데, 둘은 엄연히 작동 방식이 다르므로 각각을 실행했을 때의 결과의 차이를 확실히 구별할 수 있어야 합니다. `df.set_index()` 함수는 기존의 인덱스를 새로 대체하면서, 지정한 **'열이 가질 수 있는 값'**들이 인덱스가 됩니다. 반면 `df.stack()` 함수의 경우 현재 열들의 이름, 즉 **'컬럼들 자체'**가 현재 인덱스의 최하위 인덱스로 붙습니다.

`df.unstack()` 함수는 `df.stack()` 함수와 반대의 작용을 하며, DataFrame 상의 최하위 인덱스를 최하위 컬럼으로 올려보냅니다.

```python
df5d .unstack()
```

만약 최하위 인덱스가 아니라 특정 층에 위치한 인덱스를 컬럼으로 올리고 싶은 경우, `df.unstack()` 함수에 `level` 인자의 값을 입력해주면 됩니다. 이 level 인자의 경우 `df.stack()` 함수에도 명시할 수 있습니다. 물론 이 경우에도 `level` 인자에 인덱스 층의 이름을 직접 입력해줄 수도 있습니다.

```python
df5.unstack(d level=0)
df5.unstack(level="city")
```

새로운 두 개의 Series를 생성한 뒤, 이들을 연결합니다.

```python
s1s  = pd.Series([0, 1, 2, 3], index=['a', 'b', 'c', 'd'])
s2 = pd.Series([4, 5, 6], index=['c', 'd', 'e'])
s3 = pd.concat([s1, s2], keys=["one", "two"])
```

`s3`의 "one", "two" 인덱스를 잘 보면 하위 층에 'c'와 'd'가 공통적으로 존재합니다. `s3.unstack()`을 실행하면 최하위 인덱스가 컬럼으로 올라가는데, 겹치는 인덱스가 알아서 처리됩니다.

```python
s3s .unstack()
```

인덱스와 컬럼이 좀 더 복잡하게 구성된 DataFrame을 살펴봅시다.

```python
df6d  = pd.DataFrame({"left": df5, "right": df5 + 5},
        columns=["left", "right"])
df6.columns.name = "side"
```

`df.unstack()`과 `df.stack()` 함수를 번갈아 사용하면서, DataFrame의 모양이 어떻게 변화하는지 직접 살펴보시길 바랍니다.

```python
df6.unstack(level=d "city")
df6.unstack(level="city").stack(level="side")
```