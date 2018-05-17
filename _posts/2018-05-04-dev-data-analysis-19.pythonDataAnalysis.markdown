---
layout: post
title: "[Python Data Analysis]19.matplotlib를 사용한 데이터 시각화 맛보기"
subtitle: "Gammatplotlib를 사용한 데이터 시각화 맛보기"
categories: dev
tags: dataAnalysis
comments: true
---

## matplotlib를 사용한 데이터 시각화 맛보기

### Gammatplotlib를 사용한 데이터 시각화 맛보기

#### Game of Thrones 데이터셋 분석하기

[Game of Thrones 데이터셋 다운로드](https://drive.google.com/open?id=0B9fcvsgEhJNsbTlRLTVNZGdRQTQ)

##### Game of Thrones 데이터셋의 주요 컬럼 요약

##### battles.csv
- name: String variable. The name of the battle.

- year: Numeric variable. The year of the battle.

- battle_number: Numeric variable. A unique ID number for the battle.

- attacker_king: Categorical. The attacker's king. A slash indicators that the king charges over the course of the war. For example, "Joffrey/Tommen Baratheon" is coded as such because one king follows the other in the Iron Throne.

- defender_king: Categorical variable. The defender's king.

- attacker_1: String variable. Major house attacking.

- attacker_2: String variable. Major house attacking.

- attacker_3: String variable. Major house attacking.

- attacker_4: String variable. Major house attacking.

- defender_1: String variable. Major house defending.

- defender_2: String variable. Major house defending.

- defender_3: String variable. Major house defending.

- defender_4: String variable. Major house defending.

- attacker_outcome: Categorical variable. The outcome from the perspective of the attacker. Categories: win, loss, draw.

- battle_type: Categorical variable. A classification of the battle's primary type. Categories: pitched_battle: Armies meet in a location and fight. This is also the baseline category. ambush: A battle where stealth or subterfuge was the primary means of attack. siege: A prolonged of a fortied position. razing: An attack against an undefended position

- major_death: Binary variable. If there was a death of a major figure during the battle.

- major_capture: Binary variable. If there was the capture of the major figure during the battle.

- attacker_size: Numeric variable. The size of the attacker's force. No distinction is made between the types of soldiers such as cavalry and footmen.

- defender_size: Numeric variable. The size of the defenders's force. No distinction is made between the types of soldiers such as cavalry and footmen.

- attacker_commander: String variable. Major commanders of the attackers. Commander's names are included without honoric titles and commandders are seperated by commas.

- defender_commander: String variable. Major commanders of the defener. Commander's names are included without honoric titles and commandders are seperated by commas.

- summer: Binary variable. Was it summer?

- location: String variable. The location of the battle.

- region: Categorical variable. The region where the battle takes place. Categories: Beyond the Wall, The North, The Iron Islands, The Riverlands, The Vale of Arryn, The Westerlands, The Crownlands, The Reach, The Stormlands, Dorne

- note: String variable. Coding notes regarding individual observations.


##### character-deaths.csv

- Name: character name

- Allegiances: character house

- Death Year: year character died

- Book of Death: book character died in

- Death Chapter: chapter character died in

- Book Intro Chapter: chapter character was introduced in

- Gender: 1 is male, 0 is female

- Nobility: 1 is nobel, 0 is a commoner

- GoT: Appeared in first book

- CoK: Appeared in second book

- SoS: Appeared in third book

- FfC: Appeared in fourth book

- DwD: Appeared in fifth book


*** 참고: https://www.kaggle.com/mylesoneill/game-of-thrones


#### 작품 번호에 따른 인물들의 죽음 횟수 시각화하기 - 라인 플롯
```python
book_nums_to_death_count = deaths["Book of Death"].value_counts().sort_index()
ax1 = book_nums_to_death_count.plot(color="k", marker="o", linestyle="--")
ax1.set_xticks(np.arange(1, 6))
ax1.set_xlim([0, 6])
ax1.set_ylim([0, 120])
```

#### 대규모 전투 상에서 공격군과 수비군 간의 병력 차이 시각화하기 - 박스 플롯
```python
battles = battles.set_index(["name"])
large_battles_mask = battles["attacker_size"] + battles["defender_size"] > 10000
large_battles = battles.loc[large_battles_mask, ["attacker_size", "defender_size"]]
ax2 = large_battles.plot(kind="barh", stacked=True, fontsize=8)
```
```python
large_battles["attacker_pcts"] = \
    large_battles["attacker_size"] / (large_battles["attacker_size"] 
    + large_battles["defender_size"])
large_battles["defender_pcts"] = \
    large_battles["defender_size"] / (large_battles["attacker_size"] 
    + large_battles["defender_size"])
    ax3 = large_battles[["attacker_pcts", "defender_pcts"]].plot(kind="barh", stacked=True, fontsize=8)
```

#### 전체 전투 중 각 가문의 개입 빈도 시각화하기 - 히스토그램
```python
col_names = battles.columns[4:12]
house_names = battles[col_names].fillna("None").values
house_names = np.unique(house_names)
house_names = house_names[house_names != "None"]
houses_to_battle_counts = pd.Series(0, index=house_names)
```
```python
for col in col_names:
    houses_to_battle_counts = \
    houses_to_battle_counts.add(battles[col].value_counts(), fill_value=0)
ax4 = houses_to_battle_counts.hist(bins=10)
```
