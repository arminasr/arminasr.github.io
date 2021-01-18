---
title:  "Machine Learning fundamentals that every iOS developer needs to know: 2/5 Native domain-specific Machine Learning frameworks for iOS developers"
excerpt: "Introduction of the series about Artificial Intelligince and Machine Learning fundamentals that every iOS developer needs to know."
date:   2021-01-18 06:00:00 +0200
header:
  teaser: /assets/images/posts/ML-fundamentals-that-every-iOS-developer-needs-to-know-architecture-tools-cover.jpg
  overlay_image: /assets/images/posts/ML-fundamentals-that-every-iOS-developer-needs-to-know-Native-domain-specific-frameworks-cover.jpg
  overlay_filter: 0.3
---

## Native Apple iOS frameworks powered by ML

Apple provides frameworks that are powered by machine learning models under the hood. It is easy to use them and we might have already used them without thinking about the complexity of ML. Let's go through the explanation of each framework and see if it could make the beloved apps that we are working on even more intelligent.

- Visual
  
  As the name of the framework suggests - its purpose is to perform a variety of tasks on input images and video. Some of the ideas of what Vision is capable of:
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
  
  Whenever you work with text and want to introduce some intelligence - the Natural Language framework should be your first choise. Sometimes it can provide amazing results with very little effort. Natural Language main features:
  - Language detection
  - Sentiment Analysis
  - Word & Sentence Embedding
  - Tokenization

  Automatically detecting and preselecting language from a user's text input is small but nice detail and things like that are super simple to implement using the Natural Language framework. Whether a goal is simple or more complex - [documentation always helps](https://developer.apple.com/documentation/naturallanguage).
- Speech
  
  Thinking about implementing speech recognition into your iOS app? Speech framework is all you need to automatically generate transcripts, alternative interpretations, and confidence levels of the results from live or prerecorded audio. Combine Speech capabilities with Natural Language and sky is the limit of what can be achieved. With the help of [Documentation of the Speech framework](https://developer.apple.com/documentation/speech) speech recognition in the iOS app will be implemented in no time.
- Sound Analysis

  [Sound Analysis framework](https://developer.apple.com/documentation/soundanalysis) is dedicated to help you analyze and clasify sound. The main power of Sound Analysis framework is utylised when you already have a custom Core ML sound classification model. Such models could be downloaded or you can train it yourself using CreateML or other technologies.
  
  Do you feel amazed when auto mechanic diagnoses the problem in your car just by listening and recognizing the specific noise coming from the the engine? Well, now we have tools to make an app that is capable of doing that.
