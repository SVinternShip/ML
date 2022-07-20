## *```Model description``*
### ```InceptionNet V3```

#### 모델 조건

    1. 충분히 많은 데이터셋이 있지만 학습 시간을 줄이기 위해 전이학습이 필요
    2. 가진 환경(서버 및 학습 환경)에 맞게 빠른 추론이 가능하고 충분히 가벼운가? - 모델 구조가 간단해야 XAI의 도입이 가능함

![image](https://user-images.githubusercontent.com/53938323/179887853-83a2478f-c7e1-43cb-94e9-9708f0dddd53.png)



*[InceptionNet V3]*(https://cloud.google.com/tpu/docs/inception-v3-advanced?hl=ko):
```
Inception v3은 ImageNet 데이터 세트에서 정확도가 78.1% 이상인 것으로 입증된 영상 인식 모델입니다. 
이 모델은 장기간 수많은 연구에서 나온 다양한 아이디어가 축적된 결과입니다. 
이 내용은 세게디 외 여러 저자가 저술한 'Rethinking the Inception Architecture for Computer Vision'이라는 원본 논문을 토대로 작성되었습니다.

모델 자체는 컨볼루션, 평균 풀링, 최대 풀링, 연결, 드롭아웃, 완전 연결형 레이어를 포함한 대칭 및 비대칭 구성요소로 구성되어 있습니다. 
배치 정규화는 모델 전반에 광범위하게 사용되며 활성화 입력에 적용됩니다. 손실은 소프트맥스를 통해 계산됩니다.
```

![image](https://user-images.githubusercontent.com/53938323/179886770-bd1be44e-f349-4df7-9611-5063b669a292.png)

### ```Model Customizing```

#### 출력층 layer 추가
    
    1. Global average pooling layer 추가
    2. Drop out 50% 적용
    3. 일반 0,1 분류대신에 sigmoid 사용(추후 threshold 추가 예정)
    

#### 불량 데이터셋 제거(약 6,000장 제거)

    1. 학습에 방해가 되는 데이터셋들을 제거하였다. 
 
<img src = "https://user-images.githubusercontent.com/53938323/179888528-4a2555f9-2046-43f7-b0fa-c1a89c50429f.png" width="30%" height="30%">
<img src = "https://user-images.githubusercontent.com/53938323/179888566-0fc82b48-5d2b-411c-82b6-65055f72cfe7.png" width="30%" height="30%">

#### 학습 결과


    
