---
title:  "Machine Learning fundamentals that every iOS developer needs to know: 2/5 Native domain-specific Machine Learning frameworks for iOS developers"
excerpt: "Introduction to the domain specific frameworks for implementing articifially intelligent features in iOS applications"
date:   2021-01-23 06:00:00 +0200
toc: true
header:
  teaser: /assets/images/posts/ML-fundamentals-that-every-iOS-developer-needs-to-know-architecture-tools-cover.jpg
  overlay_image: /assets/images/posts/ML-fundamentals-that-every-iOS-developer-needs-to-know-Native-domain-specific-frameworks-cover.jpg
  overlay_filter: 0.3
---

## Intro

In the previous article [1/5 iOS Machine Learning Architecture & Tools](/ML-fundamentals-that-every-iOS-developer-needs-to-know-1-5-iOS-Machine-Learning-Architecture-Tools){:target="_blank"} all the needed prerequisites were given so that any iOS developer using Swift language could feel comfortable with the content of this article. If you did not read it yet - I encourage you to do so.

In this article, four native domain-specific frameworks powered by Machine Learning models under the hood and used in the intelligent iOS applications development will be presented more in-depth. Frameworks are easy to use and in fact, one might have already used them without thinking about the complexity of Machine Learning.

Once the capabilities of the frameworks are presented and clear, we will see how to use them practically. Readers will be provided with a source code of a demo iOS application written with Swift and SwiftUI. This application demonstrates the examples of implementing intelligent features by using previously presented domain-specific Machine Learning frameworks.

## iOS domain-specific frameworks powered by Machine Learning

Let's go through the introduction of each framework and see if it could boost the intelligence of the beloved apps that we are working on.

- Vision
  
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
  
  And that is not it. If you are interested in using Vision - there is no better place to start than the [official Vision documentation](https://developer.apple.com/documentation/vision){:target="_blank"}.

- Natural Language
  
  Whenever you work with text and want to introduce some intelligence - the Natural Language framework should be your first choice. Sometimes it can provide amazing results with very little effort. Natural Language main features:

  - Language detection
  - Sentiment Analysis
  - Word & Sentence Embedding
  - Tokenization

  Automatically detecting and preselecting language from a user's text input is small but nice detail and things like that are super simple to implement using the Natural Language framework. Whether a goal is simple or more complex - [documentation always helps](https://developer.apple.com/documentation/naturallanguage){:target="_blank"}.

- Speech
  
  Thinking about implementing speech recognition into your iOS app? Speech framework is all you need to automatically generate transcripts, alternative interpretations, and confidence levels of the results from live or prerecorded audio. Combine Speech capabilities with Natural Language and the sky is the limit of what can be achieved. With the help of [Documentation of the Speech framework](https://developer.apple.com/documentation/speech){:target="_blank"} speech recognition in the iOS app will be implemented in no time.
  
- Sound Analysis

  [Sound Analysis framework](https://developer.apple.com/documentation/soundanalysis){:target="_blank"} is dedicated to helping you analyze and classify sound. The main power of the Sound Analysis framework is utilized when you already have a custom Core ML sound classification model. Such models could be downloaded or you can train them yourself using CreateML or other technologies.
  
  Do you feel amazed when an auto mechanic diagnoses the problem in your car just by listening and recognizing the specific noise coming from the engine? Well, now we have tools to make an app that is capable of doing that.

## Demo iOS Notes application with Machine Learning features

To demonstrate how easy it is to implement Machine Learning powered features in the iOS app I have created a demo notes application. The application has three Machine learning-powered features:

- Recognizing the text in the input image
- Recognizing the speech and extracting the subscript from the audio file
- Showing the language of the input text

Let's go through the implementation of each feature. You're welcome to download the project [from the Github repo.](https://github.com/arminasr/IntelliNote/) to make it easier to follow the code.

### How to detect and recognize text in images with Swift and Vision in iOS applications

![Text Recognition with Vision](/assets/images/posts/textRecognition.gif)

For detecting and recognizing text in images we will need to use the `Vision` framework.

First, we want to create a text recognition request `VNRecognizeTextRequest`.

```swift
private var textRecognitionRequest: VNRecognizeTextRequest {
    
    // 1. Creating recognize request
    return VNRecognizeTextRequest(completionHandler: { [weak self] (request, error) in
        if let recognizedText = request.results as? [VNRecognizedTextObservation] {
        
            // 2. If the request provides a result - take the top candidate from the returned Strings.
            let transcript = recognizedText.reduce("") { result, observation in
                guard let candidate = observation.topCandidates(1).first?.string else { return "" }
                return result.appending(candidate) + "\n"
            }
            
            DispatchQueue.main.async { [weak self] in
                
                // 3. Inform the delegate about successfull text recognitioon
                self?.delegate?.didRecognizeTextFromImage(transcript)
            }
        }
    })
}
```

Once we have `VNRecognizeTextRequest`, the only missing part is creating `VNImageRequestHandler` which processes the previously created request.

```swift
func recognizeText(in cgImage: CGImage) {
    
    // 1. Sending the request off the main thread
    DispatchQueue.global(qos: .userInitiated).async { [weak self] in
        guard let self = self else { return }
        
        // 2. Creating object that processes image analysis requests
        let handler = VNImageRequestHandler(cgImage: cgImage, options: [:])
        do {
            
            // 3. Performing the previously created request
            try handler.perform([self.textRecognitionRequest])
        } catch {
            self.delegate?.didFailRecognizeTextFromImage()
        }
    }
}
```

That's it! The full implementation of [`TextRecognitionService` is in the Github repo.](https://github.com/arminasr/IntelliNote/blob/main/IntelliNote/Services/TextRecognitionService.swift)

### How to detect speech and extract text from the audio files with Swift and Speech in iOS applications

![Audio Recognition with Speech](/assets/images/posts/audioRecognition.gif)

```swift
func recognizeText(fromAudioFileWith url: URL) {
    // 1. Creating speech recognizer object
    guard let speechRecognizer = SFSpeechRecognizer(), speechRecognizer.isAvailable else {
        delegate?.didFailRecognizeFromAudio()
        return
    }
    
    // 2. Creating and executing sppech recognition request
    let request = SFSpeechURLRecognitionRequest(url: url)
    speechRecognizer.recognitionTask(with: request) { [weak self] (result, error) in
        guard let result = result else {
            self?.delegate?.didFailRecognizeFromAudio()
            return
        }
        
        // 3. Handling speech recognition results
        if result.isFinal {
            self?.delegate?.didRecogniceTextFromAudio(result.bestTranscription.formattedString)
        }
    }
}
```

This is all the code needed to implement the feature of detecting and extracting the speech from audio files using the Speech framework. The full implementation of [`SpeechRecognitionService` is in the Github repo.](https://github.com/arminasr/IntelliNote/blob/main/IntelliNote/Services/SpeechRecognitionService.swift)

### How to identify the language of the text with Swift and Natural Language in iOS applications

In the gif images provided above, you might have noticed that after successful text recognition - the language of the text is identified. This functionality is implemented using the Natural Language framework.

```swift
func detectedLanguage(for string: String) -> String? {
    guard let languageCode = NLLanguageRecognizer.dominantLanguage(for: string)?.rawValue else {
        return nil
    }

    return Locale.current.localizedString(forIdentifier: languageCode)
}
```

The whole implementation of this feature is only a couple of Swift code lines, isn't it amazing?

## Conclusion

Implementation of Machine Learning powered features using domain-specific frameworks in iOS applications can be super simple. Give a shot, spin up playgrounds in the Xcode and try it yourself. Share your questions and results in the comments!
