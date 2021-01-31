---
title:  "Machine Learning fundamentals that every iOS developer needs to know: 1/5 iOS Machine Learning Architecture & Tools"
excerpt: "Introduction to Machine Learning Architecture & Tools for iOS development. Bonus - iOS Machine Learning Tools Cheat-Sheet."
date:   2021-01-17 06:00:00 +0200
toc: true
header:
  teaser: /assets/images/posts/ML-fundamentals-that-every-iOS-developer-needs-to-know-architecture-tools-cover.jpg
  overlay_image: /assets/images/posts/ML-fundamentals-that-every-iOS-developer-needs-to-know-architecture-tools-cover.jpg
  overlay_filter: 0.3
---

## iOS Machine Learning Architecture & Tools

In this article, the most common tools for creating intelligent iOS applications will be presented. However, a separate article dedicated to each one of the tools is needed and will be posted as we progress with the **Machine Learning fundamentals that every iOS developer needs to know** series. Let's begin the journey of exploring the Machine Learning world in iOS by getting to know a bit about the architecture and available tools.

![iOS Machine Learning Architecture](/assets/images/posts/ios-ml-architecture.jpeg)

In the picture, we can see a high-level architecture of how Machine Learning works natively in iOS apps. For us, as developers, interesting parts are only Core ML and everything above it + Create ML. With the knowledge of how to use these frameworks, iOS developers can implement extraordinary features. Add **Turi Create** and **coremltools** knowledge to the bag and you are quite dangerous in the iOS world of Machine Learning and Artificial Intelligence.

### Core ML

Core ML framework is dedicated to accessing and running already pre-trained Machine Learning models in the iOS apps with Swift language. Core ML is also a basis for native domain-specific ML frameworks, like `Visual`, `Natural Language`, `Speech` and `Sound Analysis`. These frameworks run Machine Learning models under the hood and Core ML is at the center of this. A lot more about these frameworks are covered in the next article [**2/5 Native domain-specific Machine Learning frameworks for iOS developers**](/ML-fundamentals-that-every-iOS-developer-needs-to-know-2-5-Native-domain-specific-ML-frameworks-for-iOS-developers){:target="_blank"}.

Besides using the previously mentioned domain-specific ML frameworks, by interacting directly with Core ML developers can run ML models [(that can be downloaded here)](https://developer.apple.com/machine-learning/models/){:target="_blank"} directly in the iOS projects. Core ML provides a consistent API to interact with any compatible `.mlmodel` model. Here are the basic steps to make the Machine Learning model work with Core ML:

- Drag & drop the ML model to the iOS project.
- Initialize the model by its name `let model = MyModel()` (as you would initialize any class).
- Provide input with a required format to the model.
- Receive the output (prediction) from the model.

More information about how to use `.mlmodel` models with Core ML will be provided in the article dedicated just for the Core ML: [**3/5 How to use a custom Core ML model in the iOS App**](/ML-fundamentals-that-every-iOS-developer-needs-to-know-3-5-How-to-use-a-custom-CoreML-model-in-the-iOS-App){:target="_blank"}

To sum up - Core ML enables at least two powerful ways of implementing Machine Learning powered features:

1. Use and enrich the functionality of native domain-specific ML frameworks

2. Run the custom ML models

Either using native domain-specific ML-powered frameworks or running the custom ML models cover most of the cases when the iOS developer needs to interact with ML. Most often this is all that is needed to implement that super awesome feature that boosts the intelligence of the iOS application. But what if the developer's ambitions are much higher than that? What if the desired feature is so unique that no available Core ML models `.mlmodel` available on the internet fit?

### Converting third-party Machine Learning models to Core ML format

You might end up finding a Machine Learning model that fits the requirements and does exactly what you need, but the problem is this model is not in `.mlmodel` format. Worry no more!

The `coremltools` is a suite of Python scripts that is capable of converting from the most popular Machine Learning models created with deep learning frameworks like TensorFlow, PyTorch, Keras, Caffe as well as classical machine learning frameworks like LIBSVM, scikit-learn, and XGBoost to the `.mlmodel` format. Converting the models is only one of the functionality that `coremltools` provide. The `coremltools` also contains supporting tools for editing and validation of the models.

We will go more in the depth on how to use `coremltools` to convert the third-party model to the `.mlmodel` format in the **5/5 How to run any Machine Learning model in the iOS App** article. However, if you are in the urgent need to start using the `coremltools` ASAP - [coremltools documentation](https://coremltools.readme.io/docs/what-are-coreml-tools){:target="_blank"} is the place you want to hit first!

But what if requirements for implementing a Machine Learning powered feature cannot be met by leveraging any of the already available models found on the internet? Very likely that training a custom Machine Learning model by using the unique data reflecting your app's users is what you need.

### Creating and Training custom Machine Learning models for iOS applications

Dear iOS engineer, prepare to put the ML engineer's hat on and step into the land of actual Machine Learning. With the **Create ML** or **Turi Create** tools the unique Machine Learning models can be created by training them with the data gathered from the users or obtained from other channels. Although this might feel like something new and uncomfortable at first - the moment a custom model trained by yourself returns intelligent results - the number of endorphins released by your brains will overcompensate all the previous hustle.

There are many very powerful and flexible frameworks for creating and training Machine Learning models. We will focus only on frameworks provided by Apple. There are two of them:

1. Create ML

    Create ML comes as two separate components - a Create ML macOS App and a Create ML framework. Both of them have very similar functionality. The main difference is that the Create ML macOS App provides an easy to use graphical interface:

    ![Create ML macOS Application](/assets/images/posts/create-ml-app.jpg)

    When creating and training a model with the Create ML framework you rely on writing code. Almost all the same could be achieved no matter which way we go. Here are the features supported by Create ML as of the time of writing:

    - Images
      - Image classification
      - Object detection
      - Style transfer
    - Video
      - Action classification
      - Style transfer
    - Motion
      - Activity classification
    - Sound
      - Sound classification
    - Text
      - Text classification
      - Word tagging
    - Tabular
      - Tabular classification
      - Tabular regression
      - Recommendation

    Create ML is available only on the macOS, which means that models need to be created and trained on your machine and imported to the iOS project. Creating and training models from scratch in the iOS app is not possible as hardware is still not there. Hopefully, it will change soon. However, some specific kinds of models can be updated with on-device training, but it is not a straightforward process and this topic will be covered in future articles.

2. Turi Create

    Initially, Turi Create was created by a startup called "Turi". Apple acquired this startup in 2016 and open-sourced its software. Turi Create is a Python package. Yes, you heard it right - Python. But don't get scared, it is easy to use and a very powerful tool. More accurate would be to call it not a tool, but a collection of task-based tools. Here are what tasks and features can be created with it:

      - Recommender Systems
      - Image Classification
      - Drawing Classification
      - Sound Classification
      - Image Similarity
      - Object Detection
      - One-Shot Object Detection
      - Style Transfer
      - Activity Classifier
      - Text Classifier

    Although much of the capabilities are very similar to what Create ML does - Turi Create is much more flexible. It is possible to select specific algorithms for each problem.

    Besides creating and training Machine Learning models and exporting them to the Core ML format, Create ML offers other very important features. You will be surprised, but when working on Machine Learning tasks, very often most of the time is spent on working with data, not creating and training the models. Turi Create provides tools for working with data and visualizing it which is super important.

    The more in-depth information and actual examples of using both Create ML and Turi Create tools will be covered in the **4/5 Training Machine Learning models for the iOS App with Create ML and Turi Create** article.

## (Bonus) iOS Machine Learning Tools Cheat-Sheet

There are quite some tools available for implementing cool Machine Learning powered features. Here I [provide a cheat-sheet](/assets/images/posts/ios-ml-tools-cheat-sheet.jpeg){:target="_blank"} that I believe should help to select the tools in a way that is the simplest and most efficient for iOS developers comfortable with Swift language and the Apple development world.

![iOS Machine Learning Tools cheat-sheet](/assets/images/posts/ios-ml-tools-cheat-sheet.jpeg)

I'd love to hear your opinion about it. Feel free to open the discussion in the comments and share what you think!
