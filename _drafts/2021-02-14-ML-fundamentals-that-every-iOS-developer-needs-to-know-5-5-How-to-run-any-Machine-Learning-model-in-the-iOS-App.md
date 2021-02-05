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

In the previous articles we learned to train and run only machine Learning models format that is supported by the Core ML. Sadly, the most popular Machine Learning platforms and frameworks are not in the ecosystem of Apple, meaning those models are not supported by the Core ML. There are hundreds or thousands of already pre-trained models that would fit our needs, the problem is that iOS developers cannot run them in the apps. But, really, can't they?

There is a chance that machine learning model trained with one of the most popular frameworks, like `TensorFlow`, `PyTorch`, `Keras`, `Caffe` as well as classical machine learning frameworks like `LIBSVM`, `scikit-learn`, and `XGBoost` can be converted to the `.mlmodel` format. And actually even some Core ML models that can be downloadted from the Apple website are converted from some of the previously listed formats. A huge list of Core ML models that are converted from other formats and are ready to be used in the iOS applications can be found in [Awesome-CoreML-Models Github repo](https://github.com/likedan/Awesome-CoreML-Models){:target="_blank"}. You might have heard about the famous [GPT-2 model](https://en.wikipedia.org/wiki/GPT-2){:target="_blank"} created by the DeepMind company, which one of the founders is Elon Musk. GPT-2 model is converted to Core ML format, can be downloaded and easily run in the iOS project from [Awesome-CoreML-Models Github repo](https://github.com/likedan/Awesome-CoreML-Models){:target="_blank"}.

So how to convert any Machine Learning model and run it on iOS? `coremltools` is what we want to use for converting the model.

## Converting third-party Machine Learning models to Core ML format with coremltools

Machine Learning models architecture, functionality, input and output differs very much from each other. This is why converting the model and making it run on the iOS might be a bit tricky and vague task. Sometime even the theoretical and practical knowledge about the Machine Learning, convolutional neural networks, etc. might be needed. However, it is still worth to spend the time investigating the problems and converting the model instead of collecting enourmous amount of data and paying hundreds of thousands or even millions of 💵 for the processing power required for training the model.

In this article we will run through the example of converting neural networks model from the [coremltools documentation](https://coremltools.readme.io/docs/what-are-coreml-tools){:target="_blank"}, which I think highlights the important steps. With the `v4.0`coremltools introduced [Unified Conversion API](https://coremltools.readme.io/docs/unified-conversion-api){:target="_blank"} - an API for converting TensorFlow and PyTorch neural networks. `Unified Conversion API` is used in the following example.

### Converting the MobileNet model

First things first - the model to be converted needs to be loaded. In this example a well known MobileNet model is loaded.

```python
import coremltools as ct
import tensorflow as tf

# Load TensorFlow model
tf_model = tf.keras.applications.MobileNet()
```

When model is loaded, it can be converted simply like this:

```python
model_from_tf = ct.convert(tf_model)
```

Convertion results in producing the model that can be run in the iOS app through Core ML framework as described in the previous article: [3/5 How to use a custom Core ML model in the iOS App](/ML-fundamentals-that-every-iOS-developer-needs-to-know-3-5-How-to-use-a-custom-CoreML-model-in-the-iOS-App){:target="_blank"} or via [the abstraction of Vision framework](/ML-fundamentals-that-every-iOS-developer-needs-to-know-2-5-Native-domain-specific-ML-frameworks-for-iOS-developers){:target="_blank"}.

### Converting the Xception model

Previous convertion of the MobileNet model was quite straightforward.

```python
import coremltools as ct 
import tensorflow as tf

# Load from .h5 file
tf_model = tf.keras.applications.Xception(weights="imagenet", 
                                          input_shape=(299, 299, 3))

# Convert to Core ML
model = ct.convert(tf_model)
```