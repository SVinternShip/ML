

## *```Code description``*

#### 불량한 이미지 데이터셋 제거
    학습에 도움이 되지 않는 이미지들(공백 이미지, 말단 촬영 이미지)은 학습에서 제외한다.

#### 학습 데이터셋 로드
    ImageDataGenerator 를 통해 데이터셋을 불러온다. train : validation = 4 : 1 비로 설정했다.
    각 이미지 픽셀값은 0 ~ 1 로 rescale.
    원본 이미지는 (512,512), 불러올때는 이미지 사이즈 (224,224)로 resize.
    뇌출혈 vs 정상 분류이므로 binary 로 class mode 를 설정.

#### 모델 설계
    base model : InceptionNet V3
    + Global averaging pooling layer
    + Drop Out : 50%
    + Sigmoid layer [0,1]

#### 모델 컴파일
    base learning rate : 0.0005
    optimizer : Adam
    loss : Binary Cross Entrophy
    initial_epochs : 10

#### 모델 baseline
    initial loss: 0.69
    initial accuracy: 0.53

#### 모델 train
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

## *```Model description``*

### ```InceptionNet V3```

#### 모델 조건

    1. 충분히 많은 데이터셋이 있지만 학습 시간을 줄이기 위해 전이학습이 필요
    2. 가진 환경(서버 및 학습 환경)에 맞게 빠른 추론이 가능하고 충분히 가벼운가? - 모델 구조가 간단해야 XAI의 도입이 가능함

![image](https://user-images.githubusercontent.com/53938323/179887853-83a2478f-c7e1-43cb-94e9-9708f0dddd53.png)



*[InceptionNet V3]*(https://cloud.google.com/tpu/docs/inception-v3-advanced?hl=ko):
```
Inception v3은 ImageNet 데이터 세트에서 정확도가 78.1% 이상인 것으로 입증된 영상 인식 모델입니다. 
```

<img src = "https://user-images.githubusercontent.com/53938323/179886770-bd1be44e-f349-4df7-9611-5063b669a292.png" width="30%" height="30%">

### ```Model Customizing```

#### 출력층 layer 추가
    
    1. Global average pooling layer 추가
    2. Drop out 50% 적용
    3. 일반 0,1 분류대신에 sigmoid 사용(추후 threshold 추가 예정)

<img src = "https://user-images.githubusercontent.com/53938323/179889568-2afd363b-741d-4a73-a877-a17ddfcbde40.png" width="30%" height="30%">

#### 불량 데이터셋 제거(약 6,000장 제거)

    1. 학습에 방해가 되는 데이터셋들을 제거하였다. 
 
<img src = "https://user-images.githubusercontent.com/53938323/179888528-4a2555f9-2046-43f7-b0fa-c1a89c50429f.png" width="30%" height="30%">
<img src = "https://user-images.githubusercontent.com/53938323/179888566-0fc82b48-5d2b-411c-82b6-65055f72cfe7.png" width="30%" height="30%">

#### 학습 결과

##### ```Before Customizing```

<img src = "https://user-images.githubusercontent.com/53938323/179889644-049d8dcf-b5d4-4c44-9ad7-bf6ec2811db0.png" width="30%" height="30%">

##### ```After Customizing```

<img src = "https://user-images.githubusercontent.com/53938323/179889919-e9f8efd1-4810-4ef9-9b33-e6c8dd6679d3.png" width="30%" height="30%">
    
