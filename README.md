# Flutter Image Picker Web

This Web-Plugin allows Flutter Web to pick images (as File, Widget or Uint8List) and videos (as File or Uint8List). Many thanks goes to AlvaroVasconcelos for the implementation of picking images in his plugin: flutter_web_image_picker

## Getting Started

Add image_picker_web to your pubspec.yaml:

   ```
   image_picker_web: any
   ```

## Picking Images

### Pick an image

Load image as Image.memory Widget:

   ```
   Image? fromPicker = await ImagePickerWeb.getImageAsWidget();
   ```

Load image as bytes:

   ```
   Uint8List? bytesFromPicker = await ImagePickerWeb.getImageAsBytes();
   ```

Load image as and html.File object :

   ```
   html.File? imageFile = await ImagePickerWeb.getMultiImagesAsFile();
   ```

### Pick multiple images

Load images as a List<Image> :

   ```
   List<Image>? fromPicker = await ImagePickerWeb.getMultiImagesAsWidget();
   ```

Load images as bytes :

   ```
   List<Uint8List>? bytesFromPicker = await ImagePickerWeb.getMultiImagesAsBytes();
   ```

Load images as List<html.File> objects :

   ```
   List<html.File> imageFiles = await ImagePickerWeb.getMultiImagesAsFile();
   ```

## How do I get all Informations out of my Image/Video (e.g. Image AND File in one run)?

Besides the standard getImage() or getVideo() methods you can use the getters:

1. getImageInfo or

2. getVideoInfo to acheive this.

Full Example

   ```
   import 'dart:html' as html;
 
import 'package:mime_type/mime_type.dart';
import 'package:path/path.dart' as Path;
import 'package:image_picker_web/image_picker_web.dart';
import 'package:flutter/material.dart';

 html.File _cloudFile;
 var _fileBytes;
 Image _imageWidget;
 
 Future<void> getMultipleImageInfos() async {
    var mediaData = await ImagePickerWeb.getImageInfo;
    String mimeType = mime(Path.basename(mediaData.fileName));
    html.File mediaFile =
        new html.File(mediaData.data, mediaData.fileName, {'type': mimeType});

    if (mediaFile != null) {
      setState(() {
        _cloudFile = mediaFile;
        _fileBytes = mediaData.data;
        _imageWidget = Image.memory(mediaData.data);
      });
    }
  }
   ```

With getMultipleImageInfos() you can get all three available types in one call.

## Picking Videos

To load a video as html.File do:

   ```
   html.File? videoFile = await ImagePickerWeb.getVideoAsFile();
   ```

To load a video as Uint8List do:

   ```
   Uint8List? videoData = await ImagePickerWeb.getVideoAsBytes();
   ```

Reminder: Don't use Uint8List retreivement for big video files! Flutter can't handle that. Pick bigger sized videos and high-resolution videos as html.File !

After you uploaded your video somewhere hosted, you can retreive the network url to play it.

MediaInfos

The methods getVideoInfo and getImageInfo are also available and you can use them to retreive further informations about your picked source.

### Pick multiple images

Load videos as bytes:

   ```
   List<Uint8List>? videos = ImagePickerWeb.getMultiVideosAsBytes();
   ```

Load videos as List<html.File> objects :

   ```
   List<html.File>? videoFiles = await ImagePickerWeb.getMultiVideosAsFile();
   ```


