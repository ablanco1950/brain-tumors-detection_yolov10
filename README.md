# brain-tumors-detection_yolov10
From dataset https://universe.roboflow.com/test-svk7h/brain-tumors-detection/dataset/2  a model is obtained, based on yolov10 to indicate tumors in images of brains. 

=== Installation:

 Download all project datasets to a folder on disk.

Install yolov10 (if not yet installed) following the instructions given at: https://blog.roboflow.com/yolov10-how-to-train/ 

which may be reduced to !pip install -q git+https://github.com/THU-MIG/yolov10.git

If you already have ultralytics installed, it would be advisable to upgrade ultralytics, unless you have applications based on yolov10 without updating, which could be affected by the update. In that case is better install de project in a separate environment.

For that you must have an upgraded version of ultralytics and the proper version of lap, for that:

inside conda in the scripts directory of the user environment:

python pip-script.py install --no-cache-dir "lapx>=0.5.2"

upgrade ultralytics:

python pip-script.py install --upgrade ultralytics

And download from https://github.com/THU-MIG/yolov10/releases the yolov10n.pt model. In case this operation causes problems, these files are attached with the rest of the project files.

Unzip the test.zip folder

Some zip decompressors duplicate the name of the folder to be decompressed; a folder that contains another folder with the same name, should only contain one. In these cases it will be enough to cut the innermost folder and copy it to the project folder.

=== Test:

Execute:

Evaluate_brain-tumors-detection_Yolov10.py

that evaluate the 100 test images downloaded from 

https://universe.roboflow.com/test-svk7h/brain-tumors-detection/dataset/2

The program comes with a model optimized last19epoch100Detect3errors.pt

The images are presented on the screen with a red box , or several red boxes, indicating the predictions, with a green box the label of the image that must indicate te true position (labeled), also appears the confidence of predicted tumors.

All images have predicted tumors (is important in this case to detect in spite of been a false detection)

All predictions match the labels (more or less) except in three cases where they do not match (images: y719, y751, y774, y777 and y783): 95% Precision

In 11 cases, in addition to the tumor prediction, several additional tumors, no labeled, are detected (images y713, y721,  y734, y736, y736, y741, y746, y761, y777, y790 and y y798): 89%  Recall

The above success rates are actually higher, since there may be several detected and several labeled tumors in an image, it has been considered that only one has not been detected to consider the entire image with a detection error, even if in other tumors in the same image the detection coincides with the labels.

The model has been obtained with a MAP50 of 0.831 and MAP50-95 of 0.548 corresponding to epoch 19 of the training (see log in the attached LOG.txt file, in which MAP50 values ​​higher than 0.91 are obtained)



=== Training

The project comes with an optimized model: last19epoch100Detect3errors.pt

To obtain this model, the following has been executed:

 Download de file

 https://universe.roboflow.com/test-svk7h/brain-tumors-detection/dataset/2

If you do not have a roboflow user key, you can obtain one at
https://docs.roboflow.com/api-reference/authentication

After downloading the dataset, a folder named Brain-Tumors-Detection-2 is created which must be moved to the project folder

Execute:

 Train_brain-tumors-detection_Yolov10.py

This program has been adapted from

 https://medium.com/@huzeyfebicakci/custom-dataset-training-with-yolov10-a-deep-dive-into-the-latest-evolution-in-real-time-object-ab8c62c6af85

It assumes that the project is located in the folder 
“C:\brain-tumors-detection_yolov10”, 

otherwise the assignment must be changed by modifying line 22 .

The parameter multi_scale has been changed to true.

also uses the .yaml file:

data.yaml

In data.yaml the absolute addresses of the project appear assuming that it has been installed on disk C:, if it has another location these absolute addresses will have to be changed.

=========
Conclusions:

The results obtained with this project are good and should also be attributed to the set of images in the dataset, all of which come with the same size 640x640 (that of yolov10) without the need for them to be high resolution (just check the size of the images), and correct labeling is also observed.

A test with the first 6 images of  100 images that make up the test file, in red the predicted box, in green the labeled box

![Figure 1](https://github.com/ablanco1950/brain-tumors-detection_yolov10/blob/main/Figure_1.png)
![Figure 2](https://github.com/ablanco1950/brain-tumors-detection_yolov10/blob/main/Figure_2.png)
![Figure 3](https://github.com/ablanco1950/brain-tumors-detection_yolov10/blob/main/Figure_3.png)
![Figure 4](https://github.com/ablanco1950/brain-tumors-detection_yolov10/blob/main/Figure_4.png)
![Figure 5](https://github.com/ablanco1950/brain-tumors-detection_yolov10/blob/main/Figure_5.png)
![Figure 6](https://github.com/ablanco1950/brain-tumors-detection_yolov10/blob/main/Figure_6.png)

=== References

 https://universe.roboflow.com/test-svk7h/brain-tumors-detection/dataset/2

https://medium.com/@huzeyfebicakci/custom-dataset-training-with-yolov10-a-deep-dive-into-the-latest-evolution-in-real-time-object-ab8c62c6af85 

https://github.com/ablanco1950/Fracture.v1i_Reduced_YoloFromScratch

https://github.com/ablanco1950/bone-fracture-7fylg_Yolov10

https://github.com/ablanco1950/BrainTumor_sagittal_t1wce_Yolov10

https://github.com/ablanco1950/PointOutWristPositiveFracture_on_xray

https://github.com/ablanco1950/Kidney_Stone-Yolov10

