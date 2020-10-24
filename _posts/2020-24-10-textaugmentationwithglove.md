---
layout: single
title: "Text augmentation with Glove"
excerpt: "A use case of text augmentation with word embeddings of Glove"
categories:
  - web
header:
    teaser: https://leoguillaume.github.io/assets/images/2020-10-24-textaugmentationwithglove/teaser.jpg
read_time: true
author_profile: true
toc: true
share: true
tags:
  - python
  - nltk
  - glove
  - text augmentation
comments: true
---
For [Vivadata](https://vivadata.org/), I wrote an exercice about text augmentation with word embeddings. There are many way to do text augmentation, **here it's a use case of text augmentation with word embeddings of Glove to improve a classification model**.

*[Glove](https://nlp.stanford.edu/projects/glove/) is a Stanford project developed by Jeffrey Pennington, Richard Socher, Christopher D. Manning. It's a unsupervised learning algorithm for obtaining vector representations for words.*

The dataset is a SMS collection from [Kaggle](https://www.kaggle.com/uciml/sms-spam-collection-dataset) with 2 labels, spam (1) or ham (0). The aim is to a train binary classifier model to detect the spams :mailbox_with_mail:.

We'll compare the model (*a logistic regression*) with and without text augmentation.

```python
# imports

import pandas as pd
import numpy as np

import nltk
from nltk.tokenize import word_tokenize
from nltk.corpus import stopwords
from nltk.stem import WordNetLemmatizer
from nltk.corpus import wordnet

stop_words = stopwords.words('english') # stop words list
lemmatizer = WordNetLemmatizer() # lemmatizer

from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report
```
```python
df = pd.read_csv('spam.csv', encoding = 'latin-1')
```

We brievly explore the data, there 5572 SMS, 87% of which are spams. Only 747 spams for 4825 hams, the datasets it's a quite **unbalanced**.

```python
print(df.shape())
df.Class.value_counts(normalize = True)

df.head(5)
```

![image](https://leoguillaume.github.io/assets/images/2020-10-24-textaugmentationwithglove/screenshot-1.png)

I also encode labels.

```python
def class_processing(x):
    if x == 'ham':
        return 0
    else:
        return 1

df['label'] = df.Class.apply(class_processing)
```

# Text preprocessing

I realize a very classic preprocessing. The steps are: lower case, tokenize, lemmatize, remove non alphabetic words, stop words and words of one caracter.

```python
def get_wordnet_pos(pos_tag):
    output = np.asarray(pos_tag)
    for i in range(len(pos_tag)):
        if pos_tag[i][1].startswith('J'):
            output[i][1] = wordnet.ADJ
        elif pos_tag[i][1].startswith('V'):
            output[i][1] = wordnet.VERB
        elif pos_tag[i][1].startswith('R'):
            output[i][1] = wordnet.ADV
        else:
            output[i][1] = wordnet.NOUN
    return output

def text_preprocessing(text):
    text = text.lower()
    tokens = word_tokenize(text)
    pos_tag = nltk.pos_tag(tokens)
    pos_tag = get_wordnet_pos(pos_tag)  
    tokens = [lemmatizer.lemmatize(t[0], t[1]) for t in pos_tag]
    tokens = [t for t in tokens if t.isalpha()]
    tokens = [t for t in tokens if t not in stop_words]
    tokens = [t for t in tokens if len(t) > 1]
    return tokens

df['token'] = df.Message.apply(text_preprocessing)
```

# Without text augmentation

To make classification I transform texts in bag of words with Sklearn.

```python
X_train, X_test, y_train, y_test = train_test_split(df.token, df.label, test_size = 0.2, random_state = 1, stratify = y)

vec = CountVectorizer(lowercase = False, analyzer = lambda x: x)

def vectorization(train_set, test_set):
    vectorizer = CountVectorizer(analyzer = lambda x: x)
    bow_train = vectorizer.fit_transform(train_set).toarray()
    bow_train = pd.DataFrame(bow_train, columns = vectorizer.get_feature_names())

    bow_test = vectorizer.transform(test_set).toarray()
    bow_test = pd.DataFrame(bow_test, columns = vectorizer.get_feature_names())
    return bow_train, bow_test

bow_train, bow_test = vectorization(X_train, X_test)

lr = LogisticRegression()
lr.fit(bow_train, y_train)
y_pred = lr.predict(bow_test)

print(classification_report(y_test, y_pred))
```

![image](https://leoguillaume.github.io/assets/images/2020-10-24-textaugmentationwithglove/screenshot-2.png)

The score that interest us is the f1-score of spam class (1). The model detect 91% of spams, it's great, but we do better with the same model ?

# Text augmentation

We can try to make the dataset less unbalanced. We need to create new spams ! The naive approach will be to duplicate spam but this may not work very well and may simply generate overfitting.

Instead, we will use the word embeddings to find synonyms. With synonyms we can generate new spams without duplicating the texts, it's a little smarter.

How find synonyms with words embeddings ? If you have two words whose embedding has a very high cosine similarity, you can assume they're synonymous. First of all I download the model from the Glove API.

```python
import gensim.downloader as api
model = api.load("glove-wiki-gigaword-100")
```

I generate new spams by replacing the names in spams with the top-1 most similar word, thank to Glove word embeddings (in terms of cosine similarity). Names can be identified by their POS-tag 'NN' with nltk.pos_tag.

```python
spams = df.token[df.label == 1]
pos_tags = spams.apply(nltk.pos_tag)

new_spams = pos_tags.apply(lambda x: [model.most_similar(t[0], topn = 1)[0][0] if t[1] == 'NN' and t[0] in model.vocab else t[0] for t in x])

X_augmented = X.append(pd.Series(new_spams), ignore_index=True)
y_augmented = y.append(pd.Series(np.ones(len(new_spams))), ignore_index=True)

y_augmented.value_counts(normalize = True)
```

Now we have 76% of spams!

```python
X_train_a, X_test_a, y_train_a, y_test_a = train_test_split(X_augmented, y_augmented, test_size = 0.2, random_state = 1, stratify = y_augmented)

bow_train_a, bow_test_a = vectorization(X_train_a, X_test_a)
lr = LogisticRegression()
lr.fit(bow_train_a, y_train_a)
y_pred_a = lr.predict(bow_test_a)

print(classification_report(y_test_a, y_pred_a))
```

![image](https://leoguillaume.github.io/assets/images/2020-10-24-textaugmentationwithglove/screenshot-2.png)

The new prediction on minority class is better by 3% :rocket:. It's likely that a bit of overfitting contributes to this increase because we have only replaced the names, but it gives an example of the application of data augmentation with Glove.
