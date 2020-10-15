---
layout: single
title: "Generate multiple charts from a medical survey"
excerpt: "Basic data visualisations of a medical survey"
categories:
  - data analysis
read_time: true
author_profile: true
toc: true
share: true
comments: true
---
My friend Sarah in PhD of pharmacy at the University of Nantes (France) needed a helping hand to create data visualisations from a survey she conducted. The survey questioned transplant patients with cystic fibrosis to find out what questions they have to ask themselves in order to gain a better understanding of their concerns.

The survey was composed of informations on the patient (age, gender and health care center) and 103 questions. Each question had the same possible answers: yes, no and why, partially and why. The repetition of the question patterns is really cool for me, I can easily loop!

The answers was storage in a xls file. In this article I show how I was able to meet Sarah's needs with Python and in particular how to automatically generate and save charts. I skip the data cleaning, which essentially consisted of normalizing text data.

```python
# Library imports
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import os, re

# Data import
data = pd.read_excel('Questionnaire-patients-réponses.xlsx')

# Reindex columns to aggregate questions (they start with a digit) on the left
# of the table and the informations about patients on the right.

data = data.reindex(sorted(data.columns), axis=1)
```

# Global answer rate

Every answers have this pattern: `oui / non / partiellement / NA (+ comment)`. To calculate
the response rate, I have to calculate the number of "yes", "no" and "partially" for all the questions.
By replacing these values with one or zero digit, I can easily add them together.


| Q0       | Q1                 | Q2            | ... | Q103 | Sexe  |
|----------|--------------------|---------------|-----|------|-------|
| oui      | NA                | oui           |     | oui  | Femme |
| non, ... | partiellement, ... | non           |     | oui  | Homme |
| NA     | oui, ...           | partiellement |     | NA  | Femme |

<span style='font-size:30px;'>&#8681;</span>

| Q0      | Q1                | Q2            | ... | Q103 | Sexe  |
|----------|--------------------|---------------|-----|------|-------|
| 1    | 0                | 1          |     | 1 | Femme |
| 1| 1 | 1          |     | 1  | Homme |
|0     |1          | 1 |     | 0 | Femme |

```python
df_1 = data.copy()

for i in range(104):
    df1[df1.columns[i]][df[df.columns[i]].str.match('oui|partiellement|non')] = 1
    df1[df1.columns[i]][~df[df.columns[i]].str.match('oui|partiellement|non')] = 0
```

## Per gender
```python
v = df1.iloc[:,:104].groupby(df1.Sexe).sum().sum(axis = 1).sort_index()
v_sexe = (df1.Sexe.value_counts() * 104).sort_index()

plt.figure()
values.plot(kind='bar')
for i in range(2):
    plt.text(x = i - 0.1, y = v[i] + 100, s = '{:.2f}%'.format(v[i] / v_sexe[i]))
plt.title('Réponses par sexe', weight = 'bold')
plt.gca().set_ylim([0, values.max() + 500])
plt.xlabel('Sexe')
plt.ylabel('Nombre de réponses')
plt.show()
```
![](https://github.com/leoguillaume/leoguillaume.github.io/tree/master/assets/images/2020-10-12-chart_1.png)

## Per heath care center
```python
v = df1.iloc[:,:104].groupby(df1['Centre de soin']).sum().sum(axis = 1).sort_index()
v_center = (df1['Centre de soin'].value_counts() * 104).sort_index()

plt.figure()
values.plot(kind='bar')
for i in range(2):
    plt.text(x = i - 0.1, y = v[i] + 100, s = '{:.2f}%'.format(v[i] / v_center[i]))
plt.title('Réponses par centre de suivi', weight = 'bold')
plt.gca().set_ylim([0, values.max() + 500])
plt.xlabel('Centre de suivi')
plt.ylabel('Nombre de réponses')
plt.show()
```
![](https://github.com/leoguillaume/leoguillaume.github.io/tree/master/assets/images/2020-10-12-chart_2.png)

## Per age

```python
df1['age_cut'] = pd.cut(df1.âge, 4)

plt.figure()
v_age = df2['age_cut'].value_counts().sort_index()
df1.iloc[:,:104].groupby(df2['age_cut']).count().sum(axis = 1).divide(v_age).plot(kind = "bar")
plt.title('Taux de réponse par tranche d\'âge', weight = 'bold')
plt.xlabel('âge')
plt.ylabel('%')
plt.show()
```

![](https://github.com/leoguillaume/leoguillaume.github.io/tree/master/assets/images/2020-10-12-chart_2.png)


# Answer rate per question

## Per sexe
## Per heath care center
