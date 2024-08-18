# 저해상도 이미지의 복구 모델 개발
이 프로젝트는 SRCNN (Super-Resolution Convolutional Neural Network) 모델을 사용하여 저해상도 이미지를 고해상도로 변환하는 작업을 수행합니다. 모델은 Python 기반의 딥러닝 프레임워크인 PyTorch를 사용하여 학습 및 테스트됩니다. 이 프로젝트는 Google Colab에서 실행되며, 필요한 모든 스크립트와 데이터셋은 이 저장소에 통합되어 있습니다.

## 프로젝트의 배경 및 목표

- **배경**: 이미지의 해상도를 향상시키는 것은 다양한 분야에서 중요한 기술입니다. 특히 저해상도 이미지를 고해상도로 변환하는 Super-Resolution 기술은 의료 영상, 위성 이미지 분석, 사진 복원 등 여러 응용 분야에서 큰 잠재력을 가지고 있습니다.
- **목표**: CNN 기반의 Super-Resolution 모델인 SRCNN을 구축하여 저해상도 이미지를 고해상도로 변환하는 성능을 극대화하고, 이 과정에서 모델의 구조와 학습 방법을 이해하고 개선하는 것이 목표입니다.

## 활용한 데이터셋

- **데이터셋**: 다양한 해상도의 이미지로 구성된 데이터셋을 사용, 저해상도 이미지 (sub-image)와 고해상도 이미지 (label) 쌍을 생성하여 모델 학습에 활용.
- **데이터 전처리**: 이미지를 float32로 변환하고, 학습용과 검증용으로 데이터셋을 분리.

## 프로젝트 진행 과정

- **데이터 준비**:
    - 입력 및 레이블 데이터를 75:25 비율로 Train/Validation 셋으로 분리.
    - 커스텀 데이터셋 `SRCNNDataset`을 생성하여 DataLoader로 배치 단위 데이터 로딩.
- **모델 구조**:
    - 3개의 Convolutional Layer로 구성된 CNN 기반 Super-Resolution 모델을 설계.
    - 첫 번째 레이어에서 특징 추출, 두 번째 레이어에서 비선형 매핑, 세 번째 레이어에서 이미지 재구성.
- **훈련 과정**:
    - **손실 함수**: MSELoss를 사용하여 모델이 출력한 이미지와 레이블 이미지 간의 차이를 최소화.
    - **Optimizer**: Adam Optimizer를 사용해 가중치 업데이트.
    - **평가 지표**: PSNR(Peak Signal-to-Noise Ratio)을 통해 이미지의 유사도를 측정. PSNR 값이 클수록 고해상도 이미지와의 유사도가 높음을 의미.
- **검증 과정**:
    - 각 에포크마다 모델 성능을 검증 데이터셋을 통해 평가.
    - 검증 과정에서의 손실(Loss) 및 PSNR 변화를 시각화하여 모델 성능을 모니터링.
    - 최종 이미지를 시각화하여 고해상도 복원 성능 확인.

## 분석 결과
![image](https://github.com/user-attachments/assets/efeaa7ec-05e9-4056-8388-c436f8854cde)
- **성능**: 손실 함수는 학습 초기에 급격히 감소한 후 수렴하였고, PSNR은 빠르게 상승 후 안정적으로 유지되었습니다. 이는 모델이 안정적으로 학습되었으며, 고해상도 이미지와의 유사도가 높음을 시사합니다.
- **검증**: 검증 데이터셋에서도 학습 데이터셋과 유사한 성능을 보여, 모델이 과적합 없이 일반화된 성능을 보임을 확인했습니다.

## 프로젝트를 통해 얻은 인사이트

- **모델의 안정성**: 손실과 PSNR 그래프를 통해 모델이 안정적으로 학습되었음을 확인했습니다. 특히 PSNR이 검증 데이터셋에서도 높은 값을 기록해 모델의 일반화 성능이 우수함을 알 수 있었습니다.
- **추가 실험의 필요성**: 더 높은 PSNR을 달성하기 위해 다양한 네트워크 구조나 데이터 증강 기법을 적용할 수 있는 가능성을 발견했습니다.
