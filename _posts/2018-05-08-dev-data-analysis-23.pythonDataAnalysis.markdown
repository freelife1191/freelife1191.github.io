---
layout: post
title: "[Python Data Analysis]23.DataFrame 데이터 변형하기"
subtitle: "DataFrame 데이터 변형하기"
categories: dev
tags: dataAnalysis
comments: true
---

## DataFrame 데이터 변형하기

### 기존 데이터를 변형하는 자잘한 기능들

#### 중복된 값 제거하기

```python
df = pd.d DataFrame({'k1': ['one'] * 3 + ['two'] * 4, 
     'k2': [1, 1, 2, 3, 3, 4, 4]})
```

`df`를 살펴보면 몇 군데 중복된 행이 포함되어 있습니다. `df.duplicated()` 함수를 실행하면, 중복된 행이 등장하는 부분이 **True**로, 그 외의 부분이 **False**로 구성된 Series 형태의 불리언 마스크를 얻을 수 있습니다.

이렇게 얻은 불리언 마스크를 가지고 중복된 행들을 직접 처리해도 되고, 혹은 `df.drop_duplicates()` 함수를 사용하면 중복된 값이 제거된 새로운 DataFrame을 얻을 수 있습니다.

현재 `df`에 새로운 열을 하나 추가해 봅시다.

```python
df[d "v1"] = np.arange(7)
```

중복된 값이 없는 "v1" 열이 추가되었습니다. 이 상태에서 특정 열의 값을 기준으로 하여 해당 열에서 중복된 값을 가지는 행들을 제거할 수도 있습니다.

```python
df.drop_duplicates([d "k1"])
df.drop_duplicates(["k1", "k2"], keep="last")
```

`df.drop_duplicates()` 함수에 `keep` 인자를 추가하였는데, 이는 중복된 행들 중 한 행만을 남기고 나머지를 제거하는 과정에서 맨 마지막에 등장한 것을 남길지, 맨 처음에 등장한 것을 남길지 결정하는 부분입니다. "last" 값을 대입할 경우 맨 마지막, "first" 값을 대입할 경우 맨 처음 행을 남깁니다.

#### 데이터 매핑하기

DataFrame의 어떤 열이 유한 가지의 값들 중 하나를 가진다고 가정합시다. 데이터셋의 단순화를 위해 이들을 더 적은 가짓수의 값들 중 하나로 **매핑(mapping)**하고 싶을 수 있습니다.

```python
df2 = pd.d DataFrame({'food': ['bacon', 'pulled pork', 'bacon', 'Pastrami', 
      'corned beef', 'Bacon', 'pastrami', 'honey ham', 'nova lox'],
      'ounces': [4, 3, 12, 6, 7.5, 8, 3, 5, 6]})
```

생성된 `df2`의 "food" 열에 몇 가지 값이 들어가 있는데, 이 "food" 열의 값들을 새로운 값으로 매핑하는 딕셔너리를 하나 정의합니다.

```python
meat_to_animal = { 
    m 'bacon': 'pig', 
    'pulled pork': 'pig', 
    'pastrami': 'cow', 
    'corned beef': 'cow', 
    'honey ham': 'pig', 
    'nova lox': 'salmon'
}
```

이 `meat_to_animal` 딕셔너리에 명시된 규칙에 의거하여, "food" 열의 값들을 "pig", "cow", "salmon" 중 하나로 치환한 뒤 이들을 갖는 새로운 "animal" 열을 다음과 같이 추가할 수 있습니다.

```python
df2[d "animal"] = df2["food"].apply(lambda x: meat_to_animal[x.lower()])
```

`df.apply()` 함수를 사용하여, 기존 "food" 열에 포함된 각 문자열 값에 `str.lower()` 함수를 먼저 적용하여 모두 소문자로 변환한 뒤 이를 키로 갖는 `meat_to_animal`에서의 값을 반환하도록 하였습니다.

#### 값 치환하기

**pandas**에서 Series에 대해 제공하는 `s.replace()` 함수를 사용하면, Series 상의 특정 값을 다른 값으로 치환하는 작업을 보다 유연하게 할 수 있습니다.

```python
ss = pd.Series([1., -999., 2., -999., -1000., 3.])
```

`s.replace()` 함수를 적용하여, 특정 값을 가지는 성분들을 모두 NaN으로 치환할 수 있습니다. 혹은 반대로, NaN을 모두 0으로 치환할 수 있습니다.

```python
s2 = s.s replace(-999, np.nan)
s2.replace(np.nan, 0)
```

#### Categories(카테고리) 자료형

지금까지 여러분은 어떤 데이터셋에서 유한 가지 값들 중 하나를 가지는 열이 존재하는 경우를 많이 보았을 것입니다. 예를 들어 고객의 성별을 나타내는 열에서 '남성'이면 "male", '여성'이면 "female" 값을 가지는 것이 대표적인 경우입니다. 이러한 유형의 데이터를 **'카테고리(category, 범주형)'** 데이터라고 합니다.


이런 카테고리 데이터를 관리하기 위해, **pandas**에서는 **'Categories'**라는 특별한 자료형을 제공합니다. 이는 DataFrame 상의 특정 열과 같이, Series에 대하여 부여될 수 있는 자료형입니다. Categories 자료형을 활용하면, 단순히 문자열 자료형으로 저장되어 있던 데이터를 대체함으로써 메모리 사용량을 획기적으로 줄일 수 있으며, 이에 대한 각종 통계 분석도 보다 간편하게 할 수 있습니다.

#### Categories 열 생성하기

```python
df3d  = pd.DataFrame({"id":[1,2,3,4,5,6], "raw_grade":['a', 'b', 'b', 'a', 'a', 'e']})
```

`df3`의 "raw_grade" 열에는 'a', 'b', 'e' 등의 카테고리 값이 단순 문자열 형태로 저장되어 있습니다. 이를 Categories 자료형으로 치환한 새로운 "grade" 열을 다음과 같이 정의합니다.

```python
df3[d "grade"] = df3["raw_grade"].astype("category")
```

`df3["grade"]`를 확인해보면 'Categories (3, object): [a, b, e]'라고 표시되는 것을 확인할 수 있는데, 이는 해당 열이 Categories 자료형의 Series라는 것이며, 이것이 'a', 'b', 'e'의 3가지 카테고리 값을 가질 수 있다는 것을 나타냅니다.

`df3["grade"].cat.categories`를 확인하면 현재 "grade" 열이 가질 수 있는 카테고리 값을 확인할 수 있으며, 여기에 새로운 카테고리를 포함하는 리스트를 입력할 수도 있습니다.

```python
df3[d "grade"].cat.categories
df3["grade"].cat.categories = ["very good", "good", "very bad"]
```

한편 기존 카테고리 값의 종류를 늘이거나 줄이는 것도 가능합니다. `df3["grade"].cat.set_categories()` 함수를 사용하여, 기존 카테고리 값에서 추가되거나 삭제된 것들을 리스트 형태의 인자로 명시하면 됩니다.

```python
df3[d "grade"] = df3["grade"].cat.set_categories(["very bad", "bad", "medium", "good", "very good"])
```

Categories 자료형의 또 다른 특징은, 처음 정의할 때 부여한 순서에 따라 대소 관계를 가진다는 것입니다. 다음과 같이 "grade" 열의 값을 기준으로 DataFrame을 정렬해보도록 하겠습니다.

```python
df3.sort_values(d by="grade")
```

오름차순 정렬된 결과를 보면 "very bad" (-> "bad" -> "medium") -> "good" -> "very good"의 순서로 정렬되었음을 확인할 수 있습니다. 예를 들어 '사원' -> '대리' -> '과장' -> '부장' 등과 같이 어떤 카테고리 값들 간에 순서 혹은 대소 관계가 존재한다면, Categories 자료형을 아주 효과적으로 적용할 수 있을 것입니다.

#### 숫자 데이터의 카테고리화

고객 데이터셋을 관리할 때 '연령'을 나타내는 열이 숫자 데이터로 구성되어 있었다고 합시다. 이를 '청소년' -> '청년' -> '장년' -> '중년' 등과 같이 일정한 나이 기준으로 구간을 잘라서 카테고리 데이터로 변환하여 관리하면 좀 더 편리해지는 경우가 제법 있습니다. pandas에서는 숫자 데이터를 빠르고 간편하게 카테고리화하는 기능을 제공합니다.

```python
agesa  = [20, 22, 25, 27, 21, 23, 37, 31, 61, 45, 41, 32]
bins = [18, 25, 35, 60, 100]
```

`ages` 리스트에 카테고리화 하고자 하는 숫자 데이터를, `bins` 리스트에 각 구간을 구분하는 숫자값을 명시하였습니다. 즉, 이렇게 하면 18세 초과 25세 이하, 25세 초과 35세 이하 등과 같이 총 4개의 구간을 정의합니다. `pd.cut()` 함수를 사용, `ages`와 `bins`를 인자로 입력함으로써 `ages` 리스트의 각 성분들을 카테고리화 할 수 있습니다.

```python
catsc  = pd.cut(ages, bins)
```

`cats`를 확인해보면 기존의 `ages` 리스트의 각 성분이 4가지 카테고리 값 중 하나로 대체된 결과물을 확인할 수 있습니다. `cats.categories`를 확인하면, 이 과정에서 사용된 카테고리 값들만을 직접 확인할수도 있습니다. 또 `cats.codes`를 확인하면, 기존 `ages` 리스트의 각 성분에 (0부터 시작하는 인덱스 형태로) 몇 번째 카테고리 값이 부여되었는지를 확인할 수 있습니다.

만약 "(18, 25]"와 같은 이름이 별로 보기 좋지 않다면, `pd.cut()` 함수를 실행할 때 `labels` 인자의 값을 입력함으로써 각 카테고리의 이름을 직접 명시할 수도 있습니다.

```python
group_namesg  = ["Youth", "YoungAdult", "MiddleAged", "Senior"]
pd.cut(ages, bins, labels=group_names)
```

만약 구간을 구분하는 기준값을 명시하는 것이 귀찮다면, `pd.cut()` 함수를 호출할 때 몇 개의 구간으로 나눌 것인지만 명시해주면 **pandas**에서 알아서 판단하여 길이가 일정한 구간을 정의하고 각 성분을 카테고리화합니다. 이 때 `precision` 인자는 구간을 구분하는 기준값을 결정할 때 소수 몇 번째 자리까지 고려할지 결정합니다.

```python
datad  = np.random.rand(20)
pd.cut(data, 4, precision=2)
```

한편 `pd.qcut()`이라는 함수도 있는데, 이는 지정한 갯수만큼의 구간을 정의하되, 분위수를 구분값으로 합니다.

```python
data2d  = np.random.randn(1000)
cats = pd.qcut(data2, 4)
```

예를 들어 위와 같이 4를 인자로 입력한 경우, 전체 1000개의 성분 중에서 사분위수를 추출한 뒤, 이를 4개 구간을 구분하는 기준값으로 사용한다고 이해하시면 됩니다.