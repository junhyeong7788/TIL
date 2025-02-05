# 🚀 학습 키워드

## 정의

- AutoML : 머신러닝에 필요한 데이터 전처리, 모델 튜닝, 학습 등 여러 수행사항들을 쉽고 간단하게 코드 몇 줄을 통해 자동화하는 도구

## 키워드

- `AutoML 도구`, `MLJAR에서 만든 mljar-supervised`

---

# 📝새로 배운 개념

## mljar-supervised

- MLJAR 팀에서 만든 automl 툴 (mljar-supervised)
- Feature Engineering을 해주며 결과에 대한 분석 및 시각화까지 해준다는 장점

### mljar의 학습 방식

- `baseline`을 두고 ml로 예측이 가능한 데이터인 지를 확인

  - 무지성 예측을 했을 때 결과를 `baseline`으로 둠
  - logloss는 작을수록 좋은 모델인데, `baseline`의 성능이 가장 뛰어나다.
    - ML로 예측이 되지 않는 데이터로 가정 수립과 데이터 수집부터 다시 수행해야 한다는 의미

- `MODE`

  - Explain : 데이터 이해
  - Perform : 배포를 위한 학습
  - Compete : 대회 참가를 위한 학습

- `Algorithm`
  - 랜덤 포레스트, ExtraTrees, XGBoost, LightGBM, CatBoost, KNN, DNN 및 앙상블 모델

## 설치

- `pip install mljar-supervised`
- `conda install -c conda-forge mljar-supervised`

## MODE

### Explain (default)

- 처음 데이터를 확인하고 분석할때 적절하게 사용 가능
  - 75:25 train/test split
  - Baseline, Linear, Decision Tree, Random Forest, Xgboost, Neural Network 모델을 사용
  - Report에 learning curve, importance plot, SHAP plot을 제공

### Perform

- 5-fold CV
- Linear, RandomForest, LightGBM, Xgboost, CatBoost, Neural Network 모델을 사용
- Report에 learning curve와 importance plot을 제공

- 1차 학습
  - 기본 알고리즘들로 학습을 진행
  - 하이퍼 파라미터 튜닝 (랜덤 서치)
- Feature Engineering
  - Golden Features
    - 모든 feature 중 한 쌍을 골라 가능한 모든 연산에 대한 새로운 feature 생성
    - 각 feature만으로 예측 모델을 만들고 모델을 평가하여, 성능이 가장 좋은 N개의 feature를 선정
  - Feature Selection
    - 학습 데이터에 랜덤 feature를 추가, 1차 학습 때의 best model로 재학습
    - 각 feature의 중요도를 측정하여 중요도가 낮은 feature를 제거
- 2차 학습
  - Feature Engineering이 끝난 feature로 하이퍼 파라미터 튜닝
  - 앙상블, 스태킹 모델 생성

### Compete

- 대회 참가를 위한 학습 , 시간이 오래 걸리지만 성능이 좋다.
- 데이터셋의 크기와 total_time_limit 파라미터에 따라서 validation strategy가 알아서 선택
  - 80:20 train/test split / 5-fold CV / 10-fold CV 셋 중 하나를 사용
- Linear, Decision Tree, Random Forest, Extra Trees, LightGBM, Xgboost, CatBoost, Neural Network, Nearest Neighbors 모델을 사용
- 앙상블과 스태킹을 사용한다.
- Report에 learning curve만 제공

---

# ✨

- 📌 예측값 생성, 📌 평가 지표 계산

```python
from supervised.automl import AutoML

# AutoML 모델 생성 (GPU 사용 가능하도록 설정)
automl = AutoML(
    algorithms=["LightGBM", "CatBoost", "Xgboost", "Extra Trees"],  # ✅ XGBoost & ExtraTrees 추가
    mode="Compete",
    total_time_limit=3600,  # 실행 시간 제한 (초 단위, 1시간)
    eval_metric="auc",  # ✅ ROC-AUC
    random_state=42,
    ml_task="binary_classification",  # 이진 분류 문제
    train_ensemble=True,  # ✅ 앙상블 학습 사용 여부
    optuna_time_budget=3600,  # ✅ 하이퍼파라미터 튜닝 시간
    n_jobs=-1  # ✅ CPU 코어를 최대한 활용
)

automl.fit(X_train, y_train)

# 모델 예측
y_pred = automl.predict(X_test)

# 확률 예측 (ROC-AUC 평가를 위해)
y_pred_proba = automl.predict_proba(X_test)[:, 1]  # 1 클래스에 대한 확률값
```

- 📌 평가 지표 계산

```python
from sklearn.metrics import roc_auc_score, accuracy_score, classification_report

# AUC-ROC 점수
auc_score = roc_auc_score(y_test, y_pred_proba)
print(f"🎯 ROC-AUC Score: {auc_score:.4f}")

# 정확도 (Accuracy)
accuracy = accuracy_score(y_test, y_pred)
print(f"✅ Accuracy: {accuracy:.4f}")

# 상세 성능 지표 출력
print(classification_report(y_test, y_pred))
```

- 📌 피처 중요도 시각화

```python
import matplotlib.pyplot as plt

# 모델별 피처 중요도 확인
importance_df = automl.report()  # AutoML이 생성한 보고서

# 중요도 출력
importance_df = importance_df[["name", "importance"]].sort_values(by="importance", ascending=False)

# 시각화
plt.figure(figsize=(10, 6))
plt.barh(importance_df["name"], importance_df["importance"])
plt.xlabel("Feature Importance")
plt.ylabel("Features")
plt.title("Feature Importance of AutoML Model")
plt.gca().invert_yaxis()
plt.show()
```

- 📌 모델 저장

```python
import joblib

# 모델 저장
joblib.dump(automl, "automl_model.pkl")
print("✅ 모델이 automl_model.pkl 파일로 저장되었습니다.")
```

- 📌 저장된 모델 로드 후 예측

```python
# 모델 로드
loaded_model = joblib.load("automl_model.pkl")

# 새로운 데이터 예측
new_predictions = loaded_model.predict(X_test)
print(new_predictions)
```

---

# 🔗레퍼런스

## 참고 강의/글

- [mljar-supervised 사용법](https://www.ai-bio.info/usage/mljar-supervised-usage)
