# ML
ML 모델, 전처리 코드

## 코드 설명
    1. DICOM(.dcm)파일을 받아서 [-1000,3000] 까지의 픽셀값을 [0,255] 로 rescale
    2. DICOM(.dcm)파일을 받아서 brain, subdural, soft window 를 각각 뽑아 3-channel 이미지로 전처리
    3. 전처리된 이미지와 rescale 된 이미지를 모델과 Lime explainer 에 입력하여 예측값과 Lime 이미지를 반환

## *```Raw Dataset```*
### ```Dicom file```

Dicom file 은 의학계에서 사용하는 이미지 파일 형태로서, 각 픽셀값들은 Hounsfield Unit(일명 HU)을 따른다.

*[Hounsfield Unit]*(https://www.materialise.com/ko/faq/hounsfield-danwihulan):
```
Hounsfield 단위(HU)는 의료 CT 이미지의 그레이 스케일을 구성합니다. 4096개 값(12비트)의 검은색에서 흰색에 이르는 스케일로 그 범위는 -1024HU ~ 3071HU(0 또한 값에 포함됨)입니다. 이는 다음과 같이 정의됩니다.

-1024HU는 검은색이며 공기(폐 내부)를 나타냅니다. 0HU는 물(인체는 주로 물로 구성되어 있으므로 여기에서 피크가 큼)을 나타냅니다. 3071HU는 흰색이며 인체에서 가장 밀도가 높은 조직인 치아 에나멜을 나타냅니다. 다른 모든 조직은 이 스케일 내에 있습니다. 지방은 약 -100HU, 근육은 약 100HU이며 뼈 폭은 200HU(소주골/하악골)에서 약 2000HU(피질골)입니다.

일반적으로 금속 임플란트의 Hounsfield 단위는 매우 높습니다. 따라서 일반적인 12비트 CT 스캔(3071)의 최대 값에 기인합니다.
```
![ct](https://user-images.githubusercontent.com/53938323/179692161-43f0c064-423b-4bc7-ae50-13530074d16a.gif)

```
$ pip install tensorflow
```
