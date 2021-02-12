# Seting up Object Detection

### Install Object Detection Library
```
git clone x
```

### Get Prtobuf
copy the protobuf executable into your models/releases folder, and delete the rest of protobuf

|Link|Platform|Release|
|-------|----|--------|
|https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protoc-3.14.0-osx-x86_64.zip | MacOS | 14.0 |
|https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protoc-3.14.0-win64.zip | WIN 64 | 14.0 |
|https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protoc-3.14.0-win32.zip | WIN 32 | 14.0 |

# Converting TensorFlow Models to TensorFlow Lite

### Go To The Models Directory

```
cd /Users/<complete the path>/models/object_detection/
```
### Export as TFLite model
```
python export_tflite_graph_tf2.py --pipeline_config_path models\my_ssd_mobilenet_v2_fpnlite\pipeline.config --trained_checkpoint_dir models\my_ssd_mobilenet_v2_fpnlite --output_directory exported-models\my_tflite_model
```

### Get The TFLite Model

```
python convert-to-tflite.py
```
