# Seting up Object Detection

### Install all Librarys
install the TF object detection library
```
git clone https://github.com/tensorflow/models.git
```
install the use_protobuf, and the xml_to_csv, and generate_tfrecord python files from this repository. After copy them into your models/research/object_detection folder
```
git clone https://github.com/ArturK123/TFLite.git
```

### Get Prtobuf
copy the protobuf executable into your models/releases folder, and delete the rest of protobuf

|Link|Platform|Release|
|-------|----|--------|
|https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protoc-3.14.0-osx-x86_64.zip | MacOS | 14.0 |
|https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protoc-3.14.0-win64.zip | WIN 64 | 14.0 |
|https://github.com/protocolbuffers/protobuf/releases/download/v3.14.0/protoc-3.14.0-win32.zip | WIN 32 | 14.0 |

### Compile Protobuf
Go into your models directory
```
cd <complete path>/models/research
```
compile the protobuf
```
python use_protobuf.py <complete path>/models/research/ <complete path>/models/research/protoc
```
To test if this worked run
```
python object_detection/builders/model_builder_tf2_test.py
```
If it has compiled sucsessfully then you will see the following
```
[       OK ] ModelBuilderTF2Test.test_create_ssd_models_from_config
[ RUN      ] ModelBuilderTF2Test.test_invalid_faster_rcnn_batchnorm_update
[       OK ] ModelBuilderTF2Test.test_invalid_faster_rcnn_batchnorm_update
[ RUN      ] ModelBuilderTF2Test.test_invalid_first_stage_nms_iou_threshold
[       OK ] ModelBuilderTF2Test.test_invalid_first_stage_nms_iou_threshold
[ RUN      ] ModelBuilderTF2Test.test_invalid_model_config_proto
[       OK ] ModelBuilderTF2Test.test_invalid_model_config_proto
[ RUN      ] ModelBuilderTF2Test.test_invalid_second_stage_batch_size
[       OK ] ModelBuilderTF2Test.test_invalid_second_stage_batch_size
[ RUN      ] ModelBuilderTF2Test.test_session
[  SKIPPED ] ModelBuilderTF2Test.test_session
[ RUN      ] ModelBuilderTF2Test.test_unknown_faster_rcnn_feature_extractor
[       OK ] ModelBuilderTF2Test.test_unknown_faster_rcnn_feature_extractor
[ RUN      ] ModelBuilderTF2Test.test_unknown_meta_architecture
[       OK ] ModelBuilderTF2Test.test_unknown_meta_architecture
[ RUN      ] ModelBuilderTF2Test.test_unknown_ssd_feature_extractor
[       OK ] ModelBuilderTF2Test.test_unknown_ssd_feature_extractor
----------------------------------------------------------------------
Ran 20 tests in 91.767s

OK (skipped=1)
```
# Get The data
if you already have the images labeled then skip this step. Otherwise you would want to do the folowing
```
cd <home directory>
```
After this to install the img labeling software type
```
pip install labelimg
```
now you should be able to just type, and a new window should open
```
labelimg
```
Click on the open dir button, and select your image path
<p align="left">
  <img src="Screen Shot 2021-02-12 at 6.08.42 PM.png">
</p>
Now when you press W you will be able to draw boxes. After you are done labeling all your images make sure your .xml files are inside the same directory as your .png files. Now go to the object detection folder.

```
cd <complete path>/models/research/object_detection/
```

after that you want to create some folders for your images to be in

```
mkdir images
```

```
cd images
```

```
mkdir test
```

```
mkdir train
```
Now transport some of your images with the coresponding .xml files to the test and train folders inside models/research/object_dedection/images. When you are done run the python xml to csv file in your object detection directory
```
cd <complete path>/models/research/object_detection/
```

```
python xml_to_csv.py
```

### Create TFrecord 
open the generate_tfrecord.py file and change the following lines with your class names and delete any rows if you dont have as much classes
```
def class_text_to_int(row_label):
    if row_label == 'Raspberry_Pi_3':
        return 1
    elif row_label == 'Arduino_Nano':
        return 2
    elif row_label == 'ESP8266':
        return 3
    elif row_label == 'Heltec_ESP32_Lora':
        return 4
    else:
        return None
```

# Converting TensorFlow Models to TensorFlow Lite

### Go To The Models Directory

```
cd /Users/<complete the path>/models/research/object_detection/
```
### Export as TFLite model
```
python export_tflite_graph_tf2.py --pipeline_config_path models\my_ssd_mobilenet_v2_fpnlite\pipeline.config --trained_checkpoint_dir models\my_ssd_mobilenet_v2_fpnlite --output_directory exported-models\my_tflite_model
```

### Get The TFLite Model

```
python convert-to-tflite.py
```
