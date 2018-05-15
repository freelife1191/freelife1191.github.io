---
layout: post
title: "[Python Data Analysis]13.DataFrame 인덱싱 이해하기"
subtitle: "DataFrame 인덱싱 이해하기"
categories: dev
tags: data-analysis
comments: true
---

## DataFrame 인덱싱 이해하기

#### 기본 인덱싱

`df`라는 이름의 DataFrame을 다음과 같이 정의합니다.

```python
data = {"names": ["Kilho", "Kilho", "Kilho", "Charles", "Charles"],
           "year": [2014, 2015, 2016, 2015, 2016],
           "points": [1.5, 1.7, 3.6, 2.4, 2.9]}
df = pd.DataFrame(data, columns=["year", "names", "points", "penalty"],
                          index=["one", "two", "three", "four", "five"])
```

#### 열 선택하고 조작하기

`df`에서 'year' 열만을 얻고 싶을 경우, `df["year"]`를 실행합니다. 그러면 'year' 열의 값들이 Series의 형태로 인덱스와 함께 표시됩니다. 하나의 열을 가져오는 경우 `df.year`와 같이 해도 동일한 결과를 얻습니다. 두 가지 방법 중에서 여러분이 편한 것을 사용하시면 됩니다.


만약 복수 개의 열을 가져오고자 할 경우에는, `df[["year", "points"]]`와 같은 형태로 실행하시면 됩니다. 이 때, 중괄호 안에 컬럼 이름으로 구성된 리스트가 들어간다는 점을 주의하시길 바랍니다.


특정 열을 이렇게 선택한 뒤, 값을 일괄적으로 대입해줄 수도 있습니다. `df["penalty"] = 0.5` 또는 `df["penalty"] = [0.1, 0.2, 0.3, 0.4, 0.5]`를 실행하면, 기존에 `NaN`으로 표시되었던 'penalty' 열에 지정한 값을 대입하게 됩니다. 새로운 'zeros'라는 이름의 열을 추가하고자 할 경우, `df["zeros"] = np.arange(5)`와 같이 실행하시면 됩니다.


pandas의 Series를 DataFrame의 새로운 열의 값으로 대입할 수도 있는데, 이 경우 해당 Series에서 명시된 인덱스와 DataFrame 상의 인덱스를 비교하여 대응되는 인덱스의 값을 대입하는 형태로 이루어집니다. 이것이 열의 값을 Python 리스트나 numpy array로 입력하는 경우와, pandas Series로 입력하는 경우의 핵심적인 차이입니다.

```python
val = pd.Series([-1.2, -1.5, -1.7], index=["two", "four", "five"])
df["debt"] = val
```

새로운 열의 값을 기존 열의 값을 사용하여 입력할 수도 있습니다. 예를 들어 'net_points'라는 열의 값이 'points'에서 'penalty'를 뺀 것이라고 합시다. 그리고 'high_points' 열은 'net_points'의 값이 2.0보다 클 때 True, 그렇지 않을 때 False를 가지도록 합시다. 다음과 같이 실행하면 됩니다.

```python
    df["net_points"] = df["points"] - df["penalty"]
    df["high_points"] = df["net_points"] > 2.0
```

기존의 열을 DataFrame 상에서 삭제해 버리는 것은 아주 간단합니다. del 키워드와 함께 삭제할 열을 명시하면 됩니다.

```python
del high_points
del net_points
del zeros
```

#### 행 선택하고 조작하기

pandas DataFrame의 행을 인덱싱할 수 있는 방법은 무수하게 많습니다. 그리고 열을 인덱싱하는 방법에 있어서도 바로 위에서 소개했던 방법은 여러 가지 중 하나에 불과합니다. 더욱 머리를 아프게 하는 것은, pandas의 버전이 올라가면서 이러한 인덱싱 방법도 미묘하게 달라지고 있다는 것입니다.


다른 기능들과의 혼동을 방지하기 위해, DataFrame의 행을 선택하고자 할 때, 저는 `.loc`이나 `.iloc`을 사용하시길 권장드리고자 합니다.


##### df.loc

`.loc`은, 실제 인덱스를 사용하여 행을 가져올 때 사용합니다. 예를 들어 `df.loc["two"]`를 실행하면, 인덱스가 'two'인 행의 값을 모두 가져옵니다. `df.loc["two":"four"]`을 실행하면, 인덱스가 'two'부터 'four'까지의 범위에 있는 행의 모든 값을 가져옵니다.


`.loc`을 사용하면, 인덱스 뿐만 아니라 컬럼 역시 동시에 명시할 수 있습니다. 예를 들어 'two'부터 'four'까지 인덱스의 값들 중 'points' 열의 값만을 가져오고자 할 경우, `df.loc["two":"four", "points"]`를 실행하면 됩니다. 이 경우에도 하나의 열을 가져왔으므로 결과물은 Series가 됩니다. `df.loc["three":"five", "year":"penalty"]`와 같이 실행하면, 인덱스와 컬럼 모두 범위 인덱싱이 가능합니다.


새로운 행을 추가하고자 할 경우, `df.loc["six", :] = [2013, "Hayoung", 4.0, 0.1, 2.1]`과 같이 `.loc`을 사용하여 새로운 인덱스의 행을 선택하고, 여기에 대입할 값을 리스트 혹은 array의 형태로 입력해주면 됩니다.


##### df.iloc

`.iloc`은, numpy의 array 인덱싱 방식으로 행을 가져올 때 사용합니다. 예를 들어 `df.iloc[3]`을 실행하면, 인덱스 3에 해당하는 4행을 모두 가져옵니다. `df.iloc[3:5, 0:2]`와 같이 행과 열에 대한 범위 인덱싱이 가능하며, `df.iloc[[0, 1, 3], [1, 2]]`와 같이 원하는 인덱스만을 명시하여 가져올 수도 있습니다.


DataFrame의 행을 선택하는 방법은 위에서 소개해 드린 방법 외에도 몇 가지가 더 있습니다. 그럼에도 불구하고, 여러분들께 `.loc`과 `.iloc`만을 사용하여 행을 선택하고 조작하시길 권장드립니다. 그래야 나중에 혼란이 적을 것입니다.


#### 불리언 인덱싱

pandas의 DataFrame에서도 열이나 행을 선택할 때, 불리언 인덱싱이 가능합니다.


`df`에서, 'year' 열의 값이 2014보다 큰 행만을 선택하고 싶다고 가정합시다. `df["year"] > 2014`를 실행하면, 값이 2014보다 큰 위치에는 `True`, 그 외에는 `False`가 들어가 있는 불리언 Series를 얻게 됩니다. 이를 마스크라고 부릅니다.


이런 마스크는 DataFrame을 인덱싱하는 데 사용될 수 있습니다. `df.loc[df["year"] > 2014, :]`를 실행하면, 앞서 확인했던 마스크가 True에 해당하는 행만으로 구성된 DataFrame을 얻을 수 있습니다. `df.loc[df["names"] == "Kilho", ["names", "points"]]`를 실행하면, 'names' 열의 값이 "Kilho"인 행의 값 중에서 'names'와 'points' 열에 해당하는 값들만을 얻을 수 있습니다.


만약 사용할 조건, 즉 마스크가 여러 개 필요하다면, `df.loc[(df["points"] > 2) & (df["points"] < 3), :]`와 같이 실행하면 됩니다. 조건과 조건 간에 `&`가 들어가 있는 것을 주목하시길 바랍니다. `&`(and) 연산자를 사용하는 경우 두 개의 마스크가 동시에 `True`인 경우에만 해당 인덱스를 조회하며, `|`(or) 연산자를 사용하는 경우 두 개의 마스크 중 최소 하나가 `True`인 경우에 해당 인덱스를 조회합니다.