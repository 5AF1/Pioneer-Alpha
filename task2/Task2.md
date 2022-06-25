# <u>**R-CNN:**</u>

## <u>Architecture and working process:</u>

R-CNN is an object detection and classifications model. The main model works in 4 steps. They are:

1. <u>Taking the image as input:</u>
   
   Here the basic image is take as input and perform normalization

2. <u>Extracting proposed regions (~2K):</u>

    Here using selective search the model extract or propose around 2k regions from the image for passing to the model for classification. 

1. <u>Compute CNN features:</u>
   
   The extracted region is passed through the CNN architecture to extract the features. The features extracted from the image are fed to the next step.

2. <u>Classify Regions:</u>
   
   Here the features are passed through an SVM to do the final classification.

A thing to note here is that all these 2k images don't get passed all at once. This search algorithm works in the following way. It first generate an initial sub-segmentation of around 2k. Then use a greedy algorithm to gradually and recursively combines similar regions into larger ones and finally combining the regions to predict the final candidate region as proposals to improve the search.

## <u>Short comings and Strong points:</u>

Though being the State of the art paper of its time and also being the first of it's kind the main drawback of this paper and the reason for the following two papers is that the model is very very slow. The prediction timing is almost 13s/image on a GPU or 53s/image on a CPU. So this is bad for real time applications. This is primarily because of the of applying the CNN almost 2k times over and over and using the Selective search algorithm.



# **<u>Fast R-CNN:</u>**

## <u>Architecture and working process:</u>

How this model works is instead of passing only the proposed region to the CNN for feature detection, the entire image is passed to create a larger feature map of the entire image. Now instead of passing the proposed region to the CNN the proposed Region Of Interest (ROI) is projected on to the CNN extracted feature map to be passed to the next classification layer. Now during the pass to the classification layer the CNN features will have different sized output. But the final fully connected classification layer needs takes a fixed sized array as input. To solve this ROI pooling layers are used to bring the feature map to shape.

## <u>Short comings and Strong points:</u>

The main strong point of this paper is that it solved one of the main two problems of R-CNN that is repeated application of the CNN. Here instead only once is the CNN model being applied. Performance increases form 13 s/image to almost 2-3 s/image. But the main bottle neck now is the Selective search algorithm.



# **<u>Faster R-CNN:</u>**

## <u>Architecture and working process:</u>

THe main change in this model is that the Selective search algorithm is replaced with Region Proposal Networks(RPN). Here the feature map from the primary CNN is passed to a CNN in the RPN. This CNN predicts the bonding box and the if an object is present in the region or not. Everything else is almost the same. 

## <u>Short comings and Strong points:</u>

The Faster R-CNN model solved all the primary problems of the first if its type the R-CNN model reducing the computation time to almost real time with a performance increases form 2s/image to almost 0.2s/image. The only shortcoming that are immediately visible is that the model still theoretically looks at the image multiple times via the RPN. Although RPN is much faster it still needs to look at the image multiple times. To solve this problem the next State of the art model was the YOLO models. These models only look at the image once thus reducing the processing time of the overall models in general.






