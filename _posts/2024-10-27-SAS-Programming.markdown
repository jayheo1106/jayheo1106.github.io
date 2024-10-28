---
layout: post
title: SAS Programming
date: 2024-10-17 04:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: rna.avif # Add image post (optional)
categories: [SAS]
tags: [programming, SAS] # add tag
---


Hello! I’d like to share some recent updates about myself and share my past project using SAS programming.

In the fall semester of 2022, I took an Intro to SAS Programming course at Ohio State University. I had been programming mostly in R, so learning a new language was very exciting, especially with such a great professor!

Right now, I’m preparing to become a biostatistician, and SAS programming is one of the essential skills required. Looking back, I wish I had aimed to earn the SAS programming certification while taking that class! Haha. To prove my skills, I’m planning to obtain that certification by December. Here we go!

And now, I’d like to introduce a project that I worked hard on back in 2022.

## Introduction
As global warming and greenhouse gas emissions become increasingly important topics on the world stage, one industry in particular is experiencing a revolution: the automobile industry. Due to a demand for alternatives to today’s fossil fuel powered automobiles, competition in the electric vehicle sector is booming. As a result, the number of electric vehicles in the market has proliferated at a rate never seen before. But how will consumers choose the best electric vehicle? Do the properties of the vehicle change under different conditions? There are many standards used to evaluate electric vehicles, including acceleration time, safety, weight, battery, charging time, life span, and many more. The challenge of determining the best electric vehicle brands is a daunting one, but still attractive to data analysts. In this study, we will use SAS to explore various questions related to electric vehicles, and return a performance ranking based on electric vehicle data pulled from the Electric Vehicle Database.

## Data
**Sources:**  
Our dataset includes 194 EVs on the market up to 2022, manually collected from [ev-database.org](https://ev-database.org) by Mo Shiha. Each entry contains properties such as range under various conditions, technical specifications, battery capacities, and more.

**Variables:**
- **Original Variables:**  
  - **id**: unique identifier  
  - **Make**: brand of the car  
  - **link**: source URL  
  - **Range (Cold/Mild Weather)**: km range under city/highway/combined conditions in cold (-10°C) and mild (23°C) weather  
  - **Acceleration 0 - 100 km/h**: acceleration from 0 to 100 km/h  
  - **Top Speed**: max speed in km/h  
  - **Electric Range**: advertised range in km  
  - **Battery Capacity**: kWh  
  - (Additional technical specs follow in the original document.)

- **New Variables Created:**  
  - **Avg_Range**: average range across all weather conditions  
  - **Avg_City**, **Avg_Highway**, **Avg_Combined**: average city, highway, and combined ranges respectively  
  - **Charge_Time**: calculated by `Electric Range / Charge Speed`  
  - **RangeScore**: calculated by `Electric Range / Total Power`

![image](https://1drv.ms/i/c/de797db04860adb9/IQTmfKTQImVtQow66ZaGdnEDAdr-BuIvi5ln0ghs5ZFKyww?width=1024&height=1758)

## Summary
In Table 1, 34 brands are analyzed. Key findings include:
- Renault has the best average range per battery power.
- Mercedes shows the best advertised and actual electric ranges.
- Mini performs best in charging time, while Dacia excels in acceleration.
  
A more reliable conclusion can be drawn if each brand has more samples.


## Analysis
### Specific Question (Jay's Question): Range Over 300 Miles

**Objective:**  
The objective of this analysis is to determine whether the average range of electric vehicles (EVs) on a full charge exceeds 300 miles. In the past, Tesla was one of the only major manufacturers producing vehicles with such a range. However, advancements in EV technology have led many other automakers to introduce models surpassing this threshold. This shift is critical to understanding both the progress within the EV industry and the growing options available to consumers seeking extended vehicle range.

**Methods:**  
A one-sample t-test was conducted using `PROC TTEST` in SAS to assess whether the mean range of electric vehicles is greater than 300 miles. The null hypothesis assumed the average range to be 300 miles, while the alternative hypothesis proposed that it is greater than 300 miles.

**Results:**  
The test yielded a significant p-value, leading to the rejection of the null hypothesis. This suggests that the average range of EVs indeed exceeds 300 miles. The 95% confidence interval for the mean range spans from 333.6 miles to infinity, which provides further statistical evidence that modern EVs have evolved to meet and surpass this milestone. This outcome supports the notion that the electric vehicle industry has made substantial strides in recent years.

## Discussion
The results of this analysis underscore the notable advancements in EV technology, specifically in achieving ranges that exceed 300 miles, a previously rare feat. This finding is a testament to the rapid growth and innovation within the EV industry, as manufacturers strive to enhance battery efficiency and vehicle design to meet evolving consumer demands. While the statistical test indicates a strong trend towards longer ranges, it is essential to note several limitations within the data.

First, the dataset includes varying sample sizes across brands, with some brands represented by only a few models. This variation could introduce a degree of bias, as certain manufacturers with limited samples might not reflect broader trends within the company. Additionally, the dataset does not cover all EV brands on the market, excluding key players like Mitsubishi, which may impact the generalizability of the findings. 

Lastly, while range and charging capabilities are important indicators of EV performance, other factors, such as vehicle design, price, and charging infrastructure, also play crucial roles in consumer decisions. Automakers balance these features based on industry trends and consumer needs, meaning that range alone may not fully capture a vehicle's performance. Despite these considerations, this analysis highlights a pivotal shift in the EV industry, where extended range capabilities are becoming increasingly standard, illustrating both technological advancement and a promising future for electric mobility.

## References
- Bengt Halvorson. "Range life: The 8 EVs EPA-rated for 300 miles or more." *Green Car Reports*, September 19, 2021, [source](https://www.greencarreports.com/news/1133620_range-life-the-8-evs-epa-rated-for-300-miles-or-more)
- Lora D. Delwiche and Susan J. Slaughter. *The Little SAS Book, 6th Edition*. SAS Institute.
- Mo Shiha, "Electric Vehicles", Kaggle, [dataset link](https://www.kaggle.com/datasets/mohamedalishiha/electric-vehicles?resource=download)
- SAS Institute, Inc. (2018). *SAS Studio 3.8 (Enterprise Edition)* for Linux.
- KIA Motors, [website link](https://www.kia.com/kr/vehicles/kia-ev/vehicles)
- "What Do Consumers Really Want From an Electric Vehicle?", *iVendi*, March 3, 2022, [source](https://www.ivendi.com/news/what-do-consumers-really-want-from-an-electric-vehicle)
