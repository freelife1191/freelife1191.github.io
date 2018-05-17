---
layout: post
title: "[Python Data Analysis]11.numpy를 사용한 데이터 분석 맛보기"
subtitle: "MovieLens 1M 데이터셋 분석"
categories: dev
tags: data_analysis
comments: true
---

## numpy를 사용한 데이터 분석 맛보기

### MovieLens 1M 데이터셋 분석

#### 파일 읽기

[MovieLens 1M 데이터셋 다운로드]


대부분의 데이터셋은 열과 열을 구분하기 위한 구분자로 특정한 문자를 사용합니다. 예를 들어 MovieLens 1M dataset의 경우, 콜론이 두 개 붙은 문자 `::`가 구분자라고 할 수 있습니다.


구분자는 보통 콤마 ','를 많이 쓰는데, 콤마를 구분자로 사용한 파일을 특별히 **'CSV(comma-separated values) 파일'**이라고 부릅니다.


일정한 구분자를 사용하는 데이터셋 파일은 `np.loadtxt()` 함수를 사용하여 손쉽게 읽어들일 수 있습니다. 해당 함수를 호출할 때, 읽어들일 데이터셋 파일의 경로, 사용할 구분자, array의 데이터형 등이 인자로 입력됩니다.

```python
    data = np.loadtxt("data/movielens-1m/ratings.dat", delimiter="::", dtype=np.int64)
```

#### MovieLens 1M dataset 분석하기

동영상 강의의 내용을 참조해 주시길 바랍니다.


#### 파일 쓰기

여러분이 얻은 array 형태의 데이터 분석 결과물을 외부 파일로 쓰는 작업을 진행해보도록 합시다.


`np.savetxt()`함수를 사용하면, 현재 array 형태로 들고 있는 분석 결과물을 외부 파일로 손쉽게 쓸 수 있습니다. 해당 함수를 호출할 때, 저장할 파일의 경로, 저장할 array, 저장 형태(format), 구분자 등을 인자로 같이 입력합니다.

```python
    np.savetxt("mean_rating_by_user.csv", mean_rating_by_user_array,
               fmt='%.3f', delimiter=',')
```
