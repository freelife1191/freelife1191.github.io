---
layout: post
title: "[Python Data Analysis]18.플롯 모양 변형하기"
subtitle: "Figure, subplots 및 axes"
categories: dev
tags: data_analysis
comments: true
---

## 플롯 모양 변형하기

### Figure, subplots 및 axes

matplotlib에서는 **'figure(피겨)'**라는 그림 단위를 사용하여, 이 안에 한 개 혹은 복수 개의 플롯을 그리고 관리할 수 있도록 하는 기능을 지원합니다. 이 때, figure 안에 들어가는 플롯 공간 하나를 **'subplot(서브플롯)'**이라고 부릅니다.


새로운 figure를 직접 생성하고자 할 경우, `plt.figure()`함수를 사용합니다. `fig`라는 이름의 figure에 subplot을 하나 추가하고 싶으면, `fig.add_subplot()` 함수를 실행하여 그 반환값을 새로운 변수로 받습니다.

```python
fig = plt.figure()
ax1 = fig.add_subplot(2, 2, 1)
```

`fig.add_subplot()` 함수에는 총 3개의 인자가 들어갑니다. 앞의 두 개는 해당 figure 안에서 subplot들을 몇 개의 행, 몇 개의 열로 배치할 것인지를 나타냅니다. 맨 마지막 인자는, 이렇게 지정한 subplot들의 배치 구조 상에서, 해당 subplot을 실제로 어느 위치에 배치할지를 나타내는 번호입니다.


`fig.add_subplot()` 함수의 반환값을 `ax1`이라는 변수에서 받는데, 이는 해당 subplot에 그려진 빈 좌표 평면을 나타내는 변수입니다. matplotlib에서는 이 빈 좌표평면을 **'axes(액시스)'**라고 부릅니다. figure 안의 subplot에 axes를 생성한 순간부터, 비로소 여기에 플롯을 그릴 수 있는 상태가 됩니다.


같은 방법으로 `fig.add_subplot()` 함수를 여러 번 실행하여, 각 subplot 위치별로 새로운 axes를 생성함으로써 플롯을 그릴 준비를 갖출 수 있습니다.

```python
ax2 = fig.add_subplot(2, 2, 2)
ax3 = fig.add_subplot(2, 2, 3)
```

이렇게 생성된 각각의 subplot 내 axes들에 실제 플롯을 그려보도록 합시다. 만약 `plt.plot()` 함수를 실행하여 플롯을 그리는 경우, 현재 활성화되어 있는 figure의 맨 마지막 위치에 해당하는 subplot의 axes부터 차례대로 플롯이 그려지게 됩니다.

```python
plt.plot(np.random.randn(50).cumsum())
```

반면 `ax1.hist()`와 같이 특정 axes를 나타내는 변수 ax1을 직접 지정하여 플롯을 그리는 경우, 해당 axes에 플롯을 그립니다.

```python
ax1.hist(np.random.randn(100), bins=20)
ax2.scatter(np.arange(30), np.arange(30) + 3 * np.random.randn(30))
```

figure와 subplot을 그릴 때, `plt.subplots()` 함수를 사용하면 좀 더 직관적으로 할 수 있습니다.

```python
fig, axes = plt.subplots(2, 3)
```

예를 들어 위와 같이 실행하게 되면, `fig` figure 안에 총 6개의 subplot들을 2x3으로 배치하며, 각각의 내부에 `axes`를 생성합니다. 이 때 반환받은 `axes` 함수에는, subplot의 구조와 동일한 구조를 가지는 2x3 크기의 array가 들어가며, 각각의 성분이 곧 대응되는 위치의 `axes`가 되므로 이를 사용하여 원하는 위치에 플롯을 그릴 수 있습니다.


#### 색상, 마킹 및 라인 스타일

라인 플롯의 경우, 라인 색상과 마킹 기호 및 라인 스타일 등을 지정할 수 있습니다.


`plt.plot()` 함수를 사용해서 라인 플롯을 그릴 때, `color`, `marker`, `linestyle` 인자의 값을 함께 입력하면 각각 각각 라인 색상, 점을 마킹하는 기호, 라인 스타일을 지정할 수 있습니다.

```python
plt.plot(np.random.randn(30), color="g", marker='o', linestyle="--")
```

이들 각각에 입력할 수 있는 값은 matplotlib에서 따로 정의되어 있습니다. 예를 들어 `color="g"`면 녹색, `marker='o'`면 O 모양의 마킹 기호, `linestyle="--"`이면 점선 스타일을 적용하게 됩니다.


matplotlib에서 사용 가능한 주요 color, marker, linestyle 값을 본 강의노트 맨 하단에 정리해 놓았으니 참고하시길 바랍니다.


만약 여러분들이 코드를 길게 작성하기 귀찮은 경우, 라인 플롯의 색상, 마킹 및 라인 스타일을 나타내는 값들을 하나의 문자열로 붙여서 입력할 수도 있습니다.

```python
plt.plot(np.random.randn(30), "k.-")
```

한편 바 플롯이나 히스토그램, 산점도 등에는 색상과 알파값 등을 지정할 수 있습니다. 다음 코드를 실행하여 결과를 관찰해 봅시다.

```python
fig, axes = plt.subplots(2, 1)
data = pd.Series(np.random.rand(16), index=list('abcdefghijklmnop'))
data.plot(kind="bar", ax=axes[0], color='k', alpha=0.7)
data.plot(kind="barh", ax=axes[1], color='g', alpha=0.3)
```

#### 눈금, 레이블 및 범례 등

여러분이 그린 플롯의 눈금, 레이블, 범례 등을 수정할 수 있습니다. 우선 figure를 하나 만든 뒤, subplot axes를 하나 추가하고 여기에 랜덤한 값들의 누적합을 나타내는 라인 플롯을 하나 그립니다.

```python
fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)
ax.plot(np.random.randn(1000).cumsum())
```

플롯의 수평축 혹은 수직축에 나타난 눈금을 matplotlib에서는 **'틱(tick)'**이라고 부릅니다. 특별히 수평축의 눈금은 'xtick', 수직축의 눈금은 'ytick'이라고 부릅니다. 수평축의 눈금을 다른 것으로 변경하고자 할 경우, `ax.set_xticks()` 함수를 사용합니다.

```python
ticks = ax.set_xticks([0, 250, 500, 750, 1000])
```

`ax.set_xticklabels()` 함수를 사용하여, 수평축의 눈금을 숫자가 아닌 문자열 레이블로 대체할 수도 있습니다.

```python
labels = ax.set_xticklabels(["one", "two", "three", "four", "five"],
         rotation=30, fontsize="small")
```

만약 수직축의 눈금을 변경하고자 한다면, 수평축의 경우와 완전히 동일한 방식으로 `ax.set_yticks()` 등의 함수를 사용하면 됩니다.


axes의 제목을 입력하고자 할 경우, `ax.set_title()` 함수를 사용하면 됩니다. 만약 수평축과 수직축에 이름을 붙이고 싶다면, 각각 `ax.set_xlabel()`, `ax.set_ylabel()` 함수를 사용하면 됩니다.

```python
ax.set_title("Random walk plot")
ax.set_xlabel("Stages")
ax.set_ylabel("Values")
```

만약 하나의 axes에 표시한 플롯의 개수가 많다면, 범례(legend)를 표시해야 할 필요가 있습니다. 먼저 새로운 figure 안에 subplot axes를 하나 생성합니다.

```python
fig = plt.figure()
ax = fig.add_subplot(1, 1, 1)
```

다음으로, 랜덤 워크 플롯을 `ax` axes에 3개 추가합니다. 이 때, `ax.plot()` 함수를 사용할 시 `label` 인자의 값을 함께 입력해 줍니다. 입력한 `label` 인자의 값이, 나중에 axes에 범례를 표시할 때 각각의 이름으로 제시됩니다.

```python
ax.plot(np.random.randn(1000).cumsum(), 'k', label="one")
ax.plot(np.random.randn(1000).cumsum(), "b--", label="two")
ax.plot(np.random.randn(1000).cumsum(), "r.", label="three")
```

`ax.legend()` 함수를 실행하면, axes 상에 범례가 표시됩니다. 이 때 `loc="best"` 인자를 넣어주면, 현재 제시된 axes 상에서 최적의 위치에 범례를 자동으로 배치합니다.

```python
ax.legend(loc="best")
```

현재 axes에 표시된 수평축 값의 범위와 수직축 값의 범위를 변경하고자 한다면, `ax.set_xlim()` 함수와 `ax.set_ylim()` 함수를 사용하면 됩니다.

```python
ax.set_xlim([100, 900])
ax.set_ylim([-100, 100])
```

#### 부록: matplotlib에서 사용 가능한 주요 color, marker, linestyle 값

##### matplotlib에서 사용 가능한 주요 color 값
| 값   | 색상    |
| ---- | ------- |
| "b"  | blue    |
| "g"  | green   |
| "r"  | red     |
| "c"  | cyan    |
| "m"  | magenta |
| "y"  | yellow  |
| "k"  | black   |
| "w"  | white   |

##### matplotlib에서 사용 가능한 주요 marker 값
| 값   | 마킹           |
| ---- | -------------- |
| "."  | point          |
| ","  | pixel          |
| "o"  | circle         |
| "v"  | triangle_down  |
| "^"  | triangle_up    |
| "<"  | triangle_left  |
| ">"  | triangle_right |
| "8"  | octagon        |
| "s"  | square         |
| "p"  | pentagon       |
| "*"  | star           |
| "h"  | hexagon        |
| "+"  | plus           |
| "x"  | x              |
| "D"  | diamond        |

##### matplotlib에서 사용 가능한 주요 linestyle 값
| 값     | 라인 스타일      |
| ------ | ---------------- |
| "-"    | solid line       |
| "--"   | dashed line      |
| "-."   | dash-dotted line |
| ":"    | dotted line      |
| "None" | draw nothing     |