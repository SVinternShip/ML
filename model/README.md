

## *```Code description``*

#### *```불량한 이미지 데이터셋 제거```*
    학습에 도움이 되지 않는 이미지들(공백 이미지, 말단 촬영 이미지)은 학습에서 제외한다.

#### *```학습 데이터셋 로드```*
    ImageDataGenerator 를 통해 데이터셋을 불러온다. train : validation = 4 : 1 비로 설정했다.
    각 이미지 픽셀값은 0 ~ 1 로 rescale.
    원본 이미지는 (512,512), 불러올때는 이미지 사이즈 (224,224)로 resize.
    뇌출혈 vs 정상 분류이므로 binary 로 class mode 를 설정.

#### *```모델 설계```*
    base model : InceptionNet V3
    + Global averaging pooling layer
    + Drop Out : 50%
    + Sigmoid layer [0,1]

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
    
