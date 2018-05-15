---
layout: post
title: "[Python Data Analysis]3.오리엔테이션, Python 개발 준비하기"
subtitle: "오리엔테이션, Python 개발 준비하기"
categories: dev
tags: data-analysis
comments: true
---

## 오리엔테이션, Python 개발 준비하기

### 원활한 Python 데이터 분석을 위한 핵심 도구

Python에서는 Python shell이라고 부르는 기본적인 대화식 프로그래밍 툴을 제공하는데, **IPython**은 이 기본 툴에 몇 가지 강력한 기능을 덧붙인 툴이라고 할 수 있습니다.


**IPython Notebook**은, IPython의 대화식 프로그래밍 방식을 기본적으로 제공하면서, 여러분이 데이터 분석을 하는 과정을 노트 형식으로 보기 쉽게 기록하고 정리해 놓을 수 있도록 도와주는 강력한 툴입니다.


### Python 데이터 분석 라이브러리

#### numpy

**numpy**는 주요한 Python 데이터 분석 라이브러리들의 기본 베이스가 되는 라이브러리입니다. numpy는 특히 벡터(vector) 및 행렬(array) 연산에 있어 엄청난 편의성을 제공하는 라이브러리입니다.


여러분이 데이터 분석을 하는 데 직접적으로 많이 사용하지는 않겠지만, 추후 많이 사용하게 될 pandas와 matplotlib의 기반이 되는 라이브러리라고 할 수 있습니다.


#### pandas

여러분은 **pandas**를 가장 많이 사용하게 될 것입니다. pandas는 고유하게 정의한 Series 및 DataFrame 등의 자료구조를 활용하여, 빅 데이터 분석에 있어 높은 수준의 퍼포먼스를 가능하게 하는 라이브러리입니다.


여러분이 기존에 엑셀로 하던 모든 분석을 더 큰 스케일의 데이터에 적용할 수 있으며, 더 빠른 속도로 수행할 수 있습니다.


#### matplotlib

**matplotlib**은 데이터 시각화를 위한 라이브러리입니다. 엑셀에서 차트를 그릴 경우 데이터의 양이 조금만 많아지더라도 엄청나게 버벅이는데, matplotlib을 사용하면 데이터 분석 결과에 대한 시각화를 빠르고 깔끔하게 수행해줍니다.


### 통계학을 모르는 데 할 수 있을지?

통계학을 잘 모르더라도 배울 수 있습니다. 통계 이론도 물론 중요하지만, 데이터를 바라보는 눈을 기르고, 데이터를 대하는 자세를 몸으로 익히는 것이 더 중요합니다. 고등학교 시절까지 배웠던 아주 기초적인 통계 지식만 있으면, 여러 가지 데이터셋에 대한 반복 연습으로 충분히 습득이 가능합니다.


### 어떠한 데이터를 다루게 되나?

#### USA.gov bit.ly dataset

인터넷 URL을 짧게 바꿔주는 bit.ly는 미국 정부 웹사이트인 usa.gov와 파트너십을 맺고, .gov 혹은 .mil로 끝나는 URL의 길이를 줄이는 사용자들의 데이터를 실시간 피드로 제공하기로 하였습니다.


USA.gov bit.ly 데이터셋은 아래 URL을 통해 확인할 수 있습니다.


https://github.com/usagov/1.USA.gov-Data


#### MovieLens 1M dataset

미국 미네소타 대학의 GroupLens에서 운영하는 MovieLens는 비영리 영화 평점 매기기 서비스가 있습니다. MovieLens에서는 각 사용자가 여러 개의 영화에 대하여 매긴 평점을 사용하여, 해당 사용자가 시청한 적이 없는 영화에 대한 예상 평점을 산출하고 이를 기반으로 사용자에게 새로운 영화를 추천합니다. GroupLens 측은 MovieLens에서 축적한 이러한 사용자별 영화 평점 데이터셋을 일반에 공개하였습니다.


[MovieLens 1M 데이터셋 다운로드](https://drive.google.com/open?id=0B9fcvsgEhJNsRm9kbVdQT3M3ZTg)


#### US Baby Names 1880-2014

Kaggle이라는 서비스가 있습니다. 여러 가지 종류의 데이터셋을 제시해 놓고, 이들 각각에 대한 특정한 데이터 분석 목표를 세워 놓은 뒤 이를 두고 세계 각국의 데이터 분석가들이 경쟁하는 곳입니다.


Kaggle에서 제공하는 데이터셋 중 US Baby Names 데이터셋을 소개합니다. 미국의 사회보장국에서 미국 내 매해 탄생하는 남아와 여아의 이름 통계 자료를 1880년도부터 2014년도까지 수집하여 공개하였는데, 이를 데이터셋으로 만든 것입니다.


[US Baby Names 데이터셋 다운로드](https://drive.google.com/open?id=0B9fcvsgEhJNsN0FUaGZudFYyTVU)


#### 2016 US Election dataset

Kaggle에서 제공하는 두 번째 데이터셋으로, 2016 US Election 데이터셋을 소개합니다. 미국 대선 후보들의 2016년 예비 선거(primary) 결과를 담은 데이터셋입니다. 미국의 지역 별 정치 여론을 잘 반영하고 있는 데이터셋이라고 할 수 있겠습니다.


[2016 US Election 데이터셋 다운로드](https://drive.google.com/open?id=0B9fcvsgEhJNscjN0WGpRckh4SGM)


#### Lending Club Loan dataset 2007-2015

Kaggle에서 제공하는 세 번째 데이터셋은 미국의 peer-to-peer 대출 서비스인 Lending Club이라는 업체에서 2007년부터 2015년 사이에 발생한 대출 관련 정보를 데이터셋으로 구성하여 공개한 Lendign Club Loan 데이터셋입니다. 워낙 많은 정보를 포함하고 있기 때문에, 추후 다양한 분석을 진행해볼 수 있는 여지가 있는 데이터셋입니다.


[Lending Club Loan 데이터셋 다운로드](https://drive.google.com/open?id=0B9fcvsgEhJNsVlZISXdPSGc4Zlk)


#### Deaths and Battles from Game of Thrones

Kaggle에서 제공하는 네 번째 데이터셋은 절찬리에 방영된 미국 TV 드라마 시리즈인 <왕좌의 게임(Game of Thrones>에서 벌어지는 전투와, 극중에서 사망하는 등장 인물들의 정보가 포함된 Deaths and Battles from Game of Thrones 데이터셋입니다.

[Game of Thrones 데이터셋 다운로드](https://drive.google.com/open?id=0B9fcvsgEhJNsbTlRLTVNZGdRQTQ)