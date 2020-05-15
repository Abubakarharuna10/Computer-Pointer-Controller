# Computer Pointer Controller

# introduction of this  project

Computer Pointer Controller app is used to controll the movement of mouse pointer by the direction of eyes and also estimated pose of head. This app takes video as input and then app estimates eye-direction and head-pose and based on that estimation it move the mouse pointers.


## Project Set Up and Installation

You need to install openvino successfully
See this [guide](https://docs.openvinotoolkit.org/latest/_docs_install_guides_installing_openvino_linux.html) for installing openvino.

## Step 1
Clone the repository:- https://github.com/abubakarharuna10/Computer-Pointer-Controller

## Step 2
Initialize the openVINO environment:-
```
source /opt/intel/openvino/bin/setupvars.sh -pyver 3.5
```

## Step 3

Download the following models by using openVINO model downloader:-

1. Face Detection Model**
```
python /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "face-detection-adas-binary-0001"
```
2. Facial Landmarks Detection Model**
```
python /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "landmarks-regression-retail-0009"
```
3. Head Pose Estimation Model**
```
python /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "head-pose-estimation-adas-0001"
```
4. Gaze Estimation Model**
```
python /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "gaze-estimation-adas-0002"


## Demo video

(https://img.youtube.com/vi/qR9rQQ4wiMQ/0.jpg)


## Documentation

1. [Face Detection Model](https://docs.openvinotoolkit.org/latest/_models_intel_face_detection_adas_binary_0001_description_face_detection_adas_binary_0001.html)
2. [Facial Landmarks Detection Model](https://docs.openvinotoolkit.org/latest/_models_intel_landmarks_regression_retail_0009_description_landmarks_regression_retail_0009.html)
3. [Head Pose Estimation Model](https://docs.openvinotoolkit.org/latest/_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html)
4. [Gaze Estimation Model](https://docs.openvinotoolkit.org/latest/_models_intel_gaze_estimation_adas_0002_description_gaze_estimation_adas_0002.html)


## Benchmarks

Benchmark results of the model.
model loading time, input/output processing time, model inference time etc.


### FP32

**Inference Time** <br/> 
![inference_time_fp32_image](media/inference_time_fp32.png "Inference Time")

**Frames per Second** <br/> 
![fps_fp32_image](media/fps_fp32.png "Frames per Second")

**Model Loading Time** <br/> 
![model_loading_time_fp32_image](media/model_loading_time_fp32.png "Model Loading Time")

### FP16

**Inference Time** <br/> 
![inference_time_fp16_image](media/inference_time_fp16.png "Inference Time")

**Frames per Second** <br/> 
![fps_fp16_image](media/fps_fp16.png "Frames per Second")

**Model Loading Time** <br/> 
![model_loading_time_fp16_image](media/model_loading_time_fp16.png "Model Loading Time")

### INT8
**Inference Time** <br/> 
![inference_time_int8_image](media/inference_time_int8.png "Inference Time")

**Frames per Second** <br/> 
![fps_int8_image](media/fps_int8.png "Frames per Second")

**Model Loading Time** <br/> 
![model_loading_time_int8_image](media/model_loading_time_int8.png "Model Loading Time")


## Results

I have run the model in 5 diffrent hardware:-
1. Intel Core i5-6500TE CPU 
2. Intel Core i5-6500TE GPU 
3. IEI Mustang F100-A10 FPGA 
4. Intel Xeon E3-1268L v5 CPU 
5. Intel Atom x7-E3950 UP2 GPU

Also compared their performances by inference time, frame per second and model loading time.

As we can see from above graph that FPGA took more time for inference than other device because it programs each gate of fpga for compatible for this application. It can take time but there are advantages of FPGA such as:-
- It is robust meaning it is programmable per requirements unlike other hardwares.
- It has also longer life-span.

GPU proccesed more frames per second compared to any other hardware and specially when model precision is FP16 because GPU has severals Execution units and their instruction sets are optimized for 16bit floating point data types.

- We have run models with different precision, but precision affects the accuracy. Mdoel size can reduce by lowing the precision from FP32 to FP16 or INT8 and inference becomes faster but because of lowing the precision model can lose some of the important information because of that accuracy of model can decrease. 

- So when you use lower precision model then you can get lower accuracy than higher precision model.

## Stand Out Suggestions
This is where you can provide information about the stand out suggestions that you have attempted.

### Async Inference
If you have used Async Inference in your code, benchmark the results and explain its effects on power and performance of your project.

### Edge Cases
1. If for some reason model can not detect the face then it prints unable to detect the face and read another frame till it detects the 
   face or user closes the window.

2. If there are more than one face detected in the frame then model takes the first detected face for control the mouse  pointer.


