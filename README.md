# Object Detection Basics and Concepts
----

## Object Detection
-	Finding an object in certain image using a bounding box.
-	Take image as a input and compute bounding box and list of class of object as an output.
-	Also the predicted class and its confidence level corresponding to the bounding box.

### IOU (Intersection Over Union)
-	Measurement that shows how Ground Truth and Predicted Value computed by model overlapped.
-	Higher IOU value means greater detection precision; This is directly related to the performance of model.

### NMS (Non-Maximum Suppression)
-	A process of deleting an bounding boxes that are not having a maximum value. Remain only the one which has a greatest value.

Steps:
1.	Sort boxes using a probability and takes box that has highest probability.
2.	Calculate IOU of every boxes.
3.	Remove a box that has a value over certain threshold.

### Evaluate Model Performance
	True Positive (TP): Test whether predicted and actual boxes matched.
	False Positive (FP): Test whether predicted and actual boxes are not matched.
	False Negative (FN): Test whether classification ad its corresponding prediction are not matched.

Measurements
	Precision: TP/(TP+FP)
	Recall: TP/(TP+FN)

Note: 
> - If model prediction is based on unstable feature of object, FP will be increased so that the general precision will be dropped.
> - If the model itself is extremely strict, the FN will be increased, so that recall will be dropped.


### Precision Recall Curve
-	Graph that visualize an precision and recall of each Confidence threshold.
-	Precision and Recall will be differ based on threshold T.
> 1.	Prediction below the threshold T will be removed.?
> 2.	If T is closer to 1, the precision will be high, but the recall will be low. (We can say the model itself is very strict)
> 3.	If T is closer to 0, the precision will be low, but the recall will be high. (Increased False Positive)

### AP & mAP
-	Represent an area below the curve.
-	Always having a value between 0 to 1. (1 by 1 square)
-	It will offer an performance data of model towards to a single class.
-	mAP (Mean Average Precision) is used to get a localized value.
Ex: If dataset has a 10 classes, AP of each class will be calculated and using those calculated AP values, mAP will be calculated to get a value of entire model’s performance.

### Dataset
-	VOC Dataset
Trained and Verified data: 11,530
ROI Annotation: 27,450

-	COCO Dataset
Common Object in Context
200,000 Images
Over 500,000 annotation exist in 80 different categories.

----
## Object Detection Method
-	R-CNN
> - Rich Feature hierarchies for accurate object detection and semantic segmentation.
> - Using Region Proposal that overcome the disadvantage of sliding window technique.
> - Still quite slow.
-	Faster R-CNN
> - Towards Real-Time Object Detection with Region Proposal Networks.
> - RPN (Region Proposal Network) + Fast R-CNN
> - Even train the RPN.
> - For region Proposal, an Anchor Box concept has been introduced.
> - Higher precision and speed compare to Fast R-CNN.
> - Still need two steps (1. region proposal, 2. anchor box), therefore, it is hard to implement in real-time basis, which needs at least 30 to 40 fps.
-	 YOLO
> - Similar to RetinaNet, YOLO also introduce an FPN to increase precision.

### YOLO (You Look Only Once)
-	One of the fastest object detection algorithms.
-	Using 256*256 sized image.
-	It is still hard to detect a relatively small sized object. 

Architecture
> - Based on Backbone model
> - It has three stages for different scaled object.
> - YOLO Hierarchy Output:
width * height * M Matrix
(M = B * (C + 5))
B: Number of bounding boxes in each gride cell.
C: Number of class.

Objectiveness Score: Probability that object is in bounding box.

- Anchor Box
> - Prior Box
> - Neural Network is required since the process of fit the closest anchor box and refine the box size.
