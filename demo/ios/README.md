# Porcupine iOS Demos

## AccessKey

Porcupine requires a valid Picovoice `AccessKey` at initialization. `AccessKey` acts as your credentials when using Porcupine SDKs.
You can get your `AccessKey` for free. Make sure to keep your `AccessKey` secret.
Signup or Login to [Picovoice Console](https://console.picovoice.ai/) to get your `AccessKey`.

## BackgroundService Demo

This demo runs microphone recording in the background and detects the wake word while the application is **not** in focus. The wake word will be detected as long as the application remains running in the background.

**The minimum iOS version required is 10.0.**

To run the background service demo, go to [BackgroundService](./BackgroundService) directory. Then run:

```console
pod install
```

Replace `let accessKey = "${YOUR_ACCESS_KEY_HERE}"` in the file [ViewController.swift](./BackgroundService/PorcupineBackgroundServiceDemo/ViewController.swift) with your `AccessKey`.

Open `PorcupineBackgroundServiceDemo.xcworkspace` and run the demo.

Open up the demo and press start. The demo listens for the wake word "Porcupine". You may leave the application but the application must be running in the background to be able to continuously be detecting for the wake word.

## ForegroundApp Demo

This demo runs wake word detection while the application is in focus.

To run the foreground application demo:

1) Go to [ForegroundApp](./ForegroundApp) directory. Then run:

```console
pod install
```

2) Open the `PorcupineForegroundAppDemo.xcworkspace` in XCode

3) Replace `let accessKey = "${YOUR_ACCESS_KEY_HERE}"` in the file [ViewController.swift](./ForegroundApp/PorcupineForegroundAppDemo/ViewController.swift) with your `AccessKey`.

4) Go to `Product > Scheme` and select the scheme for the language you would like to demo (e.g. `esDemo` -> Spanish Demo, `deDemo` -> German Demo)

5) Run the demo with a simulator or connected iOS device

The demo allows you to select any of the pre-built keywords for detection. Press start and say the selected keyword.
