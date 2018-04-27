VisDrone2018-MOT Benchmark Toolkit 

===================================================================
Introduction
===================================================================

This is the documentation of the VisDrone2018 competitions development kit for multiple object tracking (MOT) challenge.

This code library is for research purpose only, which is modified based on the MOTChallenge [1] and PASCAL VOC [2] platform. 
The code is tested on the Windows 10 and macOS Sierra 10.12.6 systems, with the Matlab 2013a/2014b/2016b/2017b platforms.

If you have any questions, please contact us (email:tju.drone.vision@gmail.com).

===================================================================
Citation
===================================================================

If you use our toolkit or dataset, please cite our paper as follows:

@article{zhuvisdrone2018,

    title={Vision Meets Drones: A Challenge},

    author={Zhu, Pengfei and Wen, Longyin and Bian, Xiao and Haibin, Ling and Hu, Qinghua},

    journal={arXiv preprint:1804.07437},

    year={2018}

}

===================================================================
Dataset
===================================================================

For MOT competition, there are three sets of data and labels: training data, validation data, 
and test-challenge data. There is no overlap between the three sets. 

                                                          Number of snippets

    Dataset                           Training              Validation            Test-Challenge
    ------------------------------------------------------------------------------------------------
    Multiple object tracking           56 clips               7 clips                16 clips
                                     24,201 frames          2,819 frames           6,333 frames
    ------------------------------------------------------------------------------------------------
    
The challenge requires a participating algorithm to locate the target bounding boxes in each image. The objects to be detected are of various types including pedestrians, 
cars, buses, and trucks. We manually annotate the bounding boxes of different objects and ignored regiones in each image. Annotations on the training and validation sets 
are publicly available.

The link for downloading the data can be obtained by registering for the challenge at

    http://www.aiskyeye.com/
 
===================================================================
Evaluation routines
===================================================================

The notes for the folders:
* main functions
	* evalMOT.m is the main function to evaluate your tracker
	      -put the source codes in ./trackers/ according to the source codes of GOG tracker
        -modify the dataset path and result path  
        -use "isSeqDisplay" to display the groundtruth and detections
        -use "isNMS" and nmsThre to conduct NMS  
        -select the evaluated task, i.e, Task4a without detection input, Task4b with detection input
        
  * evaluateTrackA.m is the main function to evaluate your tracker using the measures in Task4a without prior detection.   
  
  * evaluateTrackB.m is the main function to evaluate your tracker using the measures in Task4b with the Faster RCNN detection.    
 
===================================================================
MOT submission format
===================================================================

Submission of the results will consist of TXT files with one line per predicted object.It looks as follows:

<frame_index>,<target_id>,<bbox_left>,<bbox_top>,<bbox_width>,<bbox_height>,<score>,<object_category>,<truncation>,<occlusion>

Position	  Name	                                      Description
   1	  <frame_index>	      The frame index of the video frame
   2	   <target_id>	      In the DETECTION result file, the identity of the target should be set to the constant -1.
   							  In the GROUNDTRUTH file, the identity of the target is used to provide the temporal corresponding relation of the bounding boxes in different frames.
   3	   <bbox_left>	      The x coordinate of the top-left corner of the predicted bounding box
   4	   <bbox_top>	      The y coordinate of the top-left corner of the predicted object bounding box
   5	  <bbox_width>	      The width in pixels of the predicted object bounding box
   6	  <bbox_height>	      The height in pixels of the predicted object bounding box
   7	     <score>	      The score in the DETECTION file indicates the confidence of the predicted bounding box enclosing an object instance.
                              The score in GROUNDTRUTH file is set to 1 or 0. 1 indicates the bounding box is considered in evaluation, while 0 indicates the bounding box will be ignored.
   8	<object_category>	  The type of object annotated (0~11: ignored regions, pedestrian, people, bicycle, car, van, truck, tricycle, awning-tricycle, bus, motor, others)
   9	   <truncation>	      The score in the DETECTION file should be set to the constant -1.
                              The score in the GROUNDTRUTH file indicates the degree of object parts appears outside a frame (i.e., no truncation = 0 (truncation ratio 0%), and partial truncation = 1 (truncation ratio 1% �� 50%)).
  10	   <occlusion>	      The score in the DETECTION file should be set to the constant -1.
                              The score in the GROUNDTRUTH file indicates the fraction of objects being occluded (i.e., no occlusion = 0 (occlusion ratio 0%), partial occlusion = 1 (occlusion ratio 1% �� 50%), and heavy occlusion = 2 (occlusion ratio 50% ~ 100%)).

The sample submission of GOG tracker can be found in our website.

====================================================================
References
====================================================================
[1] A. Milan, L. Leal-Taixe, K. Schindler, D. Cremers, S. Roth, and I. Reid, "Multiple Object Tracking Benchmark 2016", https://motchallenge.net/results/MOT16/.
[2] E. Park, W. Liu, O. Russakovsky, J. Deng, F.-F. Li, and A. Berg, "Large Scale Visual Recognition Challenge 2017", http://imagenet.org/challenges/LSVRC/2017

===================================================================
Version history
===================================================================
1.0.0 - Apr 27, 2018
  - initial release