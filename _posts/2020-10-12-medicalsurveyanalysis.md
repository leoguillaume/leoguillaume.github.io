---
layout: single
title: "Data analysis of a medical survey"
excerpt: "basic data analysis of a medical survey"
header:
  teaser: "assets/images/2020_01_header.jpg"
categories:
  - Data analysis
tags:
  - data analysis
  - python
read_time: true
author_profile: true
share: true
---
My friend [Sarah Le Brenn](https://www.linkedin.com/in/sarah-le-brenn-1a9337102/) in PhD of pharmacy at the University of Nantes (France) needed a helping hand analyzing data from a survey she conducted. The survey questioned transplant patients with cystic fibrosis to find out what questions they have to ask themselves in order to gain a better understanding of their concerns.

The survey was composed of informations on the patient (age, sex and health care center) and 100 questions. Each question had the same possible answers: yes, no and why, partially and why. The repetition of the question patterns is really cool for me, I can easily loop!

The answers was storage in a xls file. In this article I show how I was able to meet Sarah's needs with Python and in particular how to automatically generate and save charts. She needed basics statistical analysis and some data visualisations.

```python
# library imports
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import os, re

# data import
data = pd.read_excel('Questionnaire-patients-réponses.xlsx')
```
### Data cleaning
First of all, I needed to clean data. Because questions and informations about patients are mixed in the excel table, I reindex the columns (every questions started with a digit) to manipulate questions more easily. 

```python
data = data.reindex(sorted(data.columns), axis=1)
```
