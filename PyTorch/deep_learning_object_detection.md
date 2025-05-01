# Deep Neural Network란?

- **인간의 신경망을 모사**해서 원하는 결과를 내도록 만든 알고리즘
- **Perceptron**: 여러 개의 입력 신호에 가중치를 곱해 최종 output을 내는 구조
- **Multi-Layer Perceptron (MLP)**: 퍼셉트론을 여러 층으로 쌓아 복잡한 패턴도 학습 가능
- **딥러닝에서의 학습**: 원하는 y값을 얻기 위해 **가중치(w)**를 조정하는 과정
- **Loss 함수**: 예측값 y와 실제값 y의 차이를 **수치로 표현한 값**
  - PyTorch에서는 `loss.backward()` 등을 통해 이 값을 기준으로 **weight를 자동으로 업데이트**함

---

# 객체 검출 알고리즘의 평가 지표

##  IoU (Intersection over Union)

- **Bounding box**가 ground truth와 얼마나 겹치는지 나타내는 지표
- **0 ~ 1** 사이 값 (1에 가까울수록 정확)
- **학습 시 loss 함수로도 사용됨**

>  **Bounding Box**: 객체가 이미지 내에서 **존재하는 영역**을 감싸는 직사각형

---

## Precision & Recall

- **Precision**: 예측을 positive로 한 것 중 실제로 정답인 비율  
  > → "검출한 것들 중 진짜 정답만 얼마나 잘 맞췄냐"  
- **Recall**: 실제 정답 중에서 예측이 얼마나 잘 맞았는지 비율  
  > → "실제 있는 것들 중에서 얼마나 안 놓쳤냐"

### 기준 (IoU):
- **True Positive (TP)**: 객체가 box 안에 있음  
- **False Positive (FP)**: 객체 없음 (오탐)  
- **False Negative (FN)**: 객체 있는데 못 찾음 (누락)

### Precision vs Recall (Threshold 영향)
- **Confidence Threshold ↑** → **Precision ↑**, **Recall ↓**  
- **Confidence Threshold ↓** → **Precision ↓**, **Recall ↑**

---

## Confidence

- 모델이 예측한 bounding box가 **얼마나 신뢰할 만한지** 나타내는 값
- 보통 **Objectness Score**와 **Class Probability**를 곱해서 계산

---

# YOLO (You Only Look Once)

- **분류(Classification)**와 **위치 추정(Localization)**을 동시에 처리하는 객체 검출 알고리즘
- **실시간(Real-Time)** 탐지가 가능하며, 빠르면서도 정확함

## YOLO 동작 방식

1. 입력 이미지 Resize
2. CNN으로 Feature 추출
3. **Bounding box + Class + Confidence 예측**
4. **NMS (Non-Max Suppression)** 적용하여 중복 제거

## YOLO 학습 Loss 구성

- Bounding box 위치 정확도 (좌표 예측 오차)
- Confidence score 예측 오차
- Class 예측 정확도

## YOLO의 단점

- **많은 박스를 예측 후 NMS로 제거**하는 구조
- **NMS 한계**: 겹치는 객체(예: 사람 여러 명)가 있을 경우 잘 인식 못할 수 있음

---

#  DETR (DEtection TRansformer)

- Facebook AI에서 개발한 **Transformer 기반 객체 탐지 모델**

## 특징

- **Transformer Encoder-Decoder 구조** 사용 (입력: 이미지, 출력: 객체들)
- **Object Query**를 사용하여 예측 (YOLO처럼 anchor box가 없음)
- **NMS 사용하지 않음** (Hungarian Matching으로 1:1 매칭)
- **예측 box 수가 적고 깔끔**함
- **CNN + Transformer** 조합으로, 성능은 우수하나 연산량은 많음

> DETR는 YOLO처럼 빠르진 않지만, **정확하고 구조가 간단하며 후처리가 불필요**한 점에서 연구적으로 매우 흥미로운 모델이다.


