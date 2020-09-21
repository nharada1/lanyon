---
layout: post
title: The ML Design Interview 
comments: True
---
*Disclaimer: This article is how I advise personal friends to prepare for ML interviews. There is nothing in here specific to my current company, and you shouldn't assume any advice here is endorsed or supported by them.*

### A Practical Approach to Solving an ML Design Problem
Design problems can be scary parts of an interview, especially for early career engineers who are familiar with coding questions and may have not experienced a design interview. I advise anyone tackling an open ended ML problem to take a **structured approach** -- and this means both in their jobs and during a design interview. The approach here is a bit biased towards my particular domain of ML, which is deep learning heavy and often runs on robots or custom hardware, but most of this applies no matter what you're working on.

### Design a system

The most important thing to remember when being asked to design a system is that **you do not have enough information**. If your boss asked you to design Facebook's news recommendation system you wouldn't go off and build it without clearing up a *lot* of details. Similarly, a design interview should be a conversation with the interviewer.

### A structured approach
**Prompt:** Design a system to detect if a person is angry.

#### Stage 1: Understand the problem
* What is the use case?
    * How will this be used in the wild?
* What formulation do we want to put this problem in?
    * Is this an object detection problem? Classification?
* What details matter?
    * Do we need to deal with multiple people?
    * Does it need to be very fast?
    * What hardware is this running on? GPU? Microcontroller?
    * What accuracy/precision/recall tradeoffs matter?
    * What about lighting conditions? Occlusion?
* What are the pros/cons of the formulation you've picked?
* Are there any existing implementations?

#### Stage 2: Data & Metrics
* Data
    * What does our data look like?
    * How should the data be structured?
    * How do we label our data if this is a supervised task?
    * What kind of variety do we need?
    * How do we check label quality?
    * How can we improve the labeling process?
    * How do we split our data?
    * What's the right order to feed the data?
* Metrics
    * What is success?
    * What are the traditional metrics for this task?
    * How many metrics might we need? Do we need a metrics hierarchy?
    * What metrics might lie to us?
    * What modifications might we need to existing metrics?
    * How do we baseline our performance?

#### Stage 3: The Model
* Model Architecture
    * What kind of input representations might make sense?
    * What is our target output and loss function?
    * What architectures make sense?
* Training and Tuning
    * How do we do the training? Which optimizer?
    * Do we need to do any transfer learning?
    * Do we need to employ tricks like negative sampling?
    * What kind of hyperparameters actually matter?
* Model Debugging
    * How can we break down the model to simple parts to make sure those work?
    * What kind of visualizations do we want?
    * How can we know if we're overfitting or underfitting?

#### Stage 4: Operations 
* Deployment
    * What will the deployment look like?
    * What are the deployment constraints -- latency? memory? compute?
    * Does this model need specialized hardware (e.g. GPU)?
    * What happens if we need to scale up more than expected?
    * Do we need to refresh the data? How often?
    * What conditions might require a data refresh sooner than expected?
* Monitoring
    * How can we know our model is acting correctly once deployed?
    * Is there a way to collect metrics during deployment?
    * Alarms for issues that may crop up?


#### Stage 5: Making Improvements 
* Iteration
    * How can we improve the model once it's deployed?
    * What kind of error analyses can we do?
    * Are there any representation issues that mean the model cannot learn certain things?
    * Can we use the model to improve itself (active learning)?
    * How can we make improvements without causing regressions?
    * Is this model like any others we have already? Can we merge them to improve generalization?

### During the interview
The list above is huge and still only a subset of the things that matter when designing an ML system. During an interview, you can skip entire pieces of this if you think they don't matter, or are implied by the question, or just to save on time. Again, remember the important thing is to gather information and use that to ultimately build a system with the right trade-offs and qualities. 
