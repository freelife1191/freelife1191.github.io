---
layout: post
title: "[Python Data Analysis]16.pandas를 사용한 데이터 분석 맛보기"
subtitle: "Lending Club Loan 데이터셋 분석"
categories: dev
tags: data-analysis
comments: true
---

## pandas를 사용한 데이터 분석 맛보기

### Lending Club Loan 데이터셋 분석

#### 파일 읽기

[Lending Club Loan 데이터셋 다운로드](https://drive.google.com/open?id=0B9fcvsgEhJNsVlZISXdPSGc4Zlk)

본 강의에서는, Lending Club Loan dataset 2007-2015를 사용합니다.

대부분의 데이터셋은 열과 열을 구분하기 위한 구분자로 특정한 문자를 사용합니다. 구분자는 보통 콤마 ','를 많이 쓰는데, 콤마를 구분자로 사용한 파일을 특별히 **'CSV(comma-separated values) 파일'**이라고 부릅니다.


CSV 파일은 pd.read_csv() 함수를 사용하여 손쉽게 읽어들일 수 있습니다. 해당 함수를 호출할 때, 읽어들일 데이터 파일의 경로와 구분자 등을 입력합니다.

```python
dfd  = pd.read_csv("data/lending-club-loan-data/loan.csv", sep=",")
```

#### Lending Club Loan dataset 분석하기

##### Lending Club Loan dataset의 주요 컬럼 요약

- loan_amnt: 대출자의 대출 총액

- funded_amnt: 해당 대출을 위해 모금된 총액

- issue_d: 대출을 위한 기금이 모금된 월

- loan_status: 대출의 현재 상태*

- title: 대출자에 의해 제공된 대출 항목

- purpose: 대출자에 의해 제공된 대출 목적

- emp_length: 대출자의 재직 기간

- grade: LC assigned loan grade**

- int_rate: 대출 이자율

- term: 대출 상품의 기간 (36-month vs. 60-month)


*** 불량 상태(bad status): "Charged Off", "Default", "Does not meet the credit policy. Status:Charged Off", "In Grace Period", "Default Receiver", "Late (16-30 days)", "Late (31-120 days)"


** LC loan grade 참고: https://www.lendingclub.com/public/rates-and-fees.action


#### 필요한 열 발췌 및 결측값 제거하기
```python
df2d  = df[["loan_amnt", "loan_status", 
          "grade", "int_rate", "term"]]
df2 = df2.dropna(how="any")
```

#### '36개월 대출'과 '60개월 대출'의 대출 총액 파악
```python
term_to_loan_amnt_dictt  = {}
uniq_terms = df2["term"].unique()
for term in uniq_terms:
    loan_amnt_sum = df2.loc[df2["term"] == term, "loan_amnt"].sum()
    term_to_loan_amnt_dict[term] = loan_amnt_sum
term_to_loan_amnt = pd.Series(term_to_loan_amnt_dict)
```

#### 각 대출 상태(불량/우량)에 따른 대출 등급 분포 파악
```python
total_status_category = df2[t "loan_status"].unique()
bad_status_category = total_status_category[[1, 3, 4, 5, 6, 8]]
df2["bad_loan_status"] = df2["loan_status"].isin(bad_status_category)
bad_loan_status_to_grades = \
    df2.loc[df2["bad_loan_status"] == True, "grade"].value_counts()
bad_loan_status_to_grades.sort_index()
```

#### 대출 총액과 대출 이자율 간의 상관관계 파악
```python
df2[d "loan_amnt"].corr(df2["int_rate"])
```

#### 파일 쓰기

여러분이 얻을 `bad_loan_status_to_grades` Series를 외부 파일로 쓰는 작업을 진행해보도록 합시다. 이는 DataFrame에 대해서도 동일하게 적용됩니다.

`Series.to_csv()` 혹은 `df.to_csv()` 함수를 사용하면, 현재 Series 혹은 DataFrame 형태로 들고 있는 분석 결과물을 외부 파일로 손쉽게 쓸 수 있습니다. 해당 함수를 호출할 때, 저장할 파일의 경로와 구분자 등을 인자로 같이 입력합니다.

```python
bad_loan_status_to_grades.to_csv(b "bad_loan_status.csv", sep=",")
```