import 'dart:io';

import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';

void main() => runApp(MaterialApp(
  home: MyHomePage(),
));

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  File _image;

  Future getCamera() async {
    var image = await ImagePicker.pickImage(source: ImageSource.camera);

    setState(() {
      _image = image;
    });
  }


  Future getGallery() async {
    var image = await ImagePicker.pickImage(source: ImageSource.gallery);

    setState(() {
      _image = image;
    });
  }


  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Picker Example'),
        actions: <Widget>[
          IconButton(
            icon: Icon(Icons.landscape,),
            onPressed: getGallery,
          ),
          IconButton(
            icon: Icon(Icons.refresh),
            onPressed: (){
              setState(() {
                _image = null;
              });
            },
          )
        ],
      ),
      body: Center(
        child: _image == null
            ? Text('Nothing to show.')
            : Image.file(_image),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: getCamera,
        child: Icon(Icons.camera_alt),
      ),
    );
  }
}
