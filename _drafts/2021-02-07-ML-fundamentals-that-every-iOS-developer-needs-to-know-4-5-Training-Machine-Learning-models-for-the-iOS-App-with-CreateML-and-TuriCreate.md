---
title:  "Machine Learning fundamentals that every iOS developer needs to know: 4/5 Training Machine Learning models for the iOS App with Create ML and Turi Create"
excerpt: "Learn to train Machine Learning model for iOS app with Create ML and Turi Create"
date:   2021-01-07 12:00:00 +0200
toc: true
header:
  teaser: /assets/images/posts/Training-Machine-Learning-models-for-the-iOS-App-with-CreateML-and-TuriCreate-cover.jpg
  overlay_image: /assets/images/posts/Training-Machine-Learning-models-for-the-iOS-App-with-CreateML-and-TuriCreate-cover.jpg
  overlay_filter: 0.3
---

## Training Machine Learning models for the iOS App

So far in the series of articles we have learned how to build artificially intelligent features using already pre-trained Machine Learning models - either [via domain-specific frameworks](/ML-fundamentals-that-every-iOS-developer-needs-to-know-2-5-Native-domain-specific-ML-frameworks-for-iOS-developers){:target="_blank"} or by [downloading and using machine learning models from the internet](/ML-fundamentals-that-every-iOS-developer-needs-to-know-3-5-How-to-use-a-custom-CoreML-model-in-the-iOS-App){:target="_blank"}. Very often this functionality covers developer's needs, however to fulfill more specific requirements and empower the collected data, training models ourselfs is the way to go.

In this article reader will get knowledge of how to use [tools for creating and Training custom Machine Learning models](/ML-fundamentals-that-every-iOS-developer-needs-to-know-1-5-iOS-Machine-Learning-Architecture-Tools/#creating-and-training-custom-machine-learning-models-for-ios-applications){:target="_blank"}.

For simplicity a very primitive example will be used across the article - we will train a sound classifier model that can recognize and distinguish two sound categories: dogs barking and cats meowing. The dataset used for training the model can be [downloaded from the Kaggle website](https://www.kaggle.com/tongpython/cat-and-dog){:target="_blank"}.

Without any further ado let's jump into training the sound classifier machine learning model with Create ML.

## Training Machine Learning Sound Classifier model with Create ML

Create ML provides two ways of training the models - via the Create ML Application with an intuitive user interface and via code. Although we developers like to write code, I encourage you to use Create ML application instead of writing training scripts yourself using the CreateML framework in Xcode Playgrounds. The Create ML application provides almost as much flexibility as you'd get by writing code. Besides, Create ML application also draws informative training accuracy graphs, allows to test models manually, and much more. If you feel like you cannot achieve something with Create ML application, most likely you'll end up with other tools like Create ML than using Create ML in playgrounds. Ok, let's train our first Machine Learning model!

Type in `Create ML` into the finder and open the application. Then start a new project by selecting `File -> New Project`. You should end up with a window presenting a bunch of templates on your Mac screen:

![Create ML Sound Classification template](/assets/images/posts/createml-templates.png)

We are interested in the `Sound Classification` template, so let's choose this one. After entering all the needed project information, the project window with fields for selecting training and validation data appears. The data (sound samples) for each category must be separated into different folders like so:

![Training data folder structure](/assets/images/posts/training-data-folders.png)

When data is structured correctly into different folders, the last step before starting the training is selecting the datasets in the Create ML application. Validation data can be set to `Automatic`. However, this is very important that validation data is set - it prevents a common problem in Machine Learning known as **overfitting**. You can read [more about overfitting and what it is in wikipedia](https://en.wikipedia.org/wiki/Overfitting){:target="_blank"}.

![Create ML data for training selection](/assets/images/posts/createml-setup.png)

After selecting training, validation, and test data, press `Run` and go prepare some ☕️. Well, with this amount of data and M1 processor you probably won't even have time to stand up before training is finished. A lot of interesting information about the training progress and model's accuracy is presented in different tabs of the application> Create ML application even allows to test the model manually by selecting sound files. But here we are mostly interested in the output - the sound classifier model.

![Create ML data for training selection](/assets/images/posts/createml-output.png)

That's it - the Machine Learning model for classifying sounds of barking and meowing is ready for use.

## Training Machine Learning Sound Classifier model with Turi Create

It is common for iOS developers to lock in technologies provided by Apple for iOS development, like Objective-C, Swift, and Xcode. Here the comfort zone will be left because we are going to play with Python a bit ⚠️. Yes, Turi Create is a Python package! But don't get scared, [Turi Create provides a great user guide and documentation](https://apple.github.io/turicreate/docs/userguide/){:target="_blank"} and is quite easy to use. Let's see it yourself in the [Google Colab Notebook](https://colab.research.google.com/drive/1zj-iASrJdj5bbVuL6u7ln7KHGvJZAgsU?usp=sharing){:target="_blank"} where all the code for training the sound classifier is written. For those who don't know what is Google Colab, here is the official explanation:
>Colaboratory, or "Colab" for short, allows you to write and execute Python in your browser, with:
>
>- Zero configuration required
>- Free access to GPUs
>- Easy sharing

In short, Google's Colab provides a way to write code in the browser, use all the powerful Google's GPU's and train models in the cloud for free, how cool is that?

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

This is probably the simplest example of what can be achieved with Turi Create. The more advanced examples of Turi Create usage are presented [in the official documentation](https://apple.github.io/turicreate/docs/userguide/sound_classifier/advanced-usage.html){:target="_blank"}.

So, is Python and Turi Create really that scary?

## Running Sound Classifier model with Sound Analysis framework

Ok, let's run the sound classifier Machine Learning model and see how it works in Xcode Playgrounds. It doesn't matter which model we take, either one from Create ML or Turi Create should work the same way.

All the code for running the model in the Xcode Playgrounds [can be found here](https://github.com/arminasr/arminasr.github.io-playgrounds/tree/master/CatsVsDogs){:target="_blank"}. However, the essence of getting the result from the model is super simple.

```swift
class SoundClassifierObserver: NSObject {
    func analyzeSoundSample(at url: URL) {
        // 1. Initialize Sound Analyzer, model and request
        guard let fileAnalyzer = try? SNAudioFileAnalyzer(url: url),
              let model = try? CatsVsDogs(configuration: MLModelConfiguration()).model,
              let request = try? SNClassifySoundRequest(mlModel: model) else { return }
        
        // 2. Add request and analyze the sound sample
        try? fileAnalyzer.add(request, withObserver: self)
        fileAnalyzer.analyze()
    }
}
```

1. First we want to initialize Sound Analyzer, the model that we trained previously, and classification request.

2. After adding the request to the analyzer we can start the sound analysis. In this example `func analyze()` was called, which executes synchronously. Be careful, the task might run for a long time and block UI. There is another method that runs asynchronously, `func analyze(completionHandler: @escaping (Bool) -> Void)`, consider using it.

In one of the lines `self` is passed as `observer`. This passed parameter is the object that is going to observe the results from the analysis. It must conform to the protocol `SNResultsObserving`.

```swift
extension SoundClassifierObserver: SNResultsObserving {
    func requestDidComplete(_ request: SNRequest) {
        print("Request: \(request.description) completed.")
    }
    
    func request(_ request: SNRequest, didFailWithError error: Error) {
        print("Request: \(request.description) failed with error \(error.localizedDescription).")
    }
    
    func request(_ request: SNRequest, didProduce result: SNResult) {
        guard let result = result as? SNClassificationResult else { return }
        result.classifications
            .filter { $0.confidence > 0.85 }
            .forEach {
                print("Class: \($0.identifier) Confidence: \($0.confidence * 100)%")
            }
    }
}
```

Let's try to run the analysis on one of the sound samples with a cat meowing

```swift
if let testAudioURL = Bundle.main.url(forResource: "cat_152", withExtension: "wav") {
    let observer = SoundClassifierObserver()
    observer.analyzeSoundSample(at: testAudioURL)
}
```

In this case, the analysis goes successful and method `func request(_ request: SNRequest, didProduce result: SNResult)` gets called. The previously trained sound classifier is quite confident that a cat is meowing in this sound sample:

```bash
Class: cat Confidence: 99.99999775404376%
Class: cat Confidence: 99.99998888215313%
Class: cat Confidence: 99.99999989513636%
...
```

There we go, the first Machine Learning model trained by ourselves works like a charm! 🍻 Isn't that awesome?

With Create ML, training another type of model, using tabular data or images isn't very different from training a sound classifier. I can't wait to hear what Machine Learning models you'll come up with. Share it in the comments or send me a message!
