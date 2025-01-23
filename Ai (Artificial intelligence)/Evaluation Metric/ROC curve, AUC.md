# 🚀 학습 키워드

## 키워드

- ROC curve : 좌상단에 붙어있는 커브가 더 좋은 분류기를 의미
- ROC 곡선에서 추출된 값 : **AUC (Area Under the Curve)** 평가지표

---

# 📝새로 배운 개념

## ROC 정의

- ROC Curve (Receiver Operating Characteristic Curve) : `다양한 threshold에 대한 이진 분류기의 성능을 한번에 표시한 것`
  - 평가 도구 또는 시각화 방법으로 이진 분류(Binary Classification) 문제에서 모델의 성능을 평가하기 위해 사용되는 시각화 도구
  - 이진분류의 성능 : FPR(False Positive Rate)와 TPR(True Positive Rate) 의 변화를 **시각화** 하여 분류 모델의 성능을 표현

### TPR, FPR의 관계

- X축 (FPR) : 거짓 양성 비율 (False Positive Rate) = FP / (FP + TN) `= 이진 분류기에 의해 결정된 score가 표시`
- Y축 (TPR) : 참 양성 비율 (True Positive Rate) = TP / (FN + TP) , aka 재현율(Recall)

### 현 위의 점의 의미

- threshold가 변함에 따라 FPR과 TPR의 값이 바뀜
  - threshold가 높아지거나 낮아지거나 FPR과 TPR은 어느정도 비례적으로 함께 커지거나 작아짐
  - 현 위의 점이 의미하는 것 : `모든 가능한 threshold별 FPR과 TPR을 알아보겠다는 의미`

### 현의 휨 정도의 의미

- 두 클래스를 더 잘 구별할 수 있다면 ROC커브는 좌상단에 더 가까워지게 됨

## AUC 정의

- AUC (Area Under the Curve) : ROC Curve의 아래 면적을 의미
  - 0과 1 사이의 값을 가지며, 값이 클수록 (1에 가까울수록) 모델 성능이 좋음을 나타냄

### AUC의 의미

- AUC = 1 : 완벽한 분류기
- AUC = 0.5 : 무작위 예측 (성능이 나쁘지 않지만 쓸모없음)
- AUC < 0.5 : 잘못된 분류기 (모델이 성능이 나쁨)

### 계산 방법

- 면적 계산 : 사다리꼴 법칙과 적분같은 방식이 존재한다.
- Python을 이용한 계산

  ```python
  from sklearn.metrics import roc_auc_score

  # 실제값과 예측 확률
  y_true = [0, 0, 1, 1]          # 실제 클래스
  y_scores = [0.1, 0.4, 0.35, 0.8]  # 모델의 예측 확률

  # AUC 계산
  auc = roc_auc_score(y_true, y_scores)
  print("AUC:", auc)

  ```

- ROC curve 시각화와 AUC
  ```python
  from sklearn.metrics import roc_curve, auc
  import matplotlib.pyplot as plt

  # ROC Curve 계산
  fpr, tpr, _ = roc_curve(y_true, y_scores)
  roc_auc = auc(fpr, tpr)

  # ROC Curve 시각화
  plt.figure()
  plt.plot(fpr, tpr, label=f"ROC curve (area = {roc_auc:.2f})")
  plt.plot([0, 1], [0, 1], linestyle='--', color='gray')  # 대각선 기준선
  plt.xlabel("False Positive Rate")
  plt.ylabel("True Positive Rate")
  plt.title("ROC Curve")
  plt.legend(loc="lower right")
  plt.show()
  ```

---

# 💻활용 사례

- ROC curve 자체는 시각화 도구이며, 모델의 성능을 다양한 임계값(threshold)에서 비교할 수 있게 도와준다.
- AUC (ROC Curve의 면적)는 수치로 표현되는 평가지표이다.

---

# 🔗레퍼런스

## 참고 강의/글

- [ROC curve (공돌이의 수학정리노트)](https://angeloyeo.github.io/2020/08/05/ROC.html)
