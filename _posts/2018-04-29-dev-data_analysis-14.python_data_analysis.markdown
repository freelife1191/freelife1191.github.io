---
layout: post
title: "[Python Data Analysis]14.DataFrame 이리저리 조작하기"
subtitle: "DataFrame 이리저리 조작하기"
categories: dev
tags: data_analysis
---

## DataFrame 이리저리 조작하기

결측값 또는 이상치 처리하기

여러분이 pandas를 사용하여 읽어들인 데이터셋 파일에 `NaN`의 형태로 빠진 값이 존재하거나, 혹은 정상 범주에서 벗어난 값이 포함되어 있는 경우가 얼마든지 발생할 수 있습니다. 이러한 값들을 각각 **결측값(missing value)** 및 **이상치(outlier)**라고 하는데, 본격적인 데이터 분석에 앞서 이들을 적절히 처리할 필요가 있습니다.

```python
df = pd.DataFrame(np.random.randn(6, 4))
df.columns = ["A", "B", "C", "D"]
df.index = pd.date_range("20160701", periods=6)
```

랜덤한 숫자들로 구성된 DataFrame `df`를 정의하고, 인덱스와 컬럼을 명시하였습니다. 이 때, pandas에서 제공하는 `pd.date_range()` 함수를 사용하였는데, 이는 일자와 시각을 나타내는 데이터형인 datetime으로 구성된 인덱스를 생성할 때 사용하는 함수입니다. 여러분들이 많이 접할 데이터셋 중 하나가 바로 **시계열(time series)** 형태의 데이터셋인데, pandas는 이렇게 **datetime**과 관련된 간편한 기능을 많이 제공하고 있습니다.


`df`의 'F' 열을 새로 정의하고, 여기에 다음과 같이 값을 대입합니다.

```python
df["F"] = [1.0, np.nan, 3.5, 6.1, np.nan, 7.0]
```

`NaN`을 인위적으로 사용하고자 할 때, numpy에서 제공하는 `np.nan`을 사용합니다.


`df.dropna(how="any")`를 실행하면, 각각의 행을 살펴보면서 행 내 값들 중에 `NaN`이 하나라도 포함되어 있는 경우 해당 행을 DataFrame 상에서 삭제합니다. 반면 `df.dropna(how="all")`을 실행할 경우, 행 내 값들 모두가 `NaN`인 경우 해당 행을 DataFrame 상에서 삭제합니다.


아니면 `df`의 `NaN`을 실제 수치값으로 대체하고 싶을 수 있습니다. 이러한 경우 `df.fillna(value=5.0)`와 같이 실행하면, `NaN`을 지정한 값으로 대체한 결과물을 얻을 수 있습니다.


한편, `df.isnull()` 함수를 실행하면 DataFrame 상에서 `NaN`이 포함되어 있는 위치에 대한 불리언 마스크를 얻을 수 있습니다. 이를 응용하여 `df.loc[df.isnull()["F"], :]`를 실행하면, 'F'열에 `NaN`을 포함하고 있는 행만을 선택할 수 있습니다.


다음으로 각 행의 값을 관찰하여, 이상치가 포함되어 있는 행을 DataFrame 상에서 직접 삭제하는 방법을 알아보도록 하겠습니다. 예를 들어 2016년 7월 1일 행 데이터를 선택하고자 할 때, `pd.to_datetime("20160701")`을 실행하면 "20160701"이라는 문자열을 **datetime** 데이터형으로 변환하며, 이를 인덱스로 사용할 수 있습니다.


`df.drop(pd.to_datetime("20160701"))`을 실행한 결과를 보면, 2016년 7월 1일 행 데이터가 DataFrame 상에서 삭제된 것을 확인할 수 있습니다. 이렇게 인덱스를 기준으로 특정 행을 삭제하고자 할 경우 `.drop()` 함수를 사용하면 됩니다. 두 개 이상의 인덱스를 기준으로 복수 개의 행을 삭제하고자 할 경우, `df.drop([pd.to_datetime("20160702")`, `pd.to_datetime("20160704")])`와 같이 `.drop()` 함수의 매개변수로 **datetime** 리스트를 입력하면 됩니다.


`.drop()` 함수를 사용하면, 행 뿐만 아니라 열도 삭제할 수 있습니다. `df.drop("F", axis=1)`와 같이 삭제할 컬럼을 명시한 후 `axis=1` 매개변수를 명시해 주면, 'F' 열이 삭제된 것을 확인할 수 있습니다. 이 경우에도 `df.drop(["B", "F"], axis=1)`의 형태로 복수 개의 열을 명시할 수도 있습니다.