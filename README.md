## *```Model description``*
### ```InceptionNet V3```

Dicom file 은 의학계에서 사용하는 이미지 파일 형태로서, 각 픽셀값들은 Hounsfield Unit(일명 HU)을 따른다.

*[InceptionNet V3]*(https://cloud.google.com/tpu/docs/inception-v3-advanced?hl=ko):
```
Inception v3은 ImageNet 데이터 세트에서 정확도가 78.1% 이상인 것으로 입증된 영상 인식 모델입니다. 이 모델은 장기간 수많은 연구에서 나온 다양한 아이디어가 축적된 결과입니다. 이 내용은 세게디 외 여러 저자가 저술한 'Rethinking the Inception Architecture for Computer Vision'이라는 원본 논문을 토대로 작성되었습니다.

모델 자체는 컨볼루션, 평균 풀링, 최대 풀링, 연결, 드롭아웃, 완전 연결형 레이어를 포함한 대칭 및 비대칭 구성요소로 구성되어 있습니다. 배치 정규화는 모델 전반에 광범위하게 사용되며 활성화 입력에 적용됩니다. 손실은 소프트맥스를 통해 계산됩니다.
```

![image](https://user-images.githubusercontent.com/53938323/179886770-bd1be44e-f349-4df7-9611-5063b669a292.png)
