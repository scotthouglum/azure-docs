---
author: eric-urban
ms.service: cognitive-services
ms.topic: include
ms.date: 03/09/2020
ms.author: eur
ms.custom: devx-track-csharp
---

To configure the Speech SDK to accept compressed audio input, create `PullAudioInputStream` or `PushAudioInputStream`. Then, create an `AudioConfig` from an instance of your stream class that specifies the compression format of the stream. Find related sample code snippets in [About the Speech SDK audio input stream API](../../../../how-to-use-audio-input-streams.md).

Let's assume that you have an input stream class called `pullStream` and are using OPUS/OGG. Your code might look like this:

```csharp
using Microsoft.CognitiveServices.Speech;
using Microsoft.CognitiveServices.Speech.Audio;

// ... omitted for brevity

var speechConfig =
    SpeechConfig.FromSubscription(
        "YourSubscriptionKey",
        "YourServiceRegion");

// Create an audio config specifying the compressed
// audio format and the instance of your input stream class.
var audioFormat =
    AudioStreamFormat.GetCompressedFormat(
        AudioStreamContainerFormat.OGG_OPUS);
var audioConfig =
    AudioConfig.FromStreamInput(
        pullStream,
        audioFormat);

using var recognizer = new SpeechRecognizer(speechConfig, audioConfig);
var result = await recognizer.RecognizeOnceAsync();

var text = result.Text;
```
