---
layout: post
title: Power Analysis Summary
date: 2024-10-17 01:00:00 +0300
categories: [Statistics]
tags: [Power, SampleSize] # add tag
---


I've studied many statistical methods over the years, but recently, as I learned about biostatistics and survival analysis, I started working with clinical trial data. I was surprised to see how small the sample sizes can be. My professor even mentioned that having just six samples is possible, which shocked me at first. I couldn’t understand how a test could be valid with such a small sample size.

Power analysis helps us decide how many samples we need before running an experiment. It depends on three things: how much power we want, the significance level, and the effect size. Researchers need to know this in advance because experiments cost money, and it's important to design tests efficiently.

Since I want to study statistics and provide statistical analysis, I found power analysis really interesting.

In simple terms, power analysis is an important statistical tool used during study planning. It helps researchers make sure they have enough data (sample size) to test their hypothesis. It calculates the "power" of a statistical test, which tells us how likely we are to detect a real effect. The higher the power, the more reliable the study results.


## Core Concepts in Power Analysis
1. Power: This is the probability that the study will correctly identify a true effect. A power of 80% or higher is commonly targeted, meaning that the study has an 80% chance of detecting an actual effect if one exists.

2. Type I Error (α): Also known as a false positive error, this occurs when we conclude that there is an effect when there is none. It is usually set at 5% (0.05), which means there is a 5% chance of making this error.

3. Type II Error (β): Also known as a false negative error, this occurs when we fail to detect an effect that actually exists. Power is calculated as 1 - β, so as β decreases, power increases.

4. Effect Size: This is the magnitude of the difference or relationship the study aims to detect. For example, in a study comparing the means of two groups, the effect size is the expected difference between the groups. Larger effect sizes require smaller sample sizes to achieve the same power.

5. Sample Size: The number of data points needed to detect the effect. The larger the sample size, the more accurate the results tend to be, but it’s important to find a balance to avoid excessive costs or data collection efforts.


## Types of Power Analysis
1. A Priori Power Analysis: Conducted before a study begins, this analysis helps determine the sample size required to achieve a desired power level given a specific effect size and significance level (α).

2. Post-hoc Power Analysis: Done after data collection, this analysis calculates the achieved power based on the collected data. It’s less commonly used than a priori analysis, but can help assess the study’s reliability after the fact.

3. Sensitivity Analysis: This analysis estimates the minimum detectable effect size given a fixed sample size and significance level. It is useful when sample size is constrained.

4. Equivalence Testing Power Analysis: This type of analysis is used in studies designed to prove equivalence rather than detect a difference, such as in equivalence or non-inferiority tests.


## How to calculate?
Power analysis relies on balancing four main elements:

1. Significance Level (α): The probability of making a Type I error, often set at 0.05.
2. Power (1 - β): Typically set at 0.8 (80%) or higher to ensure the study is reliable.
3. Effect Size: The hypothesized difference or relationship the study aims to detect, often based on previous studies or empirical data.
4. Sample Size: Based on the above criteria, the power analysis will estimate the minimum sample size needed.

## Examples

아, sample size와 power analysis의 대표적인 예시들을 정리해 드리겠습니다. 각 예시는 연구 설계에서 자주 사용되는 유형으로, 연구 목적에 따라 다양한 방식으로 sample size를 결정할 수 있습니다.

---

### 1. **Two-Group Mean Comparison (Independent t-test)**
   - **상황**: 두 그룹 간 평균 차이를 검증할 때
   - **예시**: 새로운 약물 치료군과 기존 치료군의 평균 혈압 수치를 비교하는 경우.
   - **Power Analysis 방법**: 예상 효과 크기(cohen’s d), 유의 수준(α), 원하는 검정력(보통 0.8)을 설정하여 각 그룹의 필요 표본 크기를 계산.
   - **도구**: R의 `pwr.t.test()` 또는 G*Power를 사용해 표본 크기 계산.

근데 여기서 생각보다 애를 먹는거는 effect size (d)를 구하는것이다. 
https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F21614C4651E9DD0E1A
보통 two sample t-test에서는 이 공식을 이용한다 .
---

### 2. **ANOVA (Analysis of Variance) for Multiple Groups**
   - **상황**: 세 그룹 이상에서 평균 차이를 비교할 때
   - **예시**: 세 가지 다른 식이요법에 따른 체중 감소 효과를 비교.
   - **Power Analysis 방법**: 예상 효과 크기(cohen’s f), 유의 수준, 검정력을 설정하고 각 그룹의 표본 크기 요구를 계산.
   - **도구**: G*Power의 `ANOVA: Fixed effects, omnibus, one-way` 기능을 사용해 표본 크기를 결정.

---

### 3. **Chi-Square Test for Proportions**
   - **상황**: 두 그룹 간 비율(또는 분포)을 비교할 때
   - **예시**: 치료군과 대조군에서 특정 부작용이 발생할 확률 비교.
   - **Power Analysis 방법**: 예상되는 각 그룹의 비율, 유의 수준, 검정력을 설정하고 필요 표본 크기 계산.
   - **도구**: G*Power의 `Chi-square tests - Goodness-of-fit tests: Contingency tables` 기능을 이용해 표본 크기 계산.

---

### 4. **Correlation Analysis**
   - **상황**: 두 변수 간 상관관계를 평가할 때
   - **예시**: 수면 시간과 작업 성과 간의 상관관계를 분석하고자 할 때.
   - **Power Analysis 방법**: 예상 상관계수(r), 유의 수준, 검정력에 따라 필요 표본 크기 계산.
   - **도구**: R의 `pwr.r.test()`나 G*Power에서 `Correlation: Bivariate normal model`을 선택해 계산.

---

### 5. **Survival Analysis (Log-Rank Test)**
   - **상황**: 생존 데이터에서 두 그룹의 생존 곡선을 비교할 때
   - **예시**: 신약 투여군과 대조군 간의 생존율 차이 평가.
   - **Power Analysis 방법**: 두 그룹의 생존율, 예상 사건 발생 비율, 유의 수준, 검정력을 설정해 표본 크기 계산.
   - **도구**: G*Power에서 `Survival Analysis` 또는 `Log-Rank Test` 옵션을 통해 표본 크기 산정.

---

### 6. **Regression Analysis**
   - **상황**: 연속형 종속 변수에 대해 여러 독립 변수를 포함한 회귀 모델을 구축할 때
   - **예시**: 나이, 운동량, 식단 등과 같은 요인이 혈압에 미치는 영향을 분석.
   - **Power Analysis 방법**: 독립 변수 개수, 예상 효과 크기(f²), 유의 수준, 검정력을 설정해 회귀 모델에 필요한 표본 크기 결정.
   - **도구**: G*Power에서 `F tests - Linear multiple regression: Fixed model, R² deviation from zero`를 사용해 계산.

---

이와 같은 예시들은 다양한 연구 설계에서 표본 크기를 결정하는 데 자주 사용됩니다. 각 방법에 적합한 도구를 통해 효과 크기와 검정력, 유의 수준을 설정하여 정확한 표본 크기를 계산할 수 있습니다.

https://www.youtube.com/watch?v=VX_M3tIyiYk