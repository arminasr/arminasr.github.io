---
title:  "Machine Learning fundamentals that every iOS developer needs to know: 5/5 How to run any Machine Learning model in the iOS App"
excerpt: "The last article of the series introduces coremltools - a suite of scripts for converting Machine Learning models to Core ML acceptable format."
date:   2021-01-14 12:00:00 +0200
toc: true
header:
  teaser: /assets/images/posts/How-to-run-any-Machine-Learning-model-in-the-iOS-App-cover.jpg
  overlay_image: /assets/images/posts/How-to-run-any-Machine-Learning-model-in-the-iOS-App-cover.jpg
  overlay_filter: 0.3
---

## Different Machine Learning models formats

In the previous articles, we learned to train and run only machine Learning models format that is supported by the Core ML. Sadly, the most popular Machine Learning platforms and frameworks are not in the ecosystem of Apple, meaning those models are not supported by the Core ML. There are hundreds or thousands of already pre-trained models that would fit our needs, the problem is that iOS developers cannot run them in the apps. But can't they?

There is a big chance that machine learning models trained with one of the most popular frameworks, like `TensorFlow`, `PyTorch`, `Keras`, `Caffe` as well as classical machine learning frameworks like `LIBSVM`, `scikit-learn`, and `XGBoost` are convertible to the `.mlmodel` format. Even Core ML models featured on the Apple website are converted from some of the previously listed formats. A huge list of Core ML models that are converted from other formats and are ready to be used in the iOS applications can be found in [Awesome-CoreML-Models Github repo](https://github.com/likedan/Awesome-CoreML-Models){:target="_blank"}. You might have heard about the famous [GPT-2 model](https://en.wikipedia.org/wiki/GPT-2){:target="_blank"} created by the DeepMind company, which one of the founders is Elon Musk. GPT-2 model is converted to Core ML format, can be downloaded and easily run in the iOS project from [Awesome-CoreML-Models Github repo](https://github.com/likedan/Awesome-CoreML-Models){:target="_blank"}.

So how to convert any Machine Learning model and run it on iOS? `coremltools` is what we want to use for converting the model.

## Converting third-party Machine Learning models to Core ML format with coremltools

Machine Learning models architecture, functionality, input, and output differ very much from each other. This is why converting the model and making it run on iOS might be a bit tricky and vague task. Sometimes even theoretical and practical knowledge about the Machine Learning, convolutional neural networks, etc. might be needed. However, it is still worth spending the time investigating the problems and converting the model instead of collecting an enormous amount of data and paying hundreds of thousands or even millions  💵 for the processing power required for training the model.

In this article we will run through the example of converting neural networks model from the [coremltools documentation](https://coremltools.readme.io/docs/what-are-coreml-tools){:target="_blank"}, which I think highlights the important steps. With the `v4.0`coremltools introduced [Unified Conversion API](https://coremltools.readme.io/docs/unified-conversion-api){:target="_blank"} - an API for converting TensorFlow and PyTorch neural networks. `Unified Conversion API` is used in the following example.

### Converting the MobileNet model

First things first - the model to be converted needs to be loaded. In this example, a well known MobileNet model is loaded.

```python
import coremltools as ct
import tensorflow as tf

# Load TensorFlow model
tf_model = tf.keras.applications.MobileNet()
```

When the model is loaded, it can be converted simply like this:

```python
model_from_tf = ct.convert(tf_model)
```

Convertion results in producing the model that can be run in the iOS app through Core ML framework as described in the previous article: [3/5 How to use a custom Core ML model in the iOS App](/ML-fundamentals-that-every-iOS-developer-needs-to-know-3-5-How-to-use-a-custom-CoreML-model-in-the-iOS-App){:target="_blank"} or via [the abstraction of Vision framework](/ML-fundamentals-that-every-iOS-developer-needs-to-know-2-5-Native-domain-specific-ML-frameworks-for-iOS-developers){:target="_blank"}.

#### Loading Xception example

Loading MobileNet model is quite straight forward. Let's look into another example of loading a different model - [Xception](https://keras.io/api/applications/xception/){:target="_blank"}.

```python
tf_model = tf.keras.applications.Xception(weights="imagenet", 
                                          input_shape=(299, 299, 3))
```

This model loading is a bit more complex as it requires some parameters, like `input_shape`. Before starting the conversion it is advised to read the model's documentation, from which you want to convert. Documentation should contain important information like a list of required parameters which is mandatory for loading and converting the model.

## The sky is the limit

Nowadays developers have an enormous advantage - a comprehensive tool kit, extensive documentation, helpful communities, and Stack Overflow. Whenever we want to implement something new, often it is enough just to look for the information on the internet and very likely that somebody has already solved a similar problem and shared their knowledge with the world.

Not so long time ago Machine Learning was a buzzword, a technology, that to be leveraged required complex math and algorithms knowledge. While it is true on the academic level of Machine Learning, it doesn't have to be a case for a practical application of Machine Learning.

As we learned in the first article of the series [1/5 iOS Machine Learning Architecture & Tools](/ML-fundamentals-that-every-iOS-developer-needs-to-know-1-5-iOS-Machine-Learning-Architecture-Tools){:target="_blank"}, many tools are available for iOS developers that help to leverage Machine Learning technologies for problem-solving.

In the second article [2/5 Native domain-specific Machine Learning frameworks for iOS developers](/ML-fundamentals-that-every-iOS-developer-needs-to-know-2-5-Native-domain-specific-ML-frameworks-for-iOS-developers){:target="_blank"} we digged deeper and tried the native iOS Machine Learning frameworks, which are super easy to use. Not only easy to use - these frameworks might be the only tools needed for implementing the wanted impressive Machine Learning powered feature.

The functionality of these frameworks could be expanded by running the Core ML models provided by Apple or iOS community as we learned in [3/5 How to use a custom Core ML model in the iOS App](/ML-fundamentals-that-every-iOS-developer-needs-to-know-3-5-How-to-use-a-custom-CoreML-model-in-the-iOS-App){:target="_blank"} article.

When such models are not available, we explored how to create and train the Machine Learning models ourselves in the [4/5 Training Machine Learning models for the iOS App with Create ML and Turi Create](ML-fundamentals-that-every-iOS-developer-needs-to-know-4-5-Training-Machine-Learning-models-for-the-iOS-App-with-CreateML-and-TuriCreate){:target="_blank"} article.

Finally, in this last article of the series, we learned that models created by the scientists and engineers working for the most powerful tech companies can also run in our iOS applications. While research and development of such Machine Learning models cost millions of dollars, we iOS developers, can load and run them in our iOS applications just by spending some time on converting the model.

In these five articles, I explained the most important tools and techniques required to be dangerous in the field of Machine Learning and iOS application development. Future articles will contain more advanced content, like updating the already trained models with custom data. But for now, let's take a break from learning and apply what we already know. Let's build awesome applications and share them with the world!