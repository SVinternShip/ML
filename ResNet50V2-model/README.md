

## *```Code description``*

#### Remove Bad Image Dataset
    Images (blank image and terminal photographing image) that are not helpful for learning are excluded from learning.

#### Load Train Dataset
    Loads the dataset through the ImageDataGenerator. Set ratio "Train : validation = 4 : 1 "
    Rescale each image pixel value from 0 to 1.
    Resize the original image (512,512) to image size (224,224)
    Set class mode as binary.(Brain hemorrhage vs normal classification)

#### Model Architecture
    base model : ResNet50 V2
    + Global averaging pooling layer
    + Drop Out : 50%
    + Sigmoid layer [0,1]

#### Compile the model
    base learning rate : 0.0005
    optimizer : Adam
    loss : Binary Cross Entrophy
    initial_epochs : 10

#### Model Baseline
    initial loss: 0.69
    initial accuracy: 0.53

#### Training Model

##### ```Before Customizing```
    Epoch 1/10
    9514/9514 [==============================] - 616s 65ms/step - loss: 0.3468 - accuracy: 0.8492 - val_loss: 0.3483 - val_accuracy: 0.8457
    Epoch 2/10
    9514/9514 [==============================] - 649s 68ms/step - loss: 0.3250 - accuracy: 0.8606 - val_loss: 0.3407 - val_accuracy: 0.8518
    Epoch 3/10
    9514/9514 [==============================] - 681s 72ms/step - loss: 0.3118 - accuracy: 0.8669 - val_loss: 0.3242 - val_accuracy: 0.8633
    Epoch 4/10
    9514/9514 [==============================] - 671s 71ms/step - loss: 0.3004 - accuracy: 0.8730 - val_loss: 0.3258 - val_accuracy: 0.8647
    Epoch 5/10
    9514/9514 [==============================] - 663s 70ms/step - loss: 0.2900 - accuracy: 0.8785 - val_loss: 0.3169 - val_accuracy: 0.8663
    Epoch 6/10
    9514/9514 [==============================] - 630s 66ms/step - loss: 0.2811 - accuracy: 0.8827 - val_loss: 0.3146 - val_accuracy: 0.8701
    Epoch 7/10
    9514/9514 [==============================] - 658s 69ms/step - loss: 0.2721 - accuracy: 0.8867 - val_loss: 0.3183 - val_accuracy: 0.8715
    Epoch 8/10
    9514/9514 [==============================] - 673s 71ms/step - loss: 0.2658 - accuracy: 0.8895 - val_loss: 0.3243 - val_accuracy: 0.8707
    Epoch 9/10
    9514/9514 [==============================] - 672s 71ms/step - loss: 0.2559 - accuracy: 0.8942 - val_loss: 0.3125 - val_accuracy: 0.8722
    Epoch 10/10
    9514/9514 [==============================] - 658s 69ms/step - loss: 0.2505 - accuracy: 0.8962 - val_loss: 0.3453 - val_accuracy: 0.8643

<img src = "https://user-images.githubusercontent.com/53938323/179889644-049d8dcf-b5d4-4c44-9ad7-bf6ec2811db0.png" width="30%" height="30%">

##### Remove bad datasets (approximately 6,000 images removed)

    1. Remove datasets that interfere with learning

<img src = "https://user-images.githubusercontent.com/53938323/179888528-4a2555f9-2046-43f7-b0fa-c1a89c50429f.png" width="30%" height="30%">
<img src = "https://user-images.githubusercontent.com/53938323/179888566-0fc82b48-5d2b-411c-82b6-65055f72cfe7.png" width="30%" height="30%">

##### ```After Customizing```
    Epoch 1/10
    9212/9212 [==============================] - 921s 99ms/step - loss: 0.3595 - binary_accuracy: 0.8456 - val_loss: 0.3123 - val_binary_accuracy: 0.8700 - _timestamp: 1657823605.0000 - _runtime: 921.0000
    Epoch 2/10
    9212/9212 [==============================] - 915s 99ms/step - loss: 0.2924 - binary_accuracy: 0.8811 - val_loss: 0.2425 - val_binary_accuracy: 0.9070 - _timestamp: 1657824521.0000 - _runtime: 1837.0000
    Epoch 3/10
    9212/9212 [==============================] - 917s 100ms/step - loss: 0.2638 - binary_accuracy: 0.8958 - val_loss: 0.2364 - val_binary_accuracy: 0.9108 - _timestamp: 1657825438.0000 - _runtime: 2754.0000
    Epoch 4/10
    9212/9212 [==============================] - 869s 94ms/step - loss: 0.2430 - binary_accuracy: 0.9048 - val_loss: 0.2175 - val_binary_accuracy: 0.9239 - _timestamp: 1657826307.0000 - _runtime: 3623.0000
    Epoch 5/10
    9212/9212 [==============================] - 861s 93ms/step - loss: 0.2249 - binary_accuracy: 0.9131 - val_loss: 0.2136 - val_binary_accuracy: 0.9233 - _timestamp: 1657827168.0000 - _runtime: 4484.0000
    Epoch 6/10
    9212/9212 [==============================] - 890s 97ms/step - loss: 0.2058 - binary_accuracy: 0.9219 - val_loss: 0.2077 - val_binary_accuracy: 0.9261 - _timestamp: 1657828057.0000 - _runtime: 5373.0000
    Epoch 7/10
    9212/9212 [==============================] - 908s 99ms/step - loss: 0.1848 - binary_accuracy: 0.9308 - val_loss: 0.2147 - val_binary_accuracy: 0.9244 - _timestamp: 1657828966.0000 - _runtime: 6282.0000
    Epoch 8/10
    9212/9212 [==============================] - 903s 98ms/step - loss: 0.1630 - binary_accuracy: 0.9399 - val_loss: 0.2222 - val_binary_accuracy: 0.9241 - _timestamp: 1657829869.0000 - _runtime: 7185.0000
    Epoch 9/10
    9212/9212 [==============================] - 908s 99ms/step - loss: 0.1403 - binary_accuracy: 0.9488 - val_loss: 0.2240 - val_binary_accuracy: 0.9214 - _timestamp: 1657830778.0000 - _runtime: 8094.0000

<img src = "https://user-images.githubusercontent.com/53938323/179889919-e9f8efd1-4810-4ef9-9b33-e6c8dd6679d3.png" width="30%" height="30%">




#### Model Conditions

    1. There are plenty of datasets, but transition learning is needed to reduce learning time
    2. Is fast inference possible and light enough for the environment you have (server and learning environment)? - XAI can only be introduced if the model structure is simple

![image](https://user-images.githubusercontent.com/53938323/179887853-83a2478f-c7e1-43cb-94e9-9708f0dddd53.png)



*[InceptionNet V3]*(https://cloud.google.com/tpu/docs/inception-v3-advanced?hl=ko):
```
Inception v3 is an image recognition model that has proven to be more than 78.1% accurate on ImageNet datasets.
```

<img src = "https://user-images.githubusercontent.com/53938323/179886770-bd1be44e-f349-4df7-9611-5063b669a292.png" width="30%" height="30%">
