---
layout: single
title: “[Fr] Introduction au NLP #1"
excerpt: “Prétraitement du texte"
categories:
 - nlp
header:
 teaser: https://leoguillaume.github.io/assets/images/-nlpintroduction1/teaser.jpg
read_time: true
author_profile: true
toc: true
share: true
tags:
 - python
 - course
 - nltk
 - regex
comments: true
---

*Ce post est la première partie d'une serie de post en français consacrée à introduire le NLP sous python.*

# Qu'est ce que le NLP ?

Le Traitement Automatique du Language (TAL), ou Natural Language Processing (NLP) en anglais, est le domaine des data sciences qui s'interesse au traitement des langue naturelles.

Les applications du NLP aujourd'hui sont très nombreuses : traduction, reconnaissance vocale, résumer un texte, extraire le sujet d'un texte, analyse de sentiments, l'analyse gramaticale... Vous rencontrez chaque jour ces applications avec Google Traduction, les suggestion de réponse de Gmail ou encore lorsque vous utilisez une enceinte connectée.

## Des données textuelles

Concrètement ces applications ne font qu'utiliser les aglorithmes de machine ou deep learning standards en les soumettant à des données particulières : des textes.

:triangular_flag_on_post: Faisons un petit point de terminologie. En NLP, en général une base de donnée est appelé **un corpus**. Elle contient une colonne où chaque observation est un texte. Un observation est appelé **un document**. Ces derniers peuvent être un mot, une phrase ou encore un texte de plusieurs phrases. Un mot en NLP est appelé **un token**.

![image](https://leoguillaume.github.io/assets/images/2020-10-24-textaugmentationwithglove/screenshot-1.png)

Comme pour tout problème de machine learning la première étape est le prétraitement des données. En effet, lorsque l'on fait face à des données numériques, il convient de traiter les problèmes de colinéarité, de normaliser les données, de remplacer les valeurs manquantes, etc. Lorsque les données sont des textes l'idée est la même avec toutefois des méthodes différentes étant donnée la nature des données.

De plus, les algorithmes de machine learning prennent en entrer des nombres, ici nos données sont sous forme de strings. Ainsi prétraiter les données revient à répondre à deux questions :
- comment extraire l'information dans le texte qui va me donner le sens du texte ?
- comment transformer le texte en nombre tout en gardant le sens du texte ?

Nous répondrons à cette seconde question dans le prochain posts. Pour le moment nous allons voir comment sous python prétraiter un texte avec des librairies dédiées.

# Prétraiter des données textuelles

Pour prétraiter du texte sous python, deux librairies sont principalement utilisées : [NLTK](https://www.nltk.org/) et [spaCy](https://spacy.io/). La première étant connue pour être davantage dédiée à la recherche et offrant plus flexibilité, la seconde axée sur la mise la production et offrant plus facile d'utilisation et de robustée. Nous allons ici présenter les principales étapes nécessaires au prétraitement avec ces deux librairies.

NB: nous utiliserons ici des exemples en anglais puisque ces librairies étant implémentée par défaut pour l'anglais, elles proposent toutefois des variantes pour traiter le français.

## NLTK

```bash
pip install nltk
```

# Tokenization

La tokenization est simplement le fait de découper un texte en mots, c'est-à-dire en token. La méthode la plus simple pour ce faire est d'utiliser la méthode python `str.split()`.

```python
document = "I'm in the kitchen. Bryan is joining me."
tokens = document.split(' ')
print(tokens)
```
Output:
```bash
["I'm", 'in', 'the', 'kitchen.', 'Bryan', 'is', 'joining', 'me.']
```
