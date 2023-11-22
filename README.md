# Image Segmentation with U-Net

This repository is the implementation of building of U-Net, a type of CNN designed for quick, precise image segmentation, and using it to predict a label for every single pixel in an image. In this case, an image from a self-driving car dataset.

This type of image classification is called semantic image segmentation. It's similar to object detection in that both ask the question: "What objects are in this image and where in the image are those objects located?," but where object detection labels objects with bounding boxes that may include pixels that aren't part of the object, semantic image segmentation allows you to predict a precise mask for each object in the image by labeling each pixel in the image with its corresponding class.

<img src="images/carseg.png" style="width:900px;height:400px;">


## U-Net
U-Net, named for its U-shape, was originally created in 2015 for tumor detection, but in the years since has become a very popular choice for other semantic segmentation tasks. 

U-Net builds on a previous architecture called the Fully Convolutional Network, or FCN, which replaces the dense layers found in a typical CNN with a transposed convolution layer that upsamples the feature map back to the size of the original input image, while preserving the spatial information. This is necessary because the dense layers destroy spatial information (the "where" of the image), which is an essential part of image segmentation tasks. An added bonus of using transpose convolutions is that the input size no longer needs to be fixed, as it does when dense layers are used. 

Unfortunately, the final feature layer of the FCN suffers from information loss due to downsampling too much. It then becomes difficult to upsample after so much information has been lost, causing an output that looks rough. 

U-Net improves on the FCN, using a somewhat similar design, but differing in some important ways.  Instead of one transposed convolution at the end of the network, it uses a matching number of convolutions for downsampling the input image to a feature map, and transposed convolutions for upsampling those maps back up to the original input image size. It also adds skip connections, to retain information that would otherwise become lost during encoding. Skip connections send information to every upsampling layer in the decoder from the corresponding downsampling layer in the encoder, capturing finer information while also keeping computation low. These help prevent information loss, as well as model overfitting. 

<img src="images/unet.png" style="width:9000px;height:450px;">
<caption><center> <u><b> Figure 2 </u></b>: U-Net Architecture<br> </center></caption>


### Sample outputs

Some of the sample outputs of the model look like the following:

<img src="images/Sample Outputs.png" style="width:900px;height:450px;">

**NOTE:** You can get the model structure in (outputs.py)[outputs.py] file and the implementation in the (jupyter notebook)[Image_Segmentation_with_U-Net.ipynb].
