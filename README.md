# Flutter Scalable OCR

This package is a wrapper around [flutter_scalable_ocr](https://pub.dev/packages/flutter_scalable_ocr). It tackles the issue of fetching data just from part od a camera and also narowing down the camera viewport which was common problem.

https://github.com/KobayashiYoh/flutter_scalable_ocr/assets/82624334/26b49717-96a8-4b07-ad79-e61d7bbd6d54

## Requirements

Since thus package uses [ML Kit](https://pub.dev/packages/google_mlkit_commons) check [requirements](https://github.com/bharat-biradar/Google-Ml-Kit-plugin#requirements) before running the package in project.

## Features

Scan text from narow window of camera and not whole screen. There are two function `getScannedText` to fetch readed text as a string, or `getRawData` which returns list of `TextElement` consult [ML Kit Text Recognition](https://developers.google.com/ml-kit/vision/text-recognition) objects as from followin structure from google developer site image. Pinch and zoom should also work:

Note: Wrapper uses [Camera](https://pub.dev/packages/camera) package so you need to add perimission as in documentation.

<p float="left">
  <img src="https://developers.google.com/static/ml-kit/vision/text-recognition/images/text-structure.png" width="600" />
</p>

## Usage

Add the package to pubspec.yaml

```dart
dependencies:
  flutter_scalable_ocr: x.x.x
```

Import it

```dart
import 'package:flutter_scalable_ocr/flutter_scalable_ocr.dart';
```

Full examples for all three options are in `/example` folder so please take a look for working version.

Parameters:

| Parameter      |      Description      |  Default |
|--------------- |:---------------------:|---------:|
| `boxLeftOff`     |  Scalable center square left         | 4        |
| `boxBottomOff`   |  Scalable center square bottom    | 2.7      |
| `boxRightOff`    |  Scalable center square right  | 4        |
| `boxTopOff`      |  Scalable center square top   | 2.7      |
| `centerRadius`      |  Radius of center RRect   | Radius.zero      |
| `paintboxCustom`      |  Narrowed square in camera window  | from example|
| `boxHeight`      |  Camera Window height | from example      |
| `getScannedText`      |  Callback function that returns string |     |
| `getRawData`      |  Callback function that returns list of `TextElement`     |
| `cameraMarginColor`      | Color of camera margin     |

Use widget:

```dart
ScalableOCR(
  paintboxCustom: Paint()
    ..style = PaintingStyle.stroke
    ..strokeWidth = 4.0
    ..color = Colors.blue,
  boxLeftOff: 5,
  boxBottomOff: 2.5,
  boxRightOff: 5,
  boxTopOff: 2.5,
  centerRadius: const Radius.circular(8.0),
  boxHeight: MediaQuery.of(context).size.height / 3,
  getRawData: (value) {
    inspect(value);
  },
  getScannedText: (value) {
    setText(value);
  },
  cameraMarginColor: const Color(0xCC000000),
),
```
