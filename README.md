# Driver-Drowsiness-Detection
To identify the driver's drowsiness based on real-time camera image and image processing techniques. 
### Application
According to the National Highway Traffic Safety Administration, every year about 100,000 police-reported crashes involve drowsy driving. These crashes result in more than 1,550 fatalities and 71,000 injuries. The real number may be much higher, however, as it is difficult to determine whether a driver was drowsy at the time of a crash. This system detects whether a person is drowsy and alerts him/her.

### Requirements
* Download the file "shape_predictor_68_face_landmarks.dat" .

* numpy==1.15.2
* dlib==19.16.0
* pygame==1.9.4
* imutils==0.5.1
* opencv_python==3.4.3.18
* scipy==1.1.0

### Working Details:
I utilised a pre trained frontal face detector from Dlib’s library which is based on  a modification to the Histogram of Oriented Gradients in combination with Linear  SVM for classification. 

The basic thing about drowsiness detection is pretty simple. We first detect a face using dlib's frontal face detector. Once the face is detected , we try to detect the facial landmarks in the face using the dlib's landmark predictor. The landmark predictor returns 68 (x, y) coordinates representing different regions of the face, namely - mouth, left eyebrow, right eyebrow, right eye, left eye, nose and jaw. Ofcourse, we don't need all the landmarks, here we need to extract only the eye and the mouth region.
The eye region is marked by 6 coordinates. These coordinates can be used to find whether the eye is open or closed if the value of EAR is checked with a certain threshold value.
![image](https://user-images.githubusercontent.com/84140559/120076794-fd41c100-c0c4-11eb-9105-431e85ef83c9.png)

In the same way I have calculated the aspect ratio for the mouth to detect if a person is yawning. Although, there is no specific metric for calculating this, so I have taken for points, 2 each from the upper and lower lip and calculated the mean distance between them.

##### Note: Learn more about dlib at [here](http://dlib.net/ )
The pre-trained facial landmark detector inside the dlib library is used to estimate  the location of 68 (x, y)-coordinates that map to facial structures on the face. The 68  landmark output is shown in the figure below. 
Therefore, to extract the eye regions from a set of facial landmarks, we simply need to know the correct array slice indexes:


![image](https://user-images.githubusercontent.com/84140559/120077122-71c92f80-c0c6-11eb-9a0a-714acec311b5.png)

A blink is supposed to last 200-300 milliseconds.

A drowsy blink would last for 800-900 ms.

 ![image](https://user-images.githubusercontent.com/84140559/120077206-d71d2080-c0c6-11eb-94e6-e93499ae124b.png)












