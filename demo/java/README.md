# Porcupine Java Demos

This package provides two demonstration command-line applications for Porcupine: a file based demo, which scans a compatible WAV file for keywords, and a microphone demo, which listens for keywords and outputs detections live.

## Introduction to Porcupine

Porcupine is a highly accurate and lightweight wake word engine. It enables building always-listening voice-enabled applications using cutting edge voice AI.

Porcupine is:

- private and offline
- [accurate](https://github.com/Picovoice/wake-word-benchmark)
- [resource efficient](https://www.youtube.com/watch?v=T0tAnh8tUQg) (runs even on microcontrollers)
- data efficient (wake words can be easily generated by simply typing them, without needing thousands of hours of bespoke audio training data and manual effort)
- scalable to many simultaneous wake-words / always-on voice commands
- cross-platform

To learn more about Porcupine, see the [product](https://picovoice.ai/products/porcupine/), [documentation](https://picovoice.ai/docs/), and [GitHub](https://github.com/Picovoice/porcupine/) pages.

## Requirements

- Java 11+

## Compatibility

- Linux (x86_64)
- macOS (x86_64, arm64)
- Windows (x86_64, arm64)
- Raspberry Pi 3 (32 and 64 bit), Raspberry Pi 4 (32 and 64 bit), Raspberry Pi 5 (32 and 64 bit)

## Installation

Build the demo jars with Gradle:
```console
cd porcupine/demo/java
./gradlew build
```

## Usage

Navigate to the output directory to use the demos:

```console
cd porcupine/demo/java/build/libs
```

## AccessKey

Porcupine requires a valid Picovoice `AccessKey` at initialization. `AccessKey` acts as your credentials when using Porcupine SDKs.
You can get your `AccessKey` for free. Make sure to keep your `AccessKey` secret.
Signup or Login to [Picovoice Console](https://console.picovoice.ai/) to get your `AccessKey`.

### File Demo

The file demo uses Porcupine to scan for keywords in a wave file. The demo is mainly useful for quantitative performance benchmarking against a corpus of audio data. 
Porcupine processes a 16kHz, single-channel audio stream. If a stereo file is provided it only processes the first (left) channel. 
The following processes a file looking for instances of the phrase "Picovoice":

```console
java -jar porcupine-file-demo.jar -a ${ACCESS_KEY} -i ${AUDIO_PATH} -k picovoice
```

`-k` or `--keywords` is a shorthand for using built-in keywords shipped with the package. The list of built-in keyword files
can be seen in the usage string:

```console
java -jar porcupine-file-demo.jar -h
```

To detect multiple phrases concurrently provide them as separate arguments. If the wake word is more than a single word, surround the argument in quotation marks:

```console
java -jar porcupine-file-demo.jar -a ${ACCESS_KEY} -i ${AUDIO_PATH} -k grasshopper "hey siri"
```

To detect custom keywords (e.g. models created using [Picovoice Console](https://console.picovoice.ai/))
use the `-kp` or `--keyword_paths` argument:

```console
java -jar porcupine-file-demo.jar -a ${ACCESS_KEY} -i ${AUDIO_PATH} -kp ${KEYWORD_PATH_ONE} ${KEYWORD_PATH_TWO}
```

The sensitivity of the engine can be tuned per keyword using the `-s` or `--sensitivities` input argument:

```console
java -jar porcupine-file-demo.jar -a ${ACCESS_KEY} -i ${AUDIO_PATH} -k grasshopper porcupine -s 0.3 0.6
```

Sensitivity is the parameter that enables trading miss rate for the false alarm rate. It is a floating-point number within
`[0, 1]`. A higher sensitivity reduces the miss rate at the cost of increased false alarm rate.

### Microphone Demo

This demo opens an audio stream from a microphone and detects utterances of a given wake word. The following opens the default
microphone and detects occurrences of "Picovoice":

```console
java -jar porcupine-mic-demo.jar -a ${ACCESS_KEY} -k picovoice
```

`-k` or `--keywords` is a shorthand for using built-in keyword files shipped with the package. The list of built-in keyword files
can be seen in the usage string:

```console
java -jar porcupine-mic-demo.jar -h
```

To detect multiple phrases concurrently provide them as separate arguments. If the wake word is more than a single word, surround the argument in quotation marks: 

```console
java -jar porcupine-mic-demo.jar -a ${ACCESS_KEY} -k picovoice "hey siri"
```

To detect custom keywords (e.g. models created using [Picovoice Console](https://console.picovoice.ai/))
use the `-kp` or `--keyword_paths` argument:

```console
java -jar porcupine-mic-demo.jar -a ${ACCESS_KEY} -kp ${KEYWORD_PATH_ONE} ${KEYWORD_PATH_TWO}
```

It is possible that the default audio input device is not the one you wish to use. There are a couple
of debugging facilities baked into the demo application to solve this. First, type the following into the console:

```console
java -jar porcupine-mic-demo.jar -sd
```

It provides information about various audio input devices on the box. On a Windows PC, this is the output:

```
Available input devices:

    Device 4: Microphone Array (Realtek(R) Au
    Device 5: Microphone Headset USB
``` 

You can use the device index to specify which microphone to use for the demo. For instance, if you want to use the Headset 
microphone in the above example, you can invoke the demo application as below:

```console
java -jar porcupine-mic-demo.jar -a ${ACCESS_KEY} -k picovoice -di 5
```

If the problem persists we suggest storing the recorded audio into a file for inspection. This can be achieved with:

```console
java -jar porcupine-mic-demo.jar -a ${ACCESS_KEY} -k picovoice -di 5 -o ./test.wav
```

If after listening to stored file there is no apparent problem detected please open an issue.
