---
layout: post
title: "[Python Data Analysis]17.matplotlib의 플롯팅 함수 사용하기"
subtitle: "matplotlib의 플롯팅 함수 사용하기"
categories: dev
tags: data_analysis
comments: true
---

## matplotlib의 플롯팅 함수 사용하기

matplotlib은 numpy나 pandas를 사용하여 데이터를 분석한 결과를 시각화하는 데 사용되는 대표적인 Python 데이터 시각화 라이브러리입니다. matplotlib에서는 DataFrame 혹은 Series 형태의 데이터를 가지고 다양한 형태의 플롯을 만들어 주는 기능을 지원합니다.


IPython Notebook에서 플롯을 그리기에 앞서, `%matplotlib`라는 매직 명령어를 사용해서 플롯팅 옵션을 먼저 지정해야 합니다. `%matplotlib nbagg`를 실행하는 경우, 노트북 상에서 생성되는 플롯을 인터랙티브하게 조작할 수 있습니다. 한편 `%matplotlib inline`을 실행하면, 노트북 상의 특정 셀에서 플롯을 일단 생성하면 이를 조작할 수 없습니다.


본 강의에서는 `%matplotlib nbagg`을 실행하여 적용합니다.

```python
%matplotlib nbagg
```

#### 라인 플롯(line plot)

라인 플롯은 연속적인 직선으로 구성된 플롯입니다. 어떤 특정한 독립변수 X가 변화함에 따라 종속변수 Y가 어떻게 변화하는지를 나타내고자 할 때 라인 플롯을 사용합니다.


랜덤한 값들로 구성된 Series `s`를 인덱스와 함께 생성한 뒤 `s.plot()`을 실행하면, `s`의 인덱스와 값을 사용하여 라인 플롯을 그려줍니다. 만약 여러분이 import한 matplotlib.pyplot 모듈 `plt`를 사용하여 `plt.plot(s)`를 실행하더라도 동일한 결과를 얻을 수 있습니다.

```python
s = pd.Series(np.random.randn(10).cumsum(), index=np.arange(0, 100, 10))
s.plot()
```

생성된 플롯에 대하여, 화면에 표시된 부분을 이동시키거나 특정 부분을 확대하며, 현재 보여진 플롯을 이미지 파일 형태로 내보내는 등의 인터랙티브한 조작을 가할 수 있습니다. 플롯 우측 상단의 파란색 버튼을 클릭하게 되면, 해당 플롯을 더 이상 수정할 수 없는 상태가 됩니다.


랜덤한 값들로 구성된 DataFrame `df`을 인덱스, 컬럼과 함께 생성한 뒤 `df.plot()`을 실행하면, `df`의 인덱스와 각 컬럼 값을 사용하여 여러 개의 라인 플롯을 그려줍니다. `df`에 포함되어 있는 열의 갯수만큼 라인 플롯이 화면에 그려진 것을 확인할 수 있습니다. 만약 여러분이 import한 matplotlib.pyplot 모듈 `plt`를 사용하여 `plt.plot(df)`를 실행하더라도 동일한 결과를 얻을 수 있습니다.

```python
df = pd.DataFrame(np.random.randn(10, 4).cumsum(axis=0),
     columns=["A", "B", "C", "D"],
     index=np.arange(0, 100, 10))
df.plot()
```

만약 특정한 하나의 열에 대해서만 라인 플롯을 그리고 싶다면, 다음과 같이 해당 열을 Series 형태로 추출한 뒤 라인 플롯을 그리면 됩니다.

```python
df["B"].plot()
```

#### 바 플롯(bar plot)

바 플롯은 막대 형태의 플롯입니다. 독립변수 X가 변화하면서 종속변수 Y가 변화하는 양상을 나타낼 때, X가 연속적인 숫자에 해당하는 경우 라인 플롯을 그렸다면, X가 유한 개의 값만을 가질 경우 바 플롯을 사용하면 유용합니다.


랜덤한 값들로 구성된 Series `s2`를 인덱스와 함께 생성한 뒤 `s2.plot(kind="bar")`를 실행하면, `s2`의 인덱스와 값을 사용하여 수직 방향의 바 플롯을 그려줍니다.

```python
s2 = pd.Series(np.random.rand(16), index=list("abcdefghijklmnop"))
s2.plot(kind="bar")
```

만약 바 플롯을 수평 방향으로 그리고자 할 경우, `s2.plot(kind="barh")`를 실행하면 됩니다.

```python
s2.plot(kind="barh")
```

랜덤한 값들로 구성된 DataFrame `df2`를 인덱스, 컬럼과 함께 생성한 뒤 `df2.plot(kind="bar")`를 실행하면, `df2`의 인덱스와 각 컬럼 값을 사용하여 여러 개의 바 플롯을 그려줍니다. 이 때, 하나의 인덱스에 대하여 이에 대응되는 복수 개의 열 값이 여러 개의 바 플롯으로 나타난 것을 확인할 수 있습니다.

```python
df2 = pd.DataFrame(np.random.rand(6, 4), 
      index=["one", "two", "three", "four", "five", "six"],
      columns=pd.Index(["A", "B", "C", "D"], name="Genus"))
df2.plot(kind="bar")
```

바 플롯을 그릴 때 `stacked=True` 인자를 넣어주면, 하나의 인덱스에 대한 각 열의 값을 한 줄로 쌓아 표시해줍니다. 이는 하나의 인덱스에 대응되는 각 열 값의 상대적 비율을 확인할 때 유용합니다.

```python
df2.plot(kind="barh", stacked=True)
```

#### 히스토그램(histogram)

히스토그램의 경우 어느 하나의 변수 X가 가질 수 있는 값의 구간을 여러 개 설정한 뒤, 각각의 구간에 속하는 갯수를 막대 형태로 나타낸 플롯입니다. Series로부터 히스토그램을 그릴 때는 인덱스를 따로 명시할 필요가 없으며, 그저 값들만 가지고 있으면 됩니다.


랜덤한 값들로 구성된 Series `s3`를 생성한 뒤 `s3.hist()`를 실행하면, s3의 값을 사용하여 히스토그램을 그려줍니다.

```python
s3 = pd.Series(np.random.normal(0, 1, size=200))
s3.hist()
```

각 구간에 속하는 값의 갯수를 카운팅할 때, 구간의 개수는 자동으로 10개로 설정되어 있습니다. 이 구간을 **'bin(빈)'**이라고 부릅니다. 여러분이 히스토그램을 그릴 때, 다음과 같이 bin의 갯수를 직접 설정할 수도 있습니다.

```python
s3.hist(bins=50)
```

만약 `normed=True` 인자를 넣어주면, 각 bin에 속하는 갯수를 전체 갯수로 나눈 비율, 즉 정규화한(normalized) 값을 사용하여 히스토그램을 그립니다.

```python
s3.hist(bins=100, normed=True)
```

#### 산점도(scatter plot)

라인 플롯이나 바 플롯의 경우 어떤 독립변수 X가 변화함에 따라 종속변수 Y가 어떻게 변화하는지 나타내는 것이 목적이었다면, 산점도의 경우 이 보다는 서로 다른 두 개의 독립변수 X1, X2 간에 어떠한 관계가 있는지 알아보고자 할 때 일반적으로 많이 사용합니다. 즉 산점도는, 두 독립변수 X1과 X2의 값을 각각의 축으로 하여 2차원 평면 상에 점으로 나타낸 플롯입니다.


랜덤한 값들로 구성된 두 개의 array를 생성한 뒤, `np.concatenate()` 함수를 사용하여 이들을 열 방향으로 연결합니다.

```python
x1 = np.random.normal(1, 1, size=(100, 1))
x2 = np.random.normal(-2, 4, size=(100, 1))
X = np.concatenate((x1, x2), axis=1)
```

이렇게 생성된 X array를 사옹하여 새로운 DataFrame `df3`를 생성하면, `df3`에는 'x1'과 'x2'의 두 개의 열이 포함되어 있습니다. `plt.scatter(df3["x1"], df3["x2"])`를 실행하면, 두 열 간의 값을 기준으로 산점도를 그립니다.

```python
df3 = pd.DataFrame(X, columns=["x1", "x2"])
plt.scatter(df3["x1"], df3["x2"])
```

얻어진 산점도의 수평축에는 'x1'의 값, 수직축에는 'x2'의 값을 사용하여 해당하는 위치에 점을 찍어서 데이터를 표현합니다.