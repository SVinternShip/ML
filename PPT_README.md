
## *ML 데이터셋*

#### 데이터 출처

    RSNA(북미영상의학회)
    https://www.kaggle.com/competitions/rsna-intracranial-hemorrhage-detection
    
    뇌 CT 촬영 DICOM 파일 : 약 450 GB
    
#### 데이터셋 설명

    DICOM FILE 의 픽셀값들은 하운스필드 유닛을 따름.(약 -1,000 ~ 약 3,000) <=> 일반 이미지 (0 ~ 255) : https://www.materialise.com/ko/faq/hounsfield-danwihulan
    각 조직별로 HU 범위가 어느정도 정해져있음.
![image](https://user-images.githubusercontent.com/53938323/180634915-18084174-0ae6-4424-8fbd-12559a013bf8.png)   
![image](https://user-images.githubusercontent.com/53938323/180634801-c47fd1f4-6ebd-4474-8116-0972885394e8.png)
![image](https://user-images.githubusercontent.com/53938323/180634815-98d944f6-ae7c-406b-bc6f-3d47ca28b69b.png)

    
#### 데이터 시각화

    일반적인 이미지로 시각화를 하기 위해서 (약 -1,000 ~ 약 3,000) 의 범위에 있는 픽셀값들을 0 ~ 255 로 정규화

![image](https://user-images.githubusercontent.com/53938323/180634936-0c89ebb9-d4ff-4bb0-bf16-c0cf61994c25.png)

## *데이터 전처리*

#### 데이터 균일화 : 언더샘플링(Under Sampling)
    정상데이터셋, 뇌출혈데이터셋 원래 비율 이미지
    정상 데이터셋   : 3814760장
    뇌출혈 데이터셋 : 230812장
    정상 : 이상 = 16 : 1     => 매우 심하게 불균일한 데이터셋
    이대로 학습할 경우, 모델은 정상 데이터셋을 맞추는것에 '편향'되어 학습한다.(전부 정상이라 예측해도 정확도는 16/17*100 = 94%)
    이럴때에는 loss 함수를 dice loss 로 바꾸어도 되지만,
    뇌 CT 이미지는 각도나 넓이 등을 고려하더라도 거의 유사하다는 성질을 고려하여, Undersampling 을 진행하였다. 
    
    왜 Under Sampling 을 하였는가?
    K Fold , OverSampling 등 다양한 선택지가 있지만, 한정된 GPU 환경에서 10만장으로도 몇 시간 소요되므로 데이터셋을 줄이는것이 효울적임.
    그리고 실제로 UnderSampling 한 결과, 정확도는 92.8% 나오므로 문제는 없다.
    
![image](https://user-images.githubusercontent.com/53938323/180634984-e683baa9-7627-4e29-b714-7bd6dbef98dd.png)

    정상데이터셋, 뇌출혈데이터셋 1 : 1 맞춘 이미지(갯수 표시)
    

#### Gray(1-channel) 2 Color(3-channels)
    Brain , Subdural, Soft 의 HU 범위에 있는 픽셀값들만 추출해서 R G B 채널로 만들고 하나의 컬러 이미지로 전처리.
![image](https://user-images.githubusercontent.com/53938323/180635631-bb138810-5eda-4386-9730-c82d2e4de0b3.png)

  
#### 데이터 정규화(Normalization)

![image](https://user-images.githubusercontent.com/53938323/180635738-3c25d57e-c297-4a44-8fa0-93639475b052.png)


## *모델 아키텍쳐*

    Inception V3 모델
    출력층에 Global Averge Pooling Layer 추가 + Drop out 50% 반영
    
    1. GAP 추가 이유
    합성곱 신경망의 특성상, 필터에 의해 feature map 이 매우 커짐 => over fitting 발생.
    극단적으로 1차원 벡터로 줄여주는 GAP를 통해 해결.
    
    2. Drop Out 50% 반영 이유
    똑같이 over fitting 문제 해결(일반적으로 50% 에서 효과가 좋음)
    
GAP
![image](https://user-images.githubusercontent.com/53938323/180635855-c2b9c97f-a9ed-48d0-976f-883e44fec892.png)

모델 구조
![image](https://user-images.githubusercontent.com/53938323/180635777-3664bf8f-3815-47bf-ab2e-da97d470715b.png)
![image](https://user-images.githubusercontent.com/53938323/180636147-eac35643-9505-4935-a23c-72548b52da79.png)

Accuracy & Loss
![image](https://user-images.githubusercontent.com/53938323/180636180-1ac2dcab-964c-450b-9cd0-703060828d67.png)

그외 지표들
(Precision, Recall, f1 - score ...)
Precision : 모델이 예측한 것이 실제로 맞는가
Recall : 실제로 모델이 예측한 것이 맞는 정도
F1-Score : Precision 과 Recall 짬뽕한 지표 

실제로는 뇌출혈(양성,Positive)인데, 정상(음성,Negative)이라 예측하는 위음성(False Negative) Precentage 가 낮음 : 4.76% 
Confusion Matrix 값이 바뀌었기 때문에 곧 수정 예정.
![image](https://user-images.githubusercontent.com/53938323/180636239-ffc1fdff-941f-4b93-9742-cdcdd7b5714e.png)



## *W&B 를 통한 버전 및 학습환경관리 및 모델 공유 *

모델의 버전 관리 가능
![image](https://user-images.githubusercontent.com/53938323/180636544-0de23e52-225c-4f18-bab9-7c472df2d58c.png)

모델 학습 환경 모니터링
![image](https://user-images.githubusercontent.com/53938323/180636555-0d2d43c3-5e5e-4f5e-8268-1aff61e8c202.png)
![image](https://user-images.githubusercontent.com/53938323/180636566-6c5f676e-bf1c-4276-938c-f8e5cd42aa3f.png)

모델 저장 및 NETRON 기반 구조 확인 가능
![image](https://user-images.githubusercontent.com/53938323/180636590-85da953f-eff4-4ebd-a573-bcb49bf897b2.png)

![image](https://user-images.githubusercontent.com/53938323/180636604-da1dbf22-8cc2-4f72-b93f-1a710dedde73.png)


