---
title: "Machine Learning Tips"
author: Zhang Keke
date: 2018-02-23
categories:
  - MACHINE LEARNING
  - READING
tags:
  - Tips
---


Recap of Martin Zinkevich's blog 
[Best Practices for ML Engineering](http://martin.zinkevich.org/rules_of_ml/rules_of_ml.pdf)

---

### Before Machine Learning 

```
Do machine learning like the great engineer you are, not like the expert you aren't.
```

> Machine learning is all of Engineering.
ML is limited, but engineering is not. 
Engineering's destiny is to quantify problems then solve it. In this case, the first target is how to quantify problems --- Design metrics.

* 1: Don’t be afraid to launch a product without machine learning.
* 2: Make metrics design and implementation a priority.
* 3: Choose machine learning over a complex heuristic.
### ML Phase I: Your First Pipeline
* 4: Keep the first model simple and get the infrastructure right. 
* 5: Test the infrastructure independently from the machine learning. 
* 6: Be careful about dropped data when copying pipelines.
* 7: Turn heuristics into features, or handle them externally.
> stand on giant's shoulders

### Monitoring
* 8: Know the freshness requirements of your system.
> How fast you will lost revenue with time goes by.How open you should update your model

* 9: Detect problems before exporting models.
* 10: Watch for silent failures.
> Track statistics of Data, before preprocessing and feeds 

* 11: Give feature sets owners and documentation.
### Your First Objective
* 12: Don’t overthink which objective you choose to directly optimize. 
* 13: Choose a simple, observable and attributable metric for your first objective.

* 14: Starting with an interpretable model makes debugging easier. 

* 15: Separate Spam Filtering and Quality Ranking in a Policy Layer.
### ML Phase II: Feature Engineering
* 16: Plan to launch and iterate.
* 17: Start with directly observed and reported features as opposed to learned features.
                          
* 18: Explore with features of content that generalize across contexts. 
* 19: Use very specific features when you can.
* 20: Combine and modify existing features to create new features in human understandable ways.
* 21: The number of feature weights you can learn in a linear model is roughly proportional to the amount of data you have.
* 22: Clean up features you are no longer using.
> Unused features create technical debt

###  Human Analysis of the System
* 23: You are not a typical end user.
* 24: Measure the delta between models.
* 25: When choosing models, utilitarian performance trumps predictive power.
* 26: Look for patterns in the measured errors, and create new features.
* 27: Try to quantify observed undesirable behavior.
> Quantify bad part and improve it. Again, Metric is the first important thing
At this point, they should do whatever it takes to turn their gripes into solid numbers.

* 28: Be aware that identical short term behavior does not imply identical long term behavior.
### Training-Serving Skew
> The best solution is to explicitly monitor it so that system and  data changes don't introduce skew unnoticed.

* 29: The best way to make sure that you train like you serve is to save the set of features used at serving time, and then pipe those features to a log to use them at training time.
* 30: Importance weight sampled data, don’t arbitrarily drop it!
* 31: Beware that if you join data from a table at training and serving time, the data in the table may change.
* 32: Reuse code between your training pipeline and your serving pipeline whenever possible.
* 33: If you produce a model based on the data until January 5th, test the model on the data from January 6th and after.
> use next-day data

* 34: In binary classification for filtering (such as spam detection or determining interesting emails), make small short term sacrifices in performance for very clean data.
* 35: Beware of the inherent skew in ranking problems.
* 36: Avoid feedback loops with positional features.
* 37: Measure Training/Serving Skew.
> Training data, validation data, test data(next data), live data.

### ML Phase III: Slowed Growth, Optimization Refinement, and Complex Models
* 38: Don’t waste time on new features if unaligned objectives have become the issue.
* 39: Launch decisions will depend upon more than one metric.
* 40: Keep ensembles simple.
* 41: When performance plateaus, look for qualitatively new sources of information to add rather than refining existing signals.
* 42: Don’t expect diversity, personalization, or relevance to be as correlated with popularity as you think they are.
* 43: Your friends tend to be the same across different products. Your interests tend not to be.