# ML
ML 모델, 전처리 코드

## 코드 설명
    1. DICOM(.dcm)파일을 받아서 [-1000,3000] 까지의 픽셀값을 [0,255] 로 rescale
    2. DICOM(.dcm)파일을 받아서 brain, subdural, soft window 를 각각 뽑아 3-channel 이미지로 전처리
    3. 전처리된 이미지와 rescale 된 이미지를 모델과 Lime explainer 에 입력하여 예측값과 Lime 이미지를 반환

## ```Raw Dataset```
### ```1. Dicom file```

Dicom file 은 의학계에서 사용하는 이미지 파일 형태로서, 각 픽셀값들은 Hounsfield Unit(일명 HU)을 따른다.

*[Hounsfield Unit]*(https://www.materialise.com/ko/faq/hounsfield-danwihulan):

```
$ pip install tensorflow
```
