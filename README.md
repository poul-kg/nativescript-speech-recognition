# NativeScript Speech Recognition

[![NPM version][npm-image]][npm-url]
[![Downloads][downloads-image]][npm-url]
[![Twitter Follow][twitter-image]][twitter-url]

[npm-image]:http://img.shields.io/npm/v/nativescript-speech-recognition.svg
[npm-url]:https://npmjs.org/package/nativescript-speech-recognition
[downloads-image]:http://img.shields.io/npm/dm/nativescript-speech-recognition.svg
[twitter-image]:https://img.shields.io/twitter/follow/eddyverbruggen.svg?style=social&label=Follow%20me
[twitter-url]:https://twitter.com/eddyverbruggen

This is the plugin [demo](https://github.com/EddyVerbruggen/nativescript-speech-recognition/tree/master/demo) in action..

| ..while recognizing Dutch 🇳🇱 | .. after recognizing American-English 🇺🇸 |
| --- | --- |
| <img src="https://github.com/EddyVerbruggen/nativescript-speech-recognition/raw/master/screenshots/ios-nl.jpg" width="375px" /> | <img src="https://github.com/EddyVerbruggen/nativescript-speech-recognition/raw/master/screenshots/ios-en.jpg" width="375px" /> |

## Installation
From the command prompt go to your app's root folder and execute:

```
tns plugin add nativescript-speech-recognition
```

## API

### `available`

Depending on the OS version a speech engine may not be available.

#### JavaScript
```js
// require the plugin
var SpeechRecognition = require("nativescript-speech-recognition").SpeechRecognition;

// instantiate the plugin
var speechRecognition = new SpeechRecognition();

speechRecognition.available().then(
  function(available) {
    console.log(available ? "YES!" : "NO");
  }
);
```

#### TypeScript
```js
// import the plugin
import { SpeechRecognition } from "nativescript-speech-recognition";

// instantiate the plugin (assuming the code below is inside a Class)
private speechRecognition = new SpeechRecognition();

public checkAvailability(): void {
  this.speechRecognition.available().then(
    (available: boolean) => console.log(available ? "YES!" : "NO"),
    (err: string) => console.log(err)
  );
}
```

### `startListening`

On iOS this will trigger two prompts:

The first prompt requests to allow Apple to analyze the voice input. The user will see a consent screen which you can extend with your own message by adding a fragment like this to `app/App_Resources/iOS/Info.plist`:

```xml
<key>NSSpeechRecognitionUsageDescription</key>
<string>My custom recognition usage description. Overriding the default empty one in the plugin.</string>
```

The second prompt requests access to the microphone:

```xml
<key>NSMicrophoneUsageDescription</key>
<string>My custom microphone usage description. Overriding the default empty one in the plugin.</string>
```

#### TypeScript
```js
// import the options
import { SpeechRecognitionTranscription } from "nativescript-speech-recognition";

this.speechRecognition.startListening(
  {
    // optional, uses the device locale by default
    locale: "en-US",
    // this callback will be invoked repeatedly during recognition
    onResult: (transcription: SpeechRecognitionTranscription) => {
      console.log(`User said: ${transcription.text}`);
      console.log(`User finished?: ${transcription.finished}`);
    },
  }
).then(
  (started: boolean) => { console.log(`started listening`) },
  (errorMessage: string) => { console.log(`Error: ${errorMessage}`); }
);
```

### `stopListening`

#### TypeScript
```js
this.speechRecognition.stopListening().then(
  () => { console.log(`stopped listening`) },
  (errorMessage: string) => { console.log(`Stop error: ${errorMessage}`); }
);
```

## Usage with Angular
Check out [this tutorial (YouTube)](https://www.youtube.com/watch?v=C5i_EYjfuTE) to learn how to use this plugin in a NativeScript-Angular app.
