# 🚀 Regularization - Dropout

### 🎯 주요 키워드

- Dropout은 Deep Learning 에서 모델의 일반화 성능을 높이기 위한 Regularization 기법

---

# 📝 새로 배운 개념

## 🏷 Dropout

- **정의** : 서로 연결된 연결망(layer) 에서 0부터 1사이의 확률로 뉴런을 제거(drop)하는 기법
- **핵심 내용**

  - 어떤 특정한 설명변수 Feature만 과도하게 집중하여 학습함으로써 발생할 수 있는 Overfitting을 방지하기 위해 사용 -> 편향되지 않은 출력값
  - Mini-batch 학습 : 각 batch 별로 적용되는 것을 알 수 있다.
  - **Test 시에는 모든 뉴런이 활성화되기 때문에, 학습 단계에서 Dropout으로 꺼졌던 뉴런을 고려해 출력값을 보정해야 한다.**
    - 학습 시에는 일부 뉴런만 사용되므로 출력값의 스케일이 작고, 테스트 시에는 모든 뉴런이 활성화되므로 출력값이 커질 수 있다.
    - 이를 보정하기 위해 테스트 단계에서는 각 뉴런의 출력에 Dropout 확률만큼 스케일링을 적용하여 학습 시와 동일한 평균 출력 스케일을 유지한다.

- **예시:**

  - Train

  ```python
  import torch.nn as nn

  model = nn.Sequential(
      nn.Linear(128, 64),
      nn.ReLU(),
      nn.Dropout(0.5),  # 50% 확률로 뉴런 drop
      nn.Linear(64, 10)
  )
  ```

  - Test

  ```python
  import torch
  import torch.nn as nn

  # 간단한 모델 정의 (Dropout 포함)
  class DropoutModel(nn.Module):
      def __init__(self):
          super(DropoutModel, self).__init__()
          self.layer1 = nn.Linear(10, 5)
          self.dropout = nn.Dropout(p=0.5)  # 학습 시 50% 뉴런 drop
          self.output = nn.Linear(5, 1)

      def forward(self, x):
          x = self.layer1(x)
          x = torch.relu(x)
          x = self.dropout(x)  # 학습 시에만 활성화됨
          x = self.output(x)
          return x

  # 더미 입력값
  x = torch.randn(1, 10)

  # 모델 생성
  model = DropoutModel()

  # === 학습 모드 (dropout 활성화) ===
  model.train()
  train_output = model(x)
  print("학습 모드 출력:", train_output)

  # === 평가 모드 (dropout 비활성화 + scaling 적용) ===
  model.eval()
  test_output = model(x)
  print("테스트 모드 출력:", test_output)
  ```

---

# 💡 적용 및 활용

### 🔍 실전 적용 예시

- **자율주행 자동차의 이미지 인식**  
  자율주행 시스템은 카메라로부터 받은 이미지 데이터를 기반으로 도로, 보행자, 차량 등을 인식합니다. 이때 CNN 기반 딥러닝 모델이 사용되며, Dropout은 모델이 특정 도로나 물체 특징에 과도하게 의존하지 않도록 하여 일반화 성능을 높이는 데 활용됩니다.

- **의료 영상 분석 모델**  
  CT, MRI, X-ray 등의 의료 이미지를 분석할 때는 환자마다 해부학적 구조가 다르고 노이즈도 존재합니다. Dropout은 모델이 특정 환자나 특정 장기의 형태에만 편향되지 않도록 도와주며, 다양한 환자군에 대해 안정적인 예측 성능을 유지하도록 합니다.

---

# 🔗 레퍼런스

## 참고 강의/글

- [딥러닝 모델 성능 개선하는 법](https://facerain.github.io/improve-dl-performance/)
- [[딥러닝] Drop-out(드롭아웃) 개념, 사용이유, 수식](https://heytech.tistory.com/127)
