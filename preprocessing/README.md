
## 코드 설명
    1. Receive the DICOM (.dcm) file and rescale the pixel value up to [-1000,3000] to [0,255]
    2. Receive DICOM (.dcm) file and pre-process brain, subdual, and soft window into 3-channel image
    3. Enter the pre-processed image and the scaled image into the model and Lime expander to return the predicted value and Lime image

## *```Raw Dataset```*
### ```Dicom file```

Dicom file is an image file type used in the medical community, and each pixel value follows the Hounsfield Unit (HU).

*[Hounsfield Unit]*(https://www.materialise.com/ko/faq/hounsfield-danwihulan):
```
The Hounsfield Unit (HU) constitutes the gray scale of the medical CT image. A scale ranging from black to white with 4096 values (12 bits), ranging from -1024HU to 3071HU (also included in the value). This is defined as follows:

-1024HU is black and indicates air (inside the lungs). 0HU represents water (the human body is mainly composed of water, so the peak is large here). The 3071HU is white and represents tooth enamel, the densest tissue in the human body. All other organizations are within this scale. Fat is about -100 HU, muscle is about 100 HU, and bone width is about 2000 HU (cortical bone) from 200 HU (soju bone / mandible).
```
![ct](https://user-images.githubusercontent.com/53938323/179692161-43f0c064-423b-4bc7-ae50-13530074d16a.gif)


## *```Data Preprocessing```*
### ```gray(1-channel) to color(3-channel)```


![image](https://user-images.githubusercontent.com/53938323/179885090-90a08fde-4674-47c3-9ad1-19ba859c06c9.png)

Using the gray scale image based on the HU, each tissue/organ (brain, soft tissue, bleeding area, etc.) has a certain range in the HU,
It was converted to a color image of a 3-channel. (Additionally, ResNET and InceptionNet receive the 3-channel image as input.)

