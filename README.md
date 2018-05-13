# Traffic-light-classifier


## 1. Setup the environment (Tensorflow->object_detection on Ubuntu 16.04)

The detailed instractions on how to install Tensorflow can be found at https://www.tensorflow.org/install/
This setup though is about Linux only so we can go directly to https://www.tensorflow.org/install/install_linux
We can pick up the mechanism by which we install tensorflow from the following list: virtualenv, pip, docker, anaconda.
Our choise is virtualenv as it is the recomended mechanism. 

The following instraction will cover Python 3.x only (if you are interested in having it with Python 2.7 then go here: https://www.tensorflow.org/install/install_linux

1) Install pip and virtualenv by issuing the following command for python 3.x:
```
$ sudo apt-get install python3-pip python3-dev python-virtualenv
```
2) Create virtualenv environment by issuing the following command:
```
$ virtualenv --system-site-packages -p python3 ~/tensorflow
```
3) In case of bash activate virtualenv environment by issuing the following command:
```
$ source ~/tensorflow/bin/activate
```
4) Ensure pip ≥8.1 is installed:
```
(tensorflow)$ easy_install -U pip
```
5) In order to install tensorflow with GPU support issue the following command:
```
(tensorflow)$ pip3 install --upgrade tensorflow=1.3
```
6) Verify if tensorflow installed correctly by issuing the following command:
```
(tensorflow)$ python check.py
```
The rest of the procedure will be based on the object detection model installation instruction (for details see here: https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md)

7) Install all prerequisities for running object detection models: 
```
(tensorflow)$ sudo apt-get install protobuf-compiler python-pil python-lxml python-tk
(tensorflow)$ pip install matplotlib
```
8) Clone object detection models repo
```
(tensorflow)$ git clone https://github.com/tensorflow/models.git
```
9) Get back to the following commit:
```
commit f7e99c0873c033832529f18e6596a4527db606a1
Author: Vivek Rathod <rathodv@google.com>
Date:   Fri Nov 17 20:32:43 2017 -0800
update broken ssd models in the zoo along with notebook.
by issuing the following command
```
```
(tensorflow)$ git checkout f7e99c0
```
(suggestion from here: https://github.com/alex-lechner/Traffic-Light-Classification#troubleshooting)

10) Compile protobuf libraries as the Tensorflow Object Detection API uses Protobufs to configure model and training 
parameters.
```
From tensorflow/models/research/
(tensorflow)$ protoc object_detection/protos/*.proto --python_out=.
```
11) Append tensorflow/models/research and slim paths to PYTHONPATH by issuing the following command: 
```
From tensorflow/models/research/
(tensorflow)$ export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim
```
12) Verify if Object Detection API works by issuing the following command:
```
(tensorflow)$ python object_detection/builders/model_builder_test.py
```
## 2. Setup AWS
## 3. Setup Jupyter in AWS
https://medium.com/@alexjsanchez/python-3-notebooks-on-aws-ec2-in-15-mostly-easy-steps-2ec5e662c6c6

## 4. Train model
https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md
https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/configuring_jobs.md
http://download.tensorflow.org/models/object_detection/ssd_inception_v2_coco_2017_11_17.tar.gz
http://download.tensorflow.org/models/object_detection/rfcn_resnet101_coco_2018_01_28.tar.gz

## 5. Evaluate model
## 6. TensorBoard
## 7. Freeze model

Note the frozen models are split because they were too big to push them on github with normal sizes:
The following command was used to make them split:
```
split --bytes=40M model.pb model.pb_split
```
In order to put them together you can use cat:
```
cat model.pb_split* > model.pb
```
 
