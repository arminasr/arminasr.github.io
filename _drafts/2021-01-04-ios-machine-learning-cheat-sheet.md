---
title:  "iOS Machine Learning Cheat Sheet"
excerpt: "3 ways to incorporate Machine Learning into iOS apps"
date:   2021-01-04 15:50:00 +0200
header:
  teaser: /assets/images/new-year.jpg
  overlay_image: /assets/images/new-year.jpg
---

## iOS ❤️ Machine Learning

Sometimes ML is perceived as a super complicated topic, requiring deep knowledge of various algorithms and math. While it is true on the academic level (to understand scientific papers one might need such knowledge), it doesn't always have to be complicated on the practical level. Our goal is to create intelligent applications, not improve performance of the state of the art algorithms (leave this task for scientists working at Universities across the world or smart geniouses at Apple, Google, etc.). And in fact such a goal sometimes can be achieved quite easily.

The purpose of this article is to introduce reader to different ways of leveraging the power of Machine Learning models in iOS apps. Let's start by understanding the high level architecture of how Machine Learning in iOS works in general.

## Native iOS Machine Learning Tools and Architecture
![architecture](https://www.researchgate.net/profile/Alberto_Pacheco3/publication/324728615/figure/fig1/AS:684035428872194@1540098163253/iOS-CoreML-based-Machine-Learning-architecture.ppm)

In the picture we can see a high level architecture of how Machine learning works natively in the iOS apps. For us as developers it is interesting only CoreML and everything above it + CreateML. With knowledge how to use such frameworks iOS developer can call herself/himself dangerous in the iOS world of artificial intelligence.

![levels](https://i.imgflip.com/4shzs9.jpg)

### Native iOS frameworks powered with ML

Apple provides frameworks that are powered by machine learning models under the hood. It is easy to use them and we might have already used them without thinking about the complexity of ML. Let's go through the explanation of each framework and see if it could make our beloved apps that we are working on more intelligent.

- Visual
  
  As the name of the framework suggests - it's purpose is to perform a variety of tasks on input images and video. Some of the ideas of what Vision is capable of:
  - Barcode Detection
  - Image Classification, Saliency & Alignment
  - Image Similarity
  - Object Detection
  - Moving Object Tracking in Video
  - Trajectory Detection of Moving Object in Video
  - Contour Detection
  - Text Detection & Recognition
  - Face Detection & Tracking
  - Face Landmarks
  - Human Body Detection
  - Body Pose
  - Hand Pose
  - Animal Recognition
  
  And that is not it. If you are interested in using Vision - there is no better place to start than the [official Vision documentation](https://developer.apple.com/documentation/vision).

- Natural Language
  
  Whenever you work with text and want to introduce some intelligence - the Natural Language framework should be your first option. Sometimes it can provide amazing results with very little effort. Natural Language main features:
  - Language detection
  - Sentiment Analysis
  - Word & Sentence Embedding
  - Tokenization

  Automatically detecting and preselecting language from user's text input is small but nice detail and things like that are super simple to implement using Natural Language framework. Wether goal is simple or more complex - [documentation always helps](https://developer.apple.com/documentation/naturallanguage).
- Speech
- Sound Analysis

### (Medium) Download already trained models and use with CreateML

### (Hard) Train models yourself
