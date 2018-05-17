---
layout: post
title: "[Python Data Analysis]5.Python 데이터 분석 라이브러리 설치하기"
subtitle: "Python 데이터 분석 라이브러리 설치하기"
categories: dev
tags: data_analysis
comments: true
---

## Python 데이터 분석 라이브러리 설치하기

- numpy 설치:
```dos
pip install numpy
```

- pandas 설치:
```dos
pip install pandas
```

- matplotlib 설치:
```dos
pip install matplotlib
```

- jupyter 설치:
```dos
pip install jupyter
```

**(중요) Mac OS 사용자**분들의 경우, matplotlib까지 설치가 끝난 후, 터미널 상에서 다음의 코드를 한 번 실행해 주시길 바랍니다. 이는 추후에 matplotlib가 무리 없이 실행되도록 하기 위해 선행되어야 하는 작업입니다.
```dos
echo "backend: TkAgg" > ~/.matplotlib/matplotlibrc
```