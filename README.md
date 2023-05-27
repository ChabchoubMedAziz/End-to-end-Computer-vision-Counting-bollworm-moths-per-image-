# End-to-end-Computer-vision-Counting-bollworm-moths-per-image-
## About
Wadhwani AI has developed a mobile app that allows farmers to take photographs of trap catches and receive recommendations based on machine-generated counts of pests in those images. To produce such counts, the app contains an object detection model trained to identify two types of bollworms.
This competition objective is to use our training data – data captured by farmers and farm extension workers since 2018 – to build models that accurately count the number of  2 type of bollworms present in the image.
(https://zindi.africa/competitions/wadhwani-ai-bollworm-counting-challenge).

  ## Solution Overview:
Our training data contatins Bbox of detecting bollworms for that we tried two approaches:

• **First approach** : Build Object detection model using Faster-RCNN to detect bollworm boxes and then count the bounding boxes for every type.

• **Second approach** : Build image classifier so  we can detecte images without bollworms and reduce Flase Positive:

* Model: densenet201 image size 500
* Batch size: 8
* Epochs: 4
* Optimizer: SGD 
* Augmentations: Hflip + Vflip + Mosaic + Mixup
* Loss: CELoss

Then a regression model where we used only images classified as they got bollworms :
* Model: EfficientNetB6 image size 500 /We unfreeze the top 20 layers while leaving BatchNorm layers frozen/
* Batch size: 16
* Epochs: 20
* Optimizer: Adam
* Loss: MeanSquaredError
