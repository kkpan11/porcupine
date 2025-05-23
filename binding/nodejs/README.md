# Porcupine Binding for Node.js

## Porcupine

Porcupine is a highly accurate and lightweight wake word engine. It enables building always-listening voice-enabled applications using cutting edge voice AI.

Porcupine is:

- private and offline
- [accurate](https://github.com/Picovoice/wake-word-benchmark)
- [resource efficient](https://www.youtube.com/watch?v=T0tAnh8tUQg) (runs even on microcontrollers)
- data efficient (wake words can be easily generated by simply typing them, without needing thousands of hours of bespoke audio training data and manual effort)
- scalable to many simultaneous wake-words / always-on voice commands
- cross-platform

To learn more about Porcupine, see the [product](https://picovoice.ai/products/porcupine/), [documentation](https://picovoice.ai/docs/), and [GitHub](https://github.com/Picovoice/porcupine/) pages.

### Custom wake words

Porcupine includes several built-in keywords, which are stored as `.ppn` files. To train custom PPN files, see the [Picovoice Console](https://console.picovoice.ai/).

Unlike the built-in keywords, custom PPN files generated with the Picovoice Console carry restrictions including (but not limited to): training allowance, time limits, available platforms, and commercial usage.

## Compatibility

This binding is for running Porcupine on **Node.js 16+** on the following platforms:

- Windows (x86_64, arm64)
- Linux (x86_64)
- macOS (x86_64, arm64)
- Raspberry Pi (3, 4, 5)

### Web Browsers

This npm package is for Node.js and **does not work in a browser**. Looking to run Porcupine in-browser? There are npm packages available for [Web](https://www.npmjs.com/package/@picovoice/porcupine-web), and dedicated package for [React](https://www.npmjs.com/package/@picovoice/porcupine-react).

## AccessKey

Porcupine requires a valid Picovoice `AccessKey` at initialization. `AccessKey` acts as your credentials when using Porcupine SDKs.
You can get your `AccessKey` for free. Make sure to keep your `AccessKey` secret.
Signup or Login to [Picovoice Console](https://console.picovoice.ai/) to get your `AccessKey`.

## Usage

The binding provides the `Porcupine` class. Create instances of the `Porcupine` class to detect specific keywords.

### Quick Start: Built-in keywords

The built-in keywords give a quick way to get started. Here we can specify that we want to listen for the wake words "grasshopper" and "bumblebee" with [sensitivities](https://picovoice.ai/docs/faq/porcupine/#what-should-i-set-the-sensitivity-value-to) of 0.5 and 0.65, respectively. Since Porcupine can listen to multiple keywords simultaneously, they are provided as an array argument.

```javascript
const {
  Porcupine,
  BuiltinKeyword,
}= require("@picovoice/porcupine-node");

const accessKey = "${ACCESS_KEY}" // Obtained from the Picovoice Console (https://console.picovoice.ai/)

const handle = new Porcupine(
    accessKey,
    [BuiltinKeyword.GRASSHOPPER, BuiltinKeyword.BUMBLEBEE],
    [0.5, 0.65]);

// process a single frame of audio
// the keywordIndex provides the index of the keyword detected, or -1 if no keyword was detected
const keywordIndex = handle.process(frame);
```

#### List of built-in keywords

- ALEXA
- AMERICANO
- BLUEBERRY
- BUMBLEBEE
- COMPUTER
- GRAPEFRUIT
- GRASSHOPPER
- HEY_GOOGLE
- HEY_SIRI
- JARVIS
- OK_GOOGLE
- PICOVOICE
- PORCUPINE
- TERMINATOR

### Custom keywords

Providing an array of strings instead of the built-in enums allows you to specify an absolute path to a keyword `.ppn` file:

```javascript
const accessKey = "${ACCESS_KEY}" // Obtained from the Picovoice Console (https://console.picovoice.ai/)

const handle = new Porcupine(
    accessKey,
    ["/absolute/path/to/your/keyword.ppn"],
    [0.5]);
```

### Override model and library paths

The Porcupine constructor accepts two optional positional parameters for the absolute paths to the model and dynamic library, should you need to override them (typically, you will not).

```javascript
const accessKey = "${ACCESS_KEY}" // Obtained from the Picovoice Console (https://console.picovoice.ai/)

const handle = new Porcupine(
  accessKey,
  keywordPaths,
  sensitivities,
  modelFilePath,
  libraryFilePath
);
```

## Using the bindings from source

## Unit Tests

Run `yarn` (or`npm install`) from the [binding/nodejs](https://github.com/Picovoice/porcupine/tree/master/binding/nodejs) directory to install project dependencies. This will also run a script to copy all the necessary shared resources from the Porcupine repository into the package directory.

Run `yarn test` (or `npm run test`) from the [binding/nodejs](https://github.com/Picovoice/porcupine/tree/master/binding/nodejs) directory to execute the test suite.
