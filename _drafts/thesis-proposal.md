---
title: "Thesis description"
excerpt_separator: "--"
categories:
  - Projects
tags:
  - deep learning
  - computer vision
  - multi-task
  - thesis
  - proposal
---

## *"A multi-task Deep Learning model for real-time creation of Shared Dynamic Maps"*

---

### Background <a name='Background'/>

The project is carried out at the [Prendinger Lab](http://research.nii.ac.jp/~prendinger/) of the National Institute of Informatics (NII), Japan, in the scope of the lab project _Deep Learning for Dynamic Map Creation_, which aims at creating a dynamic digital map as a basic technology for several UAV-based applications and services, such as surveillance, incl. real-time tracking, traffic estimation, delivery and others. The lab's main project is [Dronet](http://siliconmountain.jp/), a platform for multiple UAV tasking and management and Conflict Resolution for Unmaned Aerial Traffic Management (UTM). Applications building on top of it would directly benefit from such a map. One important asset of the lab is the permission of flying drones in a relatively large area, which is currently completely forbidden in Japan.

In a first phase, a Deep Learning model for Semantic Segmentation from UAV imagery was developed, making use of state-of-the-art architectures and techniques. The approach was completely frame-by-frame. The final result was a set of very deep Fully Convolutional Residual Networks models easier to train and lighter than previous models on the task semantic segmentation with a comparable accuracy. Transfer learning techniques such as fine-tuning and multi-source training and knowledge distillation from ensembles were used.

A lighter version with reduced accuracy was also trained having in mind its deployment on less powerful, memory-bound systems and real-time applications. The final inference time of the lighter model was 0.1 seconds on a Titan X GPU. In addition, with the purpose of extending the amount of data available for Semantic Segmentation of aerial view images a small dataset was collected and labeled by the team.

In a second phase, Multi Object Tracking (MOT) is to be introduced and the real-time requirement emphasized, specially taking into account that it has to run on a limited system.

---

### Objective

The degree project will happen in the area of Deep Learning for Computer Vision within the wider area of Machine Learning.

Typically, Deep Learning models focus on solving one task. If more than one task is to be solved the naive solution is to deploy two models running in parallel. The research conducted in this project will be relevant for the deployment of Deep Learning solutions in embedded systems with GPU like the Jetson TX1, which can be found on autonomous systems or portable devices. In such systems the available resources (memory, power, etc.) are not exactly the same as the ones in the powerful GPU clusters that are used to train them. Moreover, such systems typically have the extra requirement of having to work on real-time, meaning small inference times are required.

In particular, this thesis will focus on the development of a multi-task Deep Learning architecture for both Semantic Segmentation and MOT to run on a Jetson TX1 module embedded on a UAV. The output of both tasks could then be used for the creation of Shared Dynamic Maps as explained on the [Background](#Background) section.

> **_"Is it possible to leverage multi-task learning for reducing the inference time / memory requirements of multi-purpose Deep Learning solutions while not suffering significant performance drops?_**

---

### Method

Multi-task networks share a base trunk that learns a common representation for the multiple tasks and from which a number of task-specific branches emerge. The network can be trained end-to-end by defining the loss as the sum of the losses of each task. This way, most of the computation and parameters are shared between the different tasks. Moreover, previous research as well as common sense suggest that by exploiting synergies between related tasks better results can be achieved. A comprehensive method for the training of such a kind of multi-task network is explained in [UberNet: Training a Universal ConvNet](http://cvn.ecp.fr/ubernet/). The hypothesis therefore is that with multi-task training models will not only benefit in lower memory requirements and faster

The approach will be to define a multi-task architecture based on the convolutional part of an already light architecture for Object Detection (the basis for MOT) such as the Single Shot Multibox Detector, which is in turn based on a common Convnet with available pre-trained weights such as VGG16, or one from the Semantic Segmentation task and build on top with the task specific layers of the other task.

The architecture will then be validated by training on common datasets for both tasks such as VOC07+++ or MS-COCO, which include labels for both tasks, but also on datasets where only the ground truth for one of the tasks is available.

When successful, further fine-tuning on specific datasets for aerial view imagery will be performed for evaluation of the model on the target application.

How to do the MOT from the detection results is not clear yet but a simple, classical approach would be to use a Kalman or Particle Filter for motion prediction of the targets and the Kuhn-Munkres algorithm for data association. The [POI online tracker](http://www.google.com/search?q=POI:%20Multiple%20Object%20Tracking%20with%20High%20Performance%20Detection%20and%20Appearance%20Feature) based on this approach achieves state of the art results on the [MOT Challenge Dataset](https://motchallenge.net/tracker/POI).

It is worth mentioning that with this approach further tasks could be added but this will only be included if time allows it. Otherwise, it will be left for Future Work.

---

### Evaluation

The performance of the models will be evaluated not only in terms of accuracy, but also in terms of memory requirement and inference time. Results will be compared with the naive approach of running the models in parallel in order to answer the research question with empirical data. Ideally, the models will be tested both on a desktop GPU and the Jetson TX1.

Experiments to define which layers to include in the common part of the network and where to start the task-specific network can be conducted.

Saying that a system works in real-time is an application dependent affirmation. For such an application as Dynamic Map Creation, the final goal of the lab project, it can be said that a system running at around 5 fps is real-time, although it still depends on many factors, such a value will be used as a goal.

About memory requirements, a model that can run on the Jetson TX1 GPU will be considered successful, given its limited 4 GB of memory when compared to the 12 GB of the Titan X or a K40 GPUs.

Performance in terms of model accuracy will be considered relative to their single-task counterparts.

---

### News value

The innovation in this project comes from the fact that it tackles a long-lived theme in Computer Vision such as the concurrent solving of Semantic Segmentation and Detection while focusing on its applicability to real world scenarios. Such lightweight, multi-task models are needed for example for the field of Mobile Robotics if they are to become mainstream, as a drone cannot carry a big, power-hungry GPU and neither do I when I play my Augmented Reality games on my Google Tango device.

---

### Pilot study

The state of the art in terms of speed / accuracy balance of the mentioned tasks (Semantic Segmentation, Object Detection, MOT) is being reviewed in the literature study by reading the publications and analyzing / testing the code if available.

Background knowledge in the topic is difficult to define as the field is evolving really fast but basic and necessary concepts of Machine Learning, Neural Networks and specifically ConvNets and the tasks to be solved will be covered.

Also, the literature in multi-task learning from other fields than Computer Vision will be investigated to see if some idea is applicable and can help towards this project.

Some preliminary references have already been mentioned. Others include but are not limited to the next:
 - [Faster R-CNN]()
 - [R-FCN: Object Detection via Region-based Fully Convolutional Networks]()
 - [ParseNet: Looking Wider to See Better]()
 - [YOLO (You Only Look Once): Unified, real-time Object Detection]()
 - Papers defining the datasets to be used.

---

### Conditions

A powerful system with a GPU (at least a Titan X, hopefully more) is required for the training of the models. It is to be provided by NII as well as the Jetson TX1 development kit for the test. My laptop and access to the Internet for the rest.

Moreover, the rest of the Deep Learning team at NII is focusing in the creation of a new dataset for which will be also labeled with Bounding Boxes around the targets so could be used for further training the models. For such a thing we need the drones in the lab, a bunch of people to be play for us, a server to host the Labeling tool and again a bunch of people labeling the data (or a bunch of money to pay for it). It is not necessary but it is going to happen so if possible it will be used.

Some limitations have been explained while in the method but will explicitly be stated again here. No other task than MOT and Semantic Segmentation will be included in the study. No studies on which is the best trunk network for the multi-task architecture will be conducted.

The external supervisor, Prof. Prendinger, will participate in the discussion, help with practicalities and read the final report.

---

### Schedule
