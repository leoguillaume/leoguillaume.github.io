---
layout: single
title: "Data analysis of a medical survey"
excerpt: "Basic data analysis of a medical survey"
categories:
  - data analysis
read_time: true
author_profile: true
toc: true
share: true
---
My friend Sarah in PhD of pharmacy at the University of Nantes (France) needed a helping hand analyzing data from a survey she conducted. The survey questioned transplant patients with cystic fibrosis to find out what questions they have to ask themselves in order to gain a better understanding of their concerns.

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
Then the age column was polluted by 'ans' strings (years old in French). Moreover, the patients came from 3 different care centers (Nantes, Bordeaux and Strasbourg) and there were different syntaxes for each.

```python
data['âge'] = data['âge'].astype(dtype = 'str').map(lambda x: x.strip().rstrip('ans').strip()).astype(dtype = 'int')

def care_center_cleaning(x):
    x = x.strip().lower()
    if re.findall('nantes|laennec', x):
        return 'nantes'
    elif re.findall('strasbourg', x):
        return 'strasbourg'
    else:
        return 'bordeaux'

data['Centre de suivi'] = data['Centre de suivi'].apply(care_center_cleaning)      
```
Finaly, I replace NaN values by 'NA' string to manipulate them easily.

```python
data = data.fillna('NA')
```

### Global answer rate

```python
data_1 = data.copy()

data_1 = data_1.replace('oui', 1)
data_1 = data_1.replace('non', 1)
data_1= data_1.replace('partiellement', 1)
data_1 = data_1.replace('NA', 0)

v = data_1.iloc[:,:104].groupby(data_1.Sexe).count().sum(axis = 1).sort_index()
v_sexe = (data_1.Sexe.value_counts() * 104).sort_index()

plt.figure()

values.plot(kind='bar')
for i in range(2):
    plt.text(x = i - 0.1, y = values[i] + 100, s = '{:.2f}%'.format(values[i] / v_sexe[i]))
plt.title('Réponses par sexe', weight = 'bold')
plt.gca().set_ylim([0, values.max() + 500])
plt.xlabel('Sexe')
plt.ylabel('Nombre de réponses')
plt.show()
```
