
#Windows exe of caffe to extract deep learning features
##### You can download the exe and related dlls here: [caffe-extract-deep-feat](http://pan.baidu.com/s/1c2v7OPU).

##### The code is here: [extract_feat.cpp](https://github.com/jasonustc/caffe-multigpu/blob/tools/tools/extract_feat.cpp), [feat_extrator.hpp](https://github.com/jasonustc/caffe-multigpu/blob/tools/include/caffe/util/feat_extractor.hpp). 

#### **Want to build the exe by yourself?**
You can find the windows version of caffe project at [Caffe Windows]( https://github.com/jasonustc/caffe-multigpu/tree/tools).

####**Prerequisites**
- Windows-64 bit
- Please download the image net DCNN model file (e.g. AlexNet, CaffeNet, VGG, GoogleNet) and corresponding deployed net definition file and imagenet_mean file (if needed) from online resources, then put them into the same folder with the exe (in current folder, we take AlexNet as an example) .

####**Usage**
Please remember to keep all the files or sub folders in the same folder with the exe.
You have 3 choices to use this exe, first please open the cmd window and input one of the following commands:

- ExtractDeepFeat.exe [flags] imagePath layame
- ExtractDeepFeat.exe [flags] indexFilePath layerName
- ExtractDeepFeat.exe [flags] imageFolderPath layerName

Flags including:
-  -net_file:  the net definition file. The net must include an input layer named as "data" with a type "Input". For the input layer: net input shapes should be set in input_param; reshape parameters should be set in image_data_param; transformation parameters should be set in transform_param.
- -model_file: the corresponding trained caffemodel file.
- -feat_file:  the file path to store features of all the images. if not set, features will be saved independently into "xxx.jpg.feat".
- -mode: "GPU" or "CPU", default as CPU. For GPU mode, cuda toolkit 7.5 is needed.
- -l2_norm: true or false, if l2 normalization of feature is needed.
- -sqrt: true or false, if square root of feature is needed.

You can run ExtractDeepFeat.exe in cmd and see more usage details.
    
####**Input**
- **imagePath**:  the absolute path of your image.
- **indexFilePath**: the index file of your images, which should be in txt format (with ".txt" extension" and one image path per line.
- **imageFolderPath**: absolute path of your image folder, it will scan all the images in this folder and its sub folders.
- **layerName**: the layer name of the net the model that you want to  extract feature of.

####**Output**
- The format of the feature data is float and binary.
- If feat_file not set, the deep learning feature of every image will be saved into a binary file with the same path as the image and named by  "the image name" + ".feat" .

####**Sample command**
    ExtractDeepFeat.exe E:\\myimages fc7 -model_file=bvlc_alexnet.caffemodel -net_file=image_val.prototxt
    ExtractDeepFeat.exe E:\\imageIndex.txt  prob -mode=GPU
    ExtractDeepFeat.exe E:\\test.jpg   pool5
