---
layout: post
title: "[Python Data Analysis]25.pandas의 그룹화 기능을 사용한 데이터 분석 맛보기
subtitle: "2016 US Election 데이터셋 분석"
categories: dev
tags: data-analysis
comments: true
---

## pandas의 그룹화 기능을 사용한 데이터 분석 맛보기

### 2016 US Election 데이터셋 분석

#### 2016 US Election 데이터셋 분석하기

[2016 US Election 데이터셋 다운로드]

##### 2016 US Election 데이터셋의 주요 컬럼 요약

##### primary_results.csv

- state: state where the primary or caucus was held

- state_abbreviation: two letter state abbreviation

- county: county where the results come from

- fips: FIPS county code

- party: Democrat or Republican

- candidate: name of the candidate

- votes: number of votes the candidate received in the corresponding state and county (may be missing)

- fraction_votes: fraction of votes the president received in the corresponding state, county, and primary

##### county_facts.csv

- "RHI125214: White alone, percent, 2014

- "RHI225214": Black or African American alone, percent, 2014

- "RHI325214": "American Indian and Alaska Native alone, percent, 2014

- "RHI425214": Asian alone, percent, 2014

- "RHI525214": Native Hawaiian and Other Pacific Islander alone, percent, 2014

- "RHI625214": Two or More Races, percent, 2014

- "RHI725214": Hispanic or Latino, percent, 2014

- "RHI825214": White alone, not Hispanic or Latino, percent, 2014


_(기타 컬럼 생략)_


* 참고: https://www.kaggle.com/benhamner/2016-us-election

#### 각 후보 별 전체 득표수 계산하기
```python
candidate_to_votes_s = primary.groupby("candidate")["votes"].sum().sort_values()
candidate_to_votes_s.plot(kind="barh", fontsize=8)
```

#### 각 주별, 각 정당의 득표 비율 계산하기
```python
state_party_to_votes_s = primary.groupby(["state", "party"])["votes"].sum()
state_to_votes_s = primary.groupby("state")["votes"].sum()
state_party_to_vote_pcts_s = state_party_to_votes_s / state_to_votes_s
state_party_to_vote_pcts_s.unstack().plot(kind="barh", stacked=True, fontsize=8)
```

#### 각 후보가 당선된 county의 평균 백인 유권자 비율 조사하기
```python
func = lambda agg_df: agg_df.sort_values("votes", ascending=False).iloc[0]
winners = primary.groupby("fips").agg(func)
winners_county_races = pd.merge(winners, counties[["fips", "RHI825214"]], 
                                left_index=True, right_on="fips", how="left")
winners_county_races = \
    winners_county_races.rename(columns={"RHI825214":"white_pcts"})
    winners_county_white_pcts = winners_county_races.groupby(["party", "candidate"])["white_pcts"].mean()
ax = winners_county_white_pcts.plot(kind="barh", fontsize=8)
ax.set_xlim([50, 100])
plt.tight_layout()
```

#### Pivot Table 사용하기

**'피벗 테이블(pivot table)'**을 사용하면, 데이터셋에 대하여 그룹화에 기반한 통계량을 계산하는 작업이 더 간편해집니다.

피벗 테이블은 `df.pivot_table()` 함수를 사용하여 생성합니다. `values` 인자로는 통계량을 계산할 열을, `index`와 `columns` 인자는 각각 그 값을 피벗 테이블의 인덱스와 컬럼으로 사용할 열을, `aggfunc` 인자로는 적용할 통계 함수를 명시합니다.

```python
total_votes = primary.pivot_table(values="votes", index="state", 
                                  columns="candidate", aggfunc="sum", 
                                  fill_value=0)
```

예를 들어 `total_votes`라는 피벗 테이블은 "state"와 "candidate" 열의 값을 그룹화 기준으로 하여, "votes" 열의 값의 합계를 산출한 결과입니다. 이 때 `fill_value=0`인자를 넣어주면, `NaN`이 나올 부분이 0으로 대체됩니다. 피벗 테이블도 DataFrame 형태를 지닙니다.


혹은 다음과 같이 하면 "state_abbreviation"과 "party" 열의 값을 그룹화 기준으로 하여, "fraction_votes" 열의 값의 평균을 나타내는 피벗 테이블을 만들 수 있습니다.

```python
primary.pivot_table(values="fraction_votes", index="state_abbreviation", 
                    columns="party", aggfunc="mean")
```