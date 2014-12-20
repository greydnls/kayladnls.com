---
title: Intro to Machine Learning: Math and Magic and Power. 
categories:
    - Machine Learning
    - Nerd
use:
    - posts_tags
    - posts_categories
---

Welcome to the first post in a new Machine Learning Series I'll be writing. We'll start from the top, covering what machine learning is at the most basic level. Each post will cover another topic, giving a more in depth view of key concepts and ideas. 

####Machine Learning: What even is it?
Machine learning. What do you think of when you hear that? If you're like most people (or at least like me) you think of SkyNet. Sentient computers that take over the world and enslave all of mankind. 

Really, though, what Machine learning really is: MATH. Math, and magic and a whole lot of power. If you're already having horribly flashbacks to Calculus class, don't run away screaming just yet. Focus more on the "magic" and "power" parts. The math will come, I promise. 

If you spend any time on the internet at all, you probably come into contact with dozens of services a day that use some form of machine learning. Do you use Gmail or a similar service that automatically detects "spam" for you and filters it out of your inbox? Are you on twitter right now, staring at a list of "Suggested" accounts for you to follow? 

Both of those are examples of Machine Learning in action. 

**Textbook Definition: **
>Machine learning is a scientific discipline that explores the construction and study of algorithms that can learn from data.[1]

Machine learning is about understanding data, and drawing conclusions from that data. There is a vast array of tools (algorithms) available to us to help us do that. The magic of these algorithms? They do all the work. 

These algorithms are given a **training dataset** to learn from. Their accuracy is then run against a **test dataset** to confirm that they are performing well. Once that is done, you can feel relatively safe running the algorithm against real world data. 

Think of both the training and test datasets as "past experiences". You're giving your algorithm a set of past experiences and telling it to learn from it. You can then hand it a "new experience", and based on what it has learned, it will predict the outcome for you. 

####What can you do with it?
There are two main types of Machine Learning (also called Statistical Learning): **Supervised** and **Unsupervised**.  I'll explain both breifly, and we'll go into more depth in future posts in this series. 

#####Supervised
Supervised statistical learning methods build a statistical model for predicting or estimating output based on input(s). Within the field of supervised learning, there are two more clasifications: Those algorithms that give continuous,  quantitative output and those that give non-numeric or categorical (qualitative) output. 

A common form of quantitative supervised learning is called **Regression**. 
**Example: **We have a dataset of `WageData` that includes information about the age, education, wage and calendar year of men in a specific area of the country. We can use a regression algorithm to create a model such that, given another man's information, we can accurately predict his wages. 

A common form of qualitative supervised is **Classification**.   
**Example:** By examining stock market data containing daily movements in the S&P 500 over a 5 year period, we are able to predict whether tomorrow's index will *increase* or *decrease*.  (PS: This is very hard to do, so don't get your hopes up that this series will teach you to become a Wall Street bajillionaire.)

#####Unsupervised
Unsupervised methods have input, but no output. Instead, we're trying to learn about the structure of the data, and relationships within that data. In this case, we're not trying to predict or estimate, but observe. 

A common type of Unsupervised learning is called **Clustering**. 
**Example** Given market demographics for customers of our company (age, Annual house hold income, etc) we can analyze the data and find "groupings" or "clusters" within the data. Further analysis of those clusters can help us understand how each group is related to the other. 

So, there you have it. A quick, preliminary rundown of what Machine Learning is. More to come!


> References  
> 1. Glossary of Terms [http://ai.stanford.edu/~ronnyk/glossary.html](http://ai.stanford.edu/~ronnyk/glossary.html)
