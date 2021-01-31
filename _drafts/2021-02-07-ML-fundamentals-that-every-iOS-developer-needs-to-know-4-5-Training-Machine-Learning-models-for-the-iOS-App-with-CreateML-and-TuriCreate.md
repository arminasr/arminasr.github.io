---
title:  "Machine Learning fundamentals that every iOS developer needs to know: 4/5 Training Machine Learning models for the iOS App with Create ML and Turi Create"
excerpt: "Introduction of the series about Artificial Intelligince and Machine Learning fundamentals that every iOS developer needs to know."
date:   2021-01-07 12:00:00 +0200
header:
  teaser: /assets/images/posts/Training-Machine-Learning-models-for-the-iOS-App-with-CreateML-and-TuriCreate-cover.jpg
  overlay_image: /assets/images/posts/Training-Machine-Learning-models-for-the-iOS-App-with-CreateML-and-TuriCreate-cover.jpg
  overlay_filter: 0.3
---

## Training Machine Learning models for the iOS App

So far in the series of articles we have learned how to build artificially intelligent features using already pre-trained Machine Learning models - either [via domain-specific frameworks](/ML-fundamentals-that-every-iOS-developer-needs-to-know-2-5-Native-domain-specific-ML-frameworks-for-iOS-developers){:target="_blank"} or by [downloading and using machine learning models from the internet](/ML-fundamentals-that-every-iOS-developer-needs-to-know-3-5-How-to-use-a-custom-CoreML-model-in-the-iOS-App){:target="_blank"}. Very often this functionality covers developer's needs, however to fulfill more specific requirements and empower the collected data, training models ourselfs is the way to go.

In this article reader will get knowledge of how to use [previously described tools: Create ML and Turi Create](/ML-fundamentals-that-every-iOS-developer-needs-to-know-1-5-iOS-Machine-Learning-Architecture-Tools/#creating-and-training-custom-machine-learning-models-for-ios-applications){:target="_blank"} and train their own Machine Learning models.

For the purpose of simplicity a very primitive example will be used across the article - we will train a sound classifier model that is able to recognize and distinguish two sound categories: dos barking and cats meowing. The dataset used for training the model can be [downloaded from Kaggle website](https://www.kaggle.com/tongpython/cat-and-dog){:target="_blank"}.

Without any further ado let's jump into training the sound classifier machine learning model with Create ML.

## Training Machine Learning Sound Classifier model with Create ML

Create ML provides two ways of training the models - via the Create ML Application with intuitive user interface and via code. Although we developers like to write code, I encourage to use Create ML application instead of writing training scripts yoursel using CreateML framework in Xcode Playgrounds. Create ML application provides almost as much flexibility as you'd get by writting code. However, Create ML application also draws informative training accuracy graphs, allows to test models manually and much more. If you feel like you cannot achieve something with Create ML application, most likely you'll end up with other tools like Create ML than using Create ML in playgrounds. Ok, let's train our first Machine Learning model!

Type in `Create ML` into the finder and open the application. Then start a new project by selecting `File -> New Project`. You should end up with a window presenting a bunch of templates on your Mac screen:

![Create ML Sound Classification template](/assets/images/posts/createml-templates.png)

We are interested in the `Sound Classification` template, so let's choose this one. After entering all the needed project information, the project window with fields for selecting training and validation data appears. The data (sound samples) for each category must be separated into different folders like so:

![Training data folder structure](/assets/images/posts/training-data-folders.png)

When data is structured correctly into different folders, identically for training and testing data, the last step before starting the training is selecting the training and testing data. Validation data can be set to `Automatic`. However, this is very important that validation data is set - it prevents from a common problem in Machine Learning known as **overfitting**. You can read [more about overfitting and what it is in wikipedia](https://en.wikipedia.org/wiki/Overfitting){:target="_blank"}.

![Create ML data for training selection](/assets/images/posts/createml-setup.png)

After selecting training, validation and test data, press `Run` and go prepare some ☕️. Well, with this amount of data and M1 processor you probably won't even have time to stand up before training is finished. A lot of interesting informatiopn about the training progress and model's accuracy can be found, Create ML application even allows to test the model manually by selecting sound files. But here were are interested in the output - the sound classifier model.

![Create ML data for training selection](/assets/images/posts/createml-output.png)

That's it - model for classifying sounds of barking and meowing is ready for use.

## Training Machine Learning Sound Classifier model with Turi Create

It is common for iOS developers to lock in using technologies provided by Apple for iOS development, like: Objective-C, Swift and Xcode. Here we will leave the comfort zone and play with Python a bit ⚠️. Yes, Turi Create is a Python package! But don't get scared, [Turi Create provides a great user guide and documentation](https://apple.github.io/turicreate/docs/userguide/){:target="_blank"} and is quite easy to use. Let's see it yourself in the Google Colab Notebook where all the code for training the sound classifier is written. For those who don't know what is Google Colab, here is the official explanation:
>Colaboratory, or "Colab" for short, allows you to write and execute Python in your browser, with:
>
>- Zero configuration required
>- Free access to GPUs
>- Easy sharing

In short, Google's Colab provides a way to write code in the browser, use all the powerful Google's GPU's and train models in the cloud, how cool is that?

The whole code for formatting the data and training the model [can be found here](https://colab.research.google.com/drive/1zj-iASrJdj5bbVuL6u7ln7KHGvJZAgsU?usp=sharing){:target="_blank"}.

The general rule in data science and Machine Learning is that data cleaning and formatting takes much more time than actually creating the model. As you can see from the code, when data is prepared, only a couple of lines of code are required to create and train the model.

```python
# Create the model.
model = tc.sound_classifier.create(train_data, target='category', feature='audio')

# Generate predictions from the test set.
predictions = model.predict(test_data)

# Evaluate the model's accuracy
metrics = model.evaluate(test_data)
print(metrics)

# Save the model in Turi Create format
model.save('soundClassifier.model')

# Export the model for use in Core ML
model.export_coreml('soundClassifier.mlmodel')
```

So, is Python and Turi Create really that scary?

## Using our
