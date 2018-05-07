# Paper: Are mid-air dynamic gestures applicable to user identification?
<br>  This project mainly provides the source codes and data sets for our paper：H. Liu et al., Are mid-air dynamic gestures applicable to user identification? Pattern Recognition Letters (2018), https://doi.org/10.1016/j.patrec.2018.04.026.  </br>
<br>  We will briefly introduce the role of each document from the following directions so that readers can replicate our experiments.</br>
* **Source data introduction**
* **Training and verification set**
* **The proposed Bi-GRU based biometric framework**
* **Experiment details**
## 1 Source data introduction #
<br>In this experiment, we used Microsoft Kinect v2 sensor for data acquisition. We used VS2013 and Kinect SDK v2 to develop a data acquisition program that can simultaneously capture color image data, depth image data, and human body 25 joint data in the scene.In this paper, we mainly use human body joint data. We designed three types of dynamic gestures: right hand drawing 'O', left hand drawing 'V' and both hand 'Clapping'. 60 volunteers were invited to participate in the collection of data sets. Each individual was asked to draw three types of gestures in 'O', 'V', 'Clapping' order 20 times. The relevant data sets we provide are in the '*./SkeletonData*' folder, and the specific data storage format is as follows:</br>
<br>**./SkeletonData/Person_\*/Round_\*/**</br>
<br>Where 'Person_\*' represents the 60 volunteers' identification labels, and 'Round_\*' represents the order of 20 rounds' data collection for each individual. Finally, the joint data of each round is saved in the following two TXT files:</br>
* Skeleton.txt: 25 body joint 3D coordinates (x, y, z) data stored by format x1, y1, z1, x2, y2, z2, ..., x25, y25, z25 each rows.
* Label.txt: The numbers in each line indicates the start and end frames of the gesture 'O', 'V' and 'Clapping', respectively.
## 2 Training and verification set #
<br>Before training our proposed gesture-based biometric framework, the valid training datasets and validation datasets should be selected. In section 2.1 and 2.2 of the paper we provided the data preprocessing methods to reduce joint jitter and body translation interference. In our experiment, we randomly selected 14 rounds of samples from 20 rounds' samples of each individual for training set, and the remaining 6 rounds' samples for verification set. Each gesture sequence is preprocessed and scaled to the same length of 65 frames. The complete code is given in '***train_ver_data_preprocess.py***'. </br>
<br>By using this program, effective training and verification data can be generated, and the gesture type label and user identity label of each gesture sample are recorded. Here we provide the generated training and validation data set in the '*./LabeledData*' folder and give a brief introduction to their formats. We use the gesture 'V' as an example for the other gesture types have the same format.</br>
* ./LabeledData/TrainingData/gesture_V/skeleton.txt: the effective part of the gesture V, each row represents a 65*25*3 dimension gesture sequence.
* ./LabeledData/TrainingData/gesture_V/userID.txt: the number of each line represents the user identity label of the corresponding line of gesture data in file 'skeleton.txt'.
* ./LabeledData/TrainingData/gesture_V/gestureID.txt: the number of each line represents the gesture type label of the corresponding line of gesture data in file 'skeleton.txt'.

## 3 The proposed Bi-GRU based biometric framework #