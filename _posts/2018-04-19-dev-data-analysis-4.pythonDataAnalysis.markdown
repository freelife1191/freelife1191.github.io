---
layout: post
title: "[Python Data Analysis]4.데이터 분석 환경 구성"
subtitle: "데이터 분석이란?"
categories: dev
tags: data-analysis
comments: true
---

## (Windows) 데이터 분석 환경 구성

### Python 데이터 분석을 위한 환경 구성하기

Anaconda는 데이터 분석을 위한 오픈 소스 Python 플랫폼입니다. 단 한 번의 설치로 모든 환경 설정을 한 방에 끝내주기 때문에, Windows, Mac OS 사용자들이 사용하기에 아주 좋습니다.

한편 miniconda는 Anaconda의 핵심 부분만을 추출해서 재구성한 플랫폼으로, 고유한 패키지 관리 시스템인 conda와 기본적인 Python만을 포함하고 있기 때문에 설치 소요 시간이 더 짧습니다.

Windows, Mac OS 사용자분들의 경우, 본 동영상에 따라 miniconda를 설치해 주시길 바랍니다.

링크 및 명령어를 아래와 같이 명시하였습니다.

#### miniconda 설치 (Windows)

- miniconda 설치 파일 다운로드 링크:

http://conda.pydata.org/miniconda.html

- conda 버전 업데이트:
```dos
conda update conda
```

- Python 버전 확인:
```dos
python --version
```

- pip 패키지 매니저를 사용하여 IPython 설치:
```dos
pip install ipython
```

#### miniconda 설치 (Mac OS)

- miniconda 설치 파일 다운로드 링크:

http://conda.pydata.org/miniconda.html

- miniconda 설치 파일을 다운로드 디렉터리로 옮긴 뒤, 실행 가능하도록 권한 설정:
```dos
chmod u+x Miniconda3-latest-MacOSX-x86_64.sh
```

- 권한 설정 후 miniconda 설치 파일 실행:
```dos
./Miniconda3-latest-MacOSX-x86_64.sh
```

- pip 패키지 매니저를 사용하여 IPython 설치:
```dos
pip install ipython
```