

## *```Code description``*

#### predict and lime explainer module
    window_image(dcm_file,center,width) : In the corresponding dichom file, a pixel value (HU-based) within a range of half the width is extracted based on the center.
    convert_dcm2img_3ch(dcm_file) : Extract brain, subdual, and soft window from the corresponding dicom file and convert them into 3 channel images.
    dicom2nparray(dcm_file_path) : Returns the dicom file in dicom_file_path to a numpy array.
    preprocess(dcm_file_path) : Extract the properties of the dichom file in the dichom_file_path, preprocess it into the 3 channel image, and return them all.
    predict_and_lime(img_preprocessed, img_original, loaded) : After loading the model and lime expander, return the predicted value and the image masked by lime by entering the preprocessed image and the original file returned by the numpy array. (Run lime only when predicting cerebral hemorrhage.)


#### Lime Explainer Architecture
    classifier : loaded model(InceptionNet V3 or ResNet50 V2, but commonly InceptionNet V3)
    number of samples : 50 (It takes about a second)
    top labels : 5 (but we use the best one label)


##### ```Lime Masking```
    
<img src = "https://github.com/SVinternShip/ML/blob/5fb98449d53f29e5911c823a9d19f2cea7d9f5df/predict_and_lime/lime_original.png" width="30%" height="30%">
<img src = "https://github.com/SVinternShip/ML/blob/5fb98449d53f29e5911c823a9d19f2cea7d9f5df/predict_and_lime/lime_red_masking.png" width="30%" height="30%">
<img src = "https://github.com/SVinternShip/ML/blob/5fb98449d53f29e5911c823a9d19f2cea7d9f5df/predict_and_lime/lime_skelton.png" width="30%" height="30%">
<img src = "https://github.com/SVinternShip/ML/blob/5fb98449d53f29e5911c823a9d19f2cea7d9f5df/predict_and_lime/original_image.png" width="30%" height="30%">

