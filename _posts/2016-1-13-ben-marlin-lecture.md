---
layout: post
title: Lecture Notes: Ben Marlin
comments: True
---
It's been a while, but yesterday I attended a great lecture by UMass' Ben Marlin. Ben works on very similar problems to my own research, and his paper on [conditional random fields for morphological analysis of wireless ECG signals](http://openscholar.cs.umass.edu/mlds/files/crf_bcb_paper.pdf) is a great example of how advances in machine learning can work to improve long standing problems in healthcare. The notes aren't perfect, but I've tried to fix them up from their raw form. I am unable to find slides, unfortunately.

## Segmenting and Labeling On-Body Sensor Data Streams with CRFs and Factor Graphs
Two big spaces in this research

Clinical data analytics (ICU EHRs)
mHealth Data Analytics — What we’ll talk about today. This is a broad space, incl. the app and device space like fitness wearables and iPhone apps. Wireless sensors, etc. The interesting this here is that the signals coming in are the same ones that you’ll find in an ICU.

With wearables, we want accurate, real-time, energy efficiency, and non-intrusive sensors. We work with addiction in our lab for example smoking or cocaine use. We also look at eating detection, etc. That may seem silly, but these things tie into ICU monitoring, e.g. pulmonary edema recovery. 

For mobile health, we start with detection and move to prediction, understanding and finally intervening. 

## Current problem framework
Let’s look at the pipeline for these tasks.

At the raw data level: we are looking at quasi-periodic time series data. 

    [Slide: respiration data, one channel]

Then comes segmentation of some sort. This should be unsupervised and adaptive.

    [Slide: segmentations overlaid on raw data, segments are heterogeneous]

Next is labeling these segments. This is basically state of the art, especially making \textbf{independent predictions} for each segmented datum. 

    [Slide: each segment has a color corresponding to a class]

From these segments we want to be able to come up with \textit{activity segments} where a segment represents one action like eating a sandwich or smoking a cigarette.

    [Slide: higher level colored segments, bigger than the individual segments]

## Challenges in Mobile Health
We need these things to be low: cost, power usage, noise, drift, dropout. Obviously this isn’t possible. 

1. Labeled data is very high cost. Not only that but there is limited ecological validity. 
2. Self reporting results in lack of temporal precision and low accuracy
3. The “n=me” problem. Big data doesn’t really solve problems in this space because people are so different. \textbf{With low data volumes, everyone looks different.} Then end up with covariate shift or transfer learning problems.
4. For black boxes the need to infer meaningful model results in medicine is difficult. Model distillation is needed for something like deep learning. Doctors and patients don’t trust a black box.
5. All of this needs to be real time! Model compression is coming back for something like this.

## Case Study — CRFs for Labeling and Segmenting ECG
Motivating factor is detecting cocaine usage. For cocaine users, there are morphological structural changes in the ECG besides just rate increase. For example, the QRS and QT prolongates. The detail changes are specific to this drug and thus allow us to filter out false positives that would result with something like heart rate. Detecting each part of the heart rate is very important but difficult. 

The basic idea behind this technique is to use CRFs for each segment, given a window of features around each potential peak. Sparse coding is used for feature extraction (and feature learning) and then each window’s sparse coding dictionary is the feature representation.

    [Slides: many results slides. accuracy is high, amount of train data required is low, CRF does not have differential recall]

Running out of time, but quick bit about hierarchical segmentation where we jointly label and segment. 

I spoke to Ben after the lecture to talk about transfer learning from various datasets of ECGs. He claims that the sparse coding dictionaries are farily stable and consistant, and doesn't believe that training sparse coding on more complete or noise-free datasets will see a large benefit. We also talked about trying to use the sparse coding coefficients as sequence learning inputs for far-off targets such as disease or outcome prediction. This is something I am considering applying in my own work. He has not tried this, but admits it is an idea worth pursuing. 
