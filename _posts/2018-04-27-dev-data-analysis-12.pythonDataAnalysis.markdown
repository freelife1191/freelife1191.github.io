---
layout: post
title: "[Python Data Analysis]12.pandas의 고유한 자료구조"
subtitle: "Series와 DataFrame 이해하기"
categories: dev
tags: dataAnalysis
comments: true
---

## pandas의 고유한 자료구조

### Series와 DataFrame 이해하기

pandas에서는 고유하게 정의한 자료 구조인 Series와 DataFrame을 사용하여, 빅 데이터 분석에 있어 높은 수준의 성능을 발휘합니다. Series는 동일한 데이터형의 복수 개의 성분으로 구성된 자료 구조이며, DataFrame은 서로 같거나 다른 데이터형의 여러 개의 열에 대하여 복수 개의 성분으로 구성된 '표와 같은 형태'의 자료 구조입니다.

#### Series

Series는 `pd.Series()` 함수를 사용하여 정의합니다. 이 때 Python 리스트나, 혹은 numpy array 등이 함수의 인자로 입력됩니다.


Series는 각 성분의 인덱스와, 이에 대응되는 값으로 구성되어 있습니다. Series 생성 시 인덱스를 따로 명시해주지 않으면, 0으로 시작하는 정수 형태의 기본 인덱스가 부여됩니다. 기본 인덱스 대신 Series 생성 시 각 성분에 대한 인덱스를 사용자가 직접 명시할 수도 있습니다.

```python
obj = pd.Series([4, 7, -5, 3])
obj2 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
```

어떤 Series `obj`의 인덱스만을 추출하고 싶을 경우 `obj.index`를, 값만을 추출하고 싶을 경우 `obj.values`를 사용하면 됩니다. 그리고 `obj.dtype`을 사용하면, 해당 Series에 부여된 데이터형을 확인할 수 있습니다.


Series 자체의 이름과 Series의 인덱스에 대한 이름을 지정해줄 수 있습니다. 각각 `obj.name`과 `obj.index.name`에 값을 대입해 주면 됩니다.


#### DataFrame

DataFrame은 `pd.DataFrame()` 함수를 사용하여 정의합니다. DataFrame에 입력할 데이터는 Python 딕셔너리 혹은 numpy의 2차원 array 등의 형태가 될 수 있습니다.

```python
data = {"names": ["Kilho", "Kilho", "Kilho", "Charles", "Charles"],
        "year": [2014, 2015, 2016, 2015, 2016],
        "points": [1.5, 1.7, 3.6, 2.4, 2.9]}
df = pd.DataFrame(data)
```

DataFrame에서는 서로 다른 두 종류의 인덱스가 각각 행 방향과 열 방향에 부여되어 있으며, 이들이 교차하는 지점에 실제 값이 위치해 있는 것을 확인할 수 있습니다. 이렇게 DataFrame에는 두 종류의 인덱스가 있으며, 이들을 구분하기 위해 특별히 행 방향의 인덱스를 '인덱스', 열 방향의 인덱스를 '컬럼'이라고 부릅니다. DataFrame `df`에 대하여, `df.index`와 `df.columns`를 사용하여 인덱스와 컬럼을 각각 확인할 수 있습니다. 그리고 `df.values`를 사용하면 DataFrame의 값에 해당하는 부분만 2차원 array의 형태로 얻을 수 있습니다.


DataFrame의 인덱스와 컬럼에도 Series와 유사한 방식으로 이름을 지정해줄 수 있습니다. 각각 `df.index.name`과 `df.columns.name`에 값을 대입해 주면 됩니다.


#### * DataFrame 관련 함수 혹은 변수 등을 조회하고자 할 경우

어떤 특정한 DataFrame `df`와 관련하여 실행할 수 있는 함수 혹은 변수의 정확한 이름이 제대로 기억나지 않을 경우, IPython Notebook에서 `df.`까지만 입력하고 `TAB`키를 누르면 사용 가능한 모든 변수 및 함수가 표시됩니다.


#### * NaN (not a number)

`NaN`은 numpy나 python에서 'not a number'를 표시하는 약어로, 특정 위치에 값이 존재하지 않을 때 이를 표시하기 위한 기호라고 할 수 있습니다. 여러분이 데이터셋 파일을 DataFrame의 형태로 읽어들이는 과정에서, 만약 특정 부분의 값이 포함되어 있지 않았을 경우 해당 위치에 이렇게 `NaN`으로 표시됩니다.


NaN으로 표시된 부분에 대해서는 추후에 어떠한 연산도 수행할 수 없기 때문에, 추후에 이 부분을 실제 값으로 메꿀 방법을 생각해 보아야 합니다.

#### describe 함수

DataFrame `df`에 대하여 `df.describe()` 함수를 실행하게 되면, 계산이 가능한 컬럼에 한해서 각 컬럼의 평균, 분산, 최솟/최댓값 등 기본 통계량을 산출한 결과를 보여줍니다. 이는 데이터셋을 DataFrame 형태로 막 읽어들인 직후에, 데이터셋을 전체적으로 살펴보고자 할 때 사용하기 유용합니다.