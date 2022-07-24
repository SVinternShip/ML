
## *ML 데이터셋*

#### 데이터 출처

    RSNA(북미영상의학회)
    https://www.kaggle.com/competitions/rsna-intracranial-hemorrhage-detection
    
    뇌 CT 촬영 DICOM 파일 : 약 450 GB
    
#### 데이터셋 설명

    DICOM FILE 의 픽셀값들은 하운스필드 유닛을 따름.(약 -1,000 ~ 약 3,000) <=> 일반 이미지 (0 ~ 255) : https://www.materialise.com/ko/faq/hounsfield-danwihulan
    각 조직별로 HU 범위가 어느정도 정해져있음.
    
![image](https://user-images.githubusercontent.com/53938323/180634801-c47fd1f4-6ebd-4474-8116-0972885394e8.png)
![image](https://user-images.githubusercontent.com/53938323/180634815-98d944f6-ae7c-406b-bc6f-3d47ca28b69b.png)

    
#### 데이터 시각화


## *데이터 전처리*

#### 데이터 균일화 : 언더샘플링(Under Sampling)
    정상데이터셋, 뇌출혈데이터셋 원래 비율 이미지
    정상데이터셋, 뇌출혈데이터셋 1 : 1 맞춘 이미지(갯수 표시)

#### Gray(1-channel) 2 Color(3-channels)
    회색 이미지 > 3 channel 이미지로 바뀌는거 보여주기
    
#### 데이터 정규화(Normalization)
    음... 0 , 255 , 127 이 있는 픽셀들이
    0,1,0.5 가 있는 픽셀들로 바뀌는 이미지 2개

## *모델 아키텍쳐*




## *W&B *
