---
title:  "Machine Learning fundamentals that every iOS developer needs to know: 1/5 iOS Machine Learning Architecture & Tools"
excerpt: "Introduction of the series about Artificial Intelligince and Machine Learning fundamentals that every iOS developer needs to know."
date:   2021-01-12 06:00:00 +0200
header:
  teaser: /assets/images/posts/ML-fundamentals-that-every-iOS-developer-needs-to-know-architecture-tools-cover.jpg
  overlay_image: /assets/images/posts/ML-fundamentals-that-every-iOS-developer-needs-to-know-architecture-tools-cover.jpg
  overlay_filter: 0.3
---

## iOS Machine Learning Architecture & Tools

In this article most common tools for creating the intellident iOS applications will be presented. However, an article dedicated for each one of them is needed and will be posted as we progress with the **Machine Learning fundamentals that every iOS developer needs to know** series. Let's begin the journey of exploring the Machine Learning world in the iOS by getting to know a bit about the architecture and available tools.

![architecture](https://www.researchgate.net/profile/Alberto_Pacheco3/publication/324728615/figure/fig1/AS:684035428872194@1540098163253/iOS-CoreML-based-Machine-Learning-architecture.ppm)

In the picture, we can see a high-level architecture of how Machine Learning works natively in the iOS apps. For us, as developers, interesting parts are only Core ML and everything above it + Create ML. With knowledge of how to use these frameworks, iOS developer is able to implement extraordinary features. Add **Turi Create** and **coremltools** knowledge to the bag and you are quite dangerous in the iOS world of the Machine Learning and Artificial Intelligence.

### Core ML

Core ML framework is dedicated for accessing and running already pretrained Machine Learning models in the iOS apps with Swift language. Core ML is also a basis for Native domain-specific ML frameworks, like: `Visual`, `Natural Language`, `Speech` and `Sound Analysis`. These frameworks run Machine Learning models under the hood and Core ML is at the center of this. A lot more about these frameworks will be covered in the future article **2/5 Native domain-specific Machine Learning frameworks for iOS developers**.

Besides using the previously mentioned domain-specific ML frameworks, by interacting directy with Core ML developer can run ML models [(that can downloaded)](https://developer.apple.com/machine-learning/models/) directly in the iOS projects. Core ML provides a consistent API to interact with any compatible `.mlmodel` model. Here are the basic steps to make ML model work with Core ML:

- Drag & drop the ML model to the iOS project.
- Initialize the model by it's name `let model = MyModel()` (as you would initialize any class).
- Provide an input with a required format to the model.
- Receive the output (prediction) from the model.

More information about how to use `.mlmodel` models with Core ML will be provided in the article dedicated just for the Core ML: **3/5 How to use a custom Core ML model in the iOS App**

To sum up - Core ML enables at least two really powerfull ways of implementing Machine Learning powered features:

1. Use and enrich functionality of native domain-specific ML frameworks

2. Run the custom ML models

And this covers most of the cases. Most often this is all what is needed in order to implement that super awesome feature that boost the intelligence of the iOS application. But what if developer's ambitiouns are much higher than that? What if the desired feature is so unique that no available Core ML models `.mlmodel` available on the internet fit?

### Use coremltools to convert third-party Machine Learning models to Core ML format

You might end up finding a Machine Learning model that fits the requirements and does exactly what you need, but the problem is the this model is not `.mlmodel` format. Worry no more!

The `coremltools` is a suite of Python scripts that is capable of converting from the most popular Machine Learning models created with deep learning frameworks like TensorFlow, PyTorch, Keras, Caffe as well as classical machine learning frameworks like LIBSVM, scikit-learn, and XGBoost to the `.mlmodel` format. Converting the models is only one of the functionality that `coremltools` provide. The `coremltools` also contains supporting tools for editing and validation of the models.

We will go more in depth of how to use `coremltools` to convert the third-party model to the `.mlmodel` format in the **4/5 Training Machine Learning models for the iOS App with Create ML and Turi Create** article. However, if you are in the urgent need to start using the `coremltools` ASAP - [coremltools documentation](https://coremltools.readme.io/docs/what-are-coreml-tools) is the place you want to hit first!

But what if requirements for implementing a Machine Learning powered feature cannot be met by leveraging any of the already available models available on the internet? Very likely that training a custom Machine Learning model for the iOS application by using the unique data reflecting your app's users is what you need.

### Tools for creating and training Machine Learning models for iOS applications

Dear iOS engineer, prepare to put the ML engineer's hat on and step in the land of actual Machine Learning. With the **Create ML** or **Turi Create** tools the unique Machine Learning models can be created by training them with the data gathered from the users or obtained from other channels. Although this might feel like something new and unconfortable at first - the moment custom model trained by yourself returns intelligent results - the amount of endorphins released by your brains will overcompensate all the previous hustle.

There are many very powerful and flexible frameworks for creating and training Machine Learning models.
