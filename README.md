# Face recognition models
## Step 1.	Pre-processing
안면 인식에 필요한 데이터 수집을 위해서, 먼저 얼굴 측면을 포함해 동영상을 촬영하고, 지정한 frame 구간마다 화면을 capture하여 별도로 저장.

## Step 2. Face detection 
Capture된 이미지 데이터에서, 사람의 얼굴영역만 추출하기 위해서 Faster-RCNN을 적용.
기존 영상처리만 적용한 모델에 대비해, 사전학습한 Faster-RCNN모델은 전면뿐만 아니라 측면, 작은 사람 얼굴까지 추출이 가능함.
Classification과 Object detection이 동시에 가능한 장점을 가진 모델이기 때문에 범용적으로 사용되는 모델.
기존 Fast RCNN 모델이 연산과정 중 Selective search를 수행하여 속도가 느리다. 그 이유는 해당 알고리즘은 GPU에 적합하지 않은 연산이기 때문.
이를 보안한 알고리즘이 Faster-RCNN이며, R-CNN모델 중 가장 최신 모델이며 속도, 성능 측면에서 우수함을 보여줌. 

## Step 3. Classification
MobileNet 모델은 모바일 기기 및 엣지 디바이스에 주로 사용되는 모델이다. 일반적으로 사용되는 EfficientNet, ResNet과 달리 연산량은 매우 적으며 성능은 그에 준하는 높은 성능을 보여줌.


## 참고
Training data의 화질이 너무 높은 경우, 실제 데이터와 화소가 차이나면서 안면인식 정확도가 떨어질 수 있음.
다시 말해, Training data의 화질과 모델의 정확도는 비례하지 않음.
따라서 실제 Image 데이터가 화소가 상대적으로 낮을 경우에, Training data의 화질을 의도적으로 Degradation 시켜야 할 것임.

## Augmentation
촬영 데이터의 조도, 명암, 촬영 거리가 제각각이기 때문에 이미지 정규화를 진행해야함
죽, 이미지 정규화는 학습 전 필수적으로 진행되어야 함: -> Normalize

Face-detection의 경우, 다음과 같은 augmentation을 사용하면 데이터 증강 뿐만 아니라 학습 데이터의 다양성을 줄 수 있음
1. Horizontal Flip 2. Random Rotation 3. Cental Cropping
참고 사이트 - https://pytorch.org/vision/0.9/transforms.html

https://github.com/alsgkals2/Preprocessing_Pytorch 에서 Image resize, translation type of file 등 코드정리해둔게 있어서 필요할 때 참고하시면 될 듯합니다.