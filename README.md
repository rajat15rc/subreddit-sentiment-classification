# Subreddit Sentiment Classification
Multiclass subreddit sentiment classification using logistic regression, TF-IDF, fastText, parameter tuning, and feature augmentation for imbalanced classes

This repository contains an NLP project on **multiclass sentiment classification for subreddit posts**.

The task is to classify Reddit-style post text into **five sentiment classes** using the **body text** of each post. The project compares several baseline classifiers, addresses a strongly imbalanced label distribution, improves a text-classification baseline through parameter tuning, and then further improves performance by adding carefully chosen non-text features.

## Overview

Reddit consists of user-generated threads and posts covering a wide range of topics and tones. Automatically identifying the sentiment of these posts is a useful but challenging classification problem, especially when the class distribution is highly imbalanced.

This project focuses on:
- classifying subreddit posts into **five sentiment classes**,
- comparing standard baseline classifiers,
- selecting an appropriate evaluation metric for imbalanced data,
- improving the baseline through parameter optimisation,
- and reducing errors further through feature addition.

## Why this project matters

This is not just a basic sentiment-classification exercise. The project is important because it deals with a common real-world NLP difficulty:

- **high class imbalance**, where rare classes can easily be ignored by a classifier,
- and **minority-class false negatives**, which can be especially harmful in sentiment tasks.

Instead of stopping at a standard bag-of-words baseline, this project examines:
- which classifiers perform best under imbalance,
- how parameter tuning changes the trade-off,
- and how additional features can improve minority-class behaviour.

## Problem setting

The dataset was split into:
- **training**
- **validation**
- **test**

using a ratio of:

- **63 : 16 : 21**

A key challenge in the data is **class imbalance**:
- the rarest class (`very negative`) makes up only about **0.2%** in one of the sets,
- while the `neutral` class makes up about **63%**.

This makes the task harder because a model can appear strong overall while still performing poorly on rare classes.

## Main objective

The main objective of the project was to build a sentiment-classification pipeline for subreddit posts that performs well not only on common classes, but also more reliably on rare classes.

Because of the imbalanced setting, **Weighted F1** was used as the primary comparison metric.

## Models compared

The project evaluates six classifiers:

1. **Dummy Classifier – Most Frequent**
2. **Dummy Classifier – Stratified**
3. **Logistic Regression with One-Hot Vectorization**
4. **Logistic Regression with TF-IDF Vectorization**
5. **Support Vector Classifier (SVC)**
6. **fastText**

## Baseline findings

The initial comparison showed:

- the two dummy classifiers performed worst, as expected,
- **Logistic Regression with One-Hot vectorization** performed best among the initial baseline models,
- **fastText** performed efficiently and competitively, but still fell short of the strongest logistic-regression baseline without further tuning.

The best baseline **test weighted F1** reported in the project was approximately:

- **0.7273** for **Logistic Regression with One-Hot vectorization**

This made it the strongest baseline reference point in the early phase of the study.

## Parameter optimisation

After the baseline comparison, the project improved the **TF-IDF Logistic Regression** model through parameter tuning.

To make the tuning stage more robust:
- the **training and validation data were combined**,
- and **Grid Search CV** was used.

The tuned parameters included:

- **C = 10**
- **sublinear_tf = True**
- **max_features = 5000**
- **solver = saga**

The scoring method used during tuning was **Weighted F1**, because the project aimed to improve both precision and recall under class imbalance.

### Effect of tuning
After optimisation:
- **Weighted F1 increased from about 0.73 to about 0.76**

However, the report also notes that rare-class recall was still weak, meaning false negatives remained a major issue.

## Feature addition

The strongest improvement in the project came from adding two informative features to the tuned text model:

1. **`sentiment.subjectivity`**
2. **`majority_type`**

### Why these features were added

The reasoning was:

- **subjectivity** helps distinguish emotionally loaded text from more neutral-looking text,
- **post type** helps avoid cases where the tone or style of the post causes the model to misread sentiment.

This is an important part of the project, because it shows that sentiment classification was improved not only by tuning the text pipeline, but by thinking carefully about what extra information affects sentiment interpretation.

## Final results

After adding the extra features to the tuned baseline model, the final model achieved:

- **Weighted Precision:** 0.797067
- **Weighted Recall:** 0.804532
- **Accuracy:** 0.804532
- **Weighted F1:** **0.799006**

This is the strongest result reported in the project.

## Why the final result is meaningful

The project is significant because the final model did more than improve one headline metric.

It also:
- reduced false negatives in the minority classes,
- improved the recall of the rare `very negative` class,
- and produced a more stable overall model.

The report specifically notes that:
- the rare **very negative** class achieved a recall **greater than 0.4** after feature addition,
- and false negatives for that class were **severely reduced** compared with the earlier model.

That is one of the most important outcomes of the whole project, because it shows the model became more useful for difficult, low-frequency sentiment classes rather than only improving performance on the dominant neutral class.

## Repository contents

This repository includes:
- the main notebook for model development and evaluation,
- the accompanying report describing the methodology and findings.

## What this project demonstrates

This project demonstrates:
- text classification with multiple baselines,
- evaluation under class imbalance,
- vectorization choices for NLP,
- parameter tuning with Grid Search,
- feature engineering beyond pure text features,
- and error analysis focused on minority-class behaviour.

## Key takeaway

The main lesson from this project is that **careful feature design can materially improve sentiment classification under imbalance**.

A standard text classifier can perform reasonably well, but adding features that reflect:
- how subjective the text is,
- and what kind of post it is,

can significantly improve the model’s usefulness, especially for underrepresented sentiment classes.

## Suggested future improvements

The report suggests that the model could be improved further through better preprocessing of the text body, especially by removing noisy content such as:
- URLs
- and other non-linguistic artifacts

Additional future improvements could include:
- class rebalancing strategies,
- stronger error analysis by class,
- and experiments with more advanced text representations.

## Suggested GitHub description

**.**

## Suggested topics

`nlp` `sentiment-analysis` `text-classification` `reddit` `subreddit` `logistic-regression` `fasttext` `imbalanced-data`
