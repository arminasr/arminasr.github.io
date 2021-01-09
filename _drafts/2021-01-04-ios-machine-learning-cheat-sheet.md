---
title:  "Introduction to AI/ML for iOS, iPadOS & macOS developers"
excerpt: "Artificial Intelligince and Machine Learning fundamentals that every iOS, iPadOS & macOS developer needs to know"
date:   2021-01-04 15:50:00 +0200
header:
  teaser: /assets/images/new-year.jpg
  overlay_image: /assets/images/new-year.jpg
---

## iOS ❤️ Machine Learning

Sometimes ML is perceived as a super complicated topic, requiring deep knowledge of various algorithms and math. While it is true on the academic level (to understand scientific papers one might need such knowledge), it doesn't always have to be complicated on the practical level. Our goal is to create intelligent applications, not improve the performance of the state of the art algorithms (leave this task for scientists working at Universities across the world or smart geniuses at Apple, Google, etc.). And in fact, such a goal sometimes can be achieved quite easily.

The purpose of this article is to introduce the reader to different ways of leveraging the power of Machine Learning models in iOS apps. Let's start by understanding a high-level architecture of how Machine Learning in iOS works in general.

## iOS Machine Learning Architecture & tools

![architecture](https://www.researchgate.net/profile/Alberto_Pacheco3/publication/324728615/figure/fig1/AS:684035428872194@1540098163253/iOS-CoreML-based-Machine-Learning-architecture.ppm)

In the picture, we can see a high-level architecture of how Machine learning works natively in the iOS apps. For us, as developers, interesting parts are only Core ML and everything above it + CreateML. With knowledge of how to use these frameworks, iOS developer can call herself/himself dangerous in the iOS world of artificial intelligence.

![levels](https://i.imgflip.com/4shzs9.jpg)/assets/images/new-year.jpg

### Native Apple iOS frameworks powered by ML

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

## Custom Machine Learning models in iOS apps

In the previous chapter the frameworks (provided by Apple) for creating artificially intelligent iOS applications were introduced. However, in some cases developer might want to implement Machine Learning powered features that these framework do not provide. This chapter introduces ways to create and use custom Machine Learning models that will take iOS applications to the next level.

### Find, download & use already trained models

There is a vast amount of already trained models that are publicly available and ready to be used. All that is needed is to find, download & integrate them in your application, simple as that 🚀. Here is the list of suggested places to look for the models:

- [The official Apple website](https://developer.apple.com/machine-learning/models/)
  
  Machine Learning models are already in Core ML format, (which is `.mlmodel`) and could be immediately used in your iOS application.

- [Awesome Core ML Models repo](https://github.com/likedan/Awesome-CoreML-Models)

> the largest collection of machine learning models in Core ML format, to help iOS, macOS, tvOS, and watchOS developers experiment with machine learning techniques.

### Usage of Core ML format models `.mlmodel`

It is quite simple to use the models that are already in `.mlmodel` format. Let's go through the example of using `SqueezeNet Image Classification model` that classifies the dominant object in a camera frame or image. The example code is written in the Playgrounds project and [can be found here](https://github.com/arminasr/arminasr.github.io-playgrounds/tree/master/SqueezeNetPlayground/SqueezeNetPlayground.playground).

First thing that we need to do - [download](https://ml-assets.apple.com/coreml/models/Image/ObjectDetection/YOLOv3Tiny/YOLOv3Tiny.mlmodel), drag and drop the model into the project.
![squeezeNetInfo](/assets/images/posts/squeezeNetInfo.png)
By selecting the imported model we immedietely get some useful information about it, like what are the input and output types and interesting metadata.

Besides using some `UIImage` extensions (thanks [@francoismarceau29](https://gist.github.com/francoismarceau29/abac55c22f6e440800d1d73d72bf2225#file-uiimage-cvpixelbuffer-swift)) for formatting the image to meet input requirements, this is all the code needed to get predictions from the model:

```swift
import CoreML
import UIKit

func getPredictions(for image: UIImage) {
    let errorMessage = "Could not predict with a given picture"
    // 1. Initialize the SqueezeNet model
    guard let model = try? SqueezeNet(configuration: MLModelConfiguration()),
          // 2. Resize image & convert to CVPixelBuffer to meet the input requirements
          let resizedImage = image.resize(to: CGSize(width: 227, height: 227)),
          let buffer = resizedImage.toCVPixelBuffer(),
          // 3. Get predictions 🚀
          let predictions = try? model.prediction(image: buffer).classLabelProbs else {
        print(errorMessage)
        return
    }

    let sortedPredictions = predictions.sorted { $0.value > $1.value }
    sortedPredictions.forEach {
        print("\(String(format: "%.1f", $0.value * 100))% probability: \($0.key)")
    }
}

if let image = UIImage(named: "myCatPic.jpg") {
    getPredictions(for: image)
}
```

1. The SqueezeNet model is initialized by simply accesing it via model's name.
2. SqueezeNet model expects the input of the image which size is 227 x 227px. Also it must be converted to a `CVPixelBuffer` format.
3. Receive predictions from the model by calling `model.prediction(...)` method.
4. Profit!

![My Cat](/assets/images/posts/myCatPic.jpg)

After passing the picture of my cat to the model, I learned that my cat is "tabby cat", because it has 'M' shaped marking on its forehead.

```
48.4% probability: tabby, tabby cat
29.6% probability: Egyptian cat
16.9% probability: tiger cat
2.9% probability: Persian cat
1.9% probability: lynx, catamount
0.2% probability: wood rabbit, cottontail, cottontail rabbit
```

Sweet!

### (Hard) Train models yourself
