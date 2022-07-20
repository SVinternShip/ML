

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
    10364/10364 [==============================] - 1015s 97ms/step - loss: 0.4067 - binary_accuracy: 0.8149 - val_loss: 0.3050 - val_binary_accuracy: 0.8757 - _timestamp: 1658302150.0000 - _runtime: 1018.0000
    Epoch 2/10
    10364/10364 [==============================] - 974s 94ms/step - loss: 0.3309 - binary_accuracy: 0.8595 - val_loss: 0.2593 - val_binary_accuracy: 0.8996 - _timestamp: 1658303125.0000 - _runtime: 1993.0000
    Epoch 3/10
    10364/10364 [==============================] - 964s 93ms/step - loss: 0.2991 - binary_accuracy: 0.8762 - val_loss: 0.2599 - val_binary_accuracy: 0.9001 - _timestamp: 1658304089.0000 - _runtime: 2957.0000
    Epoch 4/10
    10364/10364 [==============================] - 968s 93ms/step - loss: 0.2775 - binary_accuracy: 0.8869 - val_loss: 0.2672 - val_binary_accuracy: 0.8901 - _timestamp: 1658305057.0000 - _runtime: 3925.0000
    Epoch 5/10
    10364/10364 [==============================] - 1006s 97ms/step - loss: 0.2591 - binary_accuracy: 0.8965 - val_loss: 0.2415 - val_binary_accuracy: 0.9103 - _timestamp: 1658306063.0000 - _runtime: 4931.0000
    Epoch 6/10
    10364/10364 [==============================] - 984s 95ms/step - loss: 0.2394 - binary_accuracy: 0.9043 - val_loss: 0.2347 - val_binary_accuracy: 0.9155 - _timestamp: 1658307047.0000 - _runtime: 5915.0000
    Epoch 7/10
    10364/10364 [==============================] - 990s 96ms/step - loss: 0.2168 - binary_accuracy: 0.9140 - val_loss: 0.2345 - val_binary_accuracy: 0.9165 - _timestamp: 1658308037.0000 - _runtime: 6905.0000
    Epoch 8/10
    10364/10364 [==============================] - 963s 93ms/step - loss: 0.1915 - binary_accuracy: 0.9249 - val_loss: 0.2473 - val_binary_accuracy: 0.9140 - _timestamp: 1658309001.0000 - _runtime: 7869.0000
    Epoch 9/10
    10364/10364 [==============================] - 944s 91ms/step - loss: 0.1635 - binary_accuracy: 0.9367 - val_loss: 0.2619 - val_binary_accuracy: 0.9135 - _timestamp: 1658309945.0000 - _runtime: 8813.0000
    Epoch 10/10
    10364/10364 [==============================] - 946s 91ms/step - loss: 0.1357 - binary_accuracy: 0.9473 - val_loss: 0.3062 - val_binary_accuracy: 0.9118 - _timestamp: 1658310891.0000 - _runtime: 9759.0000
    
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
