# Facial-emotion-Recognition(얼굴 감정 인식)

## 프로젝트 개요
**얼굴 감정 인식(Facial Emotion Recognition, FER)** 프로젝트는 컴퓨터 비전과 인공지능 기술을 활용하여 사람의 얼굴 표정을 분석하고 그로부터 감정을 추정하는 기술 및 시스템을 개발하는 것을 말합니다.
이런 기술을 통해 보안 및 감시, 의료 및 심리치료, 마케팅 및 소비자 분석, 고객 서비스 및 자동차 산업 등 다양한 산업에서 여러 문제를 해결할 수 있는 강력한 도구입니다. 이를 통해 보다 안전하고, 효과적이며, 개인화된 서비스를 제공할 수 있으며, 인간-기계 상호작용의 질을 크게 향상시킬 수 있습니다.

## **필요 라이브러리 및 프로그램**

1.Python: 코드를 실행하는 기본 환경.

2.TensorFlow/Keras: 딥러닝 모델을 구축하고 학습하는 데 사용됩니다.

* TensorFlow는 버전 2.x 이상을 권장합니다.

* Keras는 TensorFlow에 포함되어 있으므로 별도로 설치할 필요는 없습니다.

3.OpenCV: 컴퓨터 비전 작업을 수행하는 라이브러리.

4.DeepFace: 얼굴 감정 인식을 수행하는 라이브러리.

5.Matplotlib: 학습 결과를 시각화하는 데 사용됩니다.

6.Numpy: 수치 계산 및 배열 조작을 위한 라이브러리.

7.Google Colab: 코드를 실행할 수 있는 클라우드 기반 환경 (또는 로컬 환경).


## 추후 개선 사항
얼굴 감정 인식에 있어서 응용 분야에 따라 실시간으로 감정을 인식하면서 성능이 높게 나와야 하지만 60%의 정확도에 그쳐 나의 프로젝트 같은 경우 지속적으로 성능 부분을 개선해야 한다고 생각한다.

또한 우리나라 사람의 얼굴 뿐만 아니라 다양한 인종, 성별, 나이를 포함한 데이터를 확보해야 모델의 일반화 성능이 향상된다는 점과 개인의 프라이버시와 데이터 사용에 관한 윤리적 문제를 고려해야 한다는 점에서 얼굴 감정 인식의 한계점을 확인할 수 있.


-----
## 데이터 세트
**Kaggle - FER2013**

이미지에서 표정 학습
데이터세트 정보
데이터는 48x48픽셀의 회색조 얼굴 이미지로 구성됩니다. 얼굴은 자동으로 등록되어 얼굴이 어느 정도 중앙에 위치하고 각 이미지에서 거의 동일한 공간을 차지합니다.

FER2013의 과제 얼굴 표정에 나타난 감정을 기반으로 각 얼굴을 7가지 범주(0=화남, 1=혐오, 2=두려움, 3=행복, 4=슬픔, 5=놀람, 6=보통) 중 하나로 분류하는 것입니다. 훈련 세트는 28,709개의 예시로 구성되어 있으며, 공개 테스트 세트는 3,589개의 예시로 구성되어 있습니다.

## 모델 설명
![스크린샷 2024-06-11 230752](https://github.com/hyeoni0525/Facial-emotion-Recognition/assets/170999814/d279a0af-0346-4f2b-92ce-824985c78e10)

기본적으로 다양한 모델을 사용했으나 결과가 가장 높게 나왔던 2D CNN 모델을 선택했습니다. 기존의 DNN은 고해상도의 이미지를 처리할 때 입력 뉴런의 수가 급격하게 증가하게 되고 파라미터의 수도 급격하게 늘어나기 때문에 이미지나 영상과 같은 데이터를 처리할 때 생기는 문제점이 발생합니다. 이를 보완하기 위해 뉴런이 특정 범위에 있는 이미지만 학습하기 때문에 훨씬 적은 양의 파라미터가 필요로 하는 CNN 모델이 적합하다고 생각했습니다.

이 모델은 입력 이미지에서 특징을 추출하고, 이를 기반으로 감정 클래스를 예측하는 CNN 모델입니다. 여러 Conv2D와 MaxPooling2D 레이어를 통해 특징을 추출하고, Fully Connected 레이어를 통해 감정을 분류합니다. Dropout 레이어를 추가하여 과적합을 방지하고 모델의 일반화 성능을 높였습니다.

## 실험 결과
모델 평가에 사용된 지표는 accuracy가 있습니다.
Accuracy (정확도)란, 전체 문제중에서 정답을 맞춘 비율입니다.
Accuracy = TP+TN / TP+TN+FP+FN 으로

TP : 모델이 정답을 맞췄을 때,

TN : 모델이 오답을 맞췄을 때,

FP : 모델이 오답을 정답으로 잘못 예측했을 때,

FN : 모델이 정답을 오답으로 잘못 예측했을 때,

**맞춘 예측의 수 / 전체 문제의 수**

이렇게 볼 수 있기 때문에 감정을 인식하는데 있어서 얼마나 정확하게 맞출 수 있는지 정확도가 가장 중요하다고 생각해서 accuracy를 평가 지표로 사용했습니다.

그래프는 각각 순서대로 (epochs10 batch16), (epochs10 batch32), (epochs50 batch16), (epochs50 batch32), (epochs50 batch32 + 데이터 증강), (resnet50+reduceLR), (MobileNetV2) 순서 입니다.
이와 같이 다양한 ablation study를 통해 가장 최적의 값이 (epochs50 batch32)일 때 가장 높은 값이 나타나는 것을 확인 할 수 있었습니다.
![epochs10batch16](https://github.com/hyeoni0525/Facial-emotion-Recognition/assets/170999814/dae8787a-dd19-43c3-a01f-726f01dc6626)
![epochs10batch32](https://github.com/hyeoni0525/Facial-emotion-Recognition/assets/170999814/0c15e09e-a24e-4e02-8d7d-699e281df0de)
![epochs50batch16](https://github.com/hyeoni0525/Facial-emotion-Recognition/assets/170999814/0c18864a-ac64-41f2-aa5c-e364b5564281)
![epochs50batch32](https://github.com/hyeoni0525/Facial-emotion-Recognition/assets/170999814/5fbc9f51-5131-4670-b1e1-e82149277ada)
![epochs50batch32 증강변화rotation_range=30에서40 width_shift_range=0 2,          height_shift_range=0 2](https://github.com/hyeoni0525/Facial-emotion-Recognition/assets/170999814/edd450bd-710f-416a-a664-a48a3fedb698)
![resnet50+reduceLR](https://github.com/hyeoni0525/Facial-emotion-Recognition/assets/170999814/a0d4fd97-9b50-47fe-8f3d-8cf26c3bcf74)
![MobileNetV2](https://github.com/hyeoni0525/Facial-emotion-Recognition/assets/170999814/7137f830-4c8a-489a-a4cc-5683d1a13dfb)


-----
## 프로젝트 결과
![Emotions (3)](https://github.com/hyeoni0525/Facial-emotion-Recognition/assets/170999814/6d1b5278-522c-46ee-9056-c419bf498989)


이를 토대로 영상의 각 프레임마다 테스트를 하고 dominant_emotion을 나타내도록 설정했습니다.

단, 정확도가 낮을수록 감정이 잘못 나타나는 빈도가 많고 제 프로젝트의 경우 정확도가 60%이므로 정확도를 더 올려 오탐지 비율을 줄여야 할 것 입니다.




