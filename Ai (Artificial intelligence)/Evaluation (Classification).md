# 🚀 학습 키워드

- Machine Learning : 데이터 가공/변환, 모델 학습/예측, 평가의 프로세스
- 머신러닝 모델은 여러 가지 방법으로 예측 성능을 평가할 수 있다.
- 일반적으로 *모델이 분류냐 회귀냐* 에 따라 여러 종류로 나뉨
	- 분류의 경우 실제 결과 데이터와 예측 결과 데이터가 얼마나 정확하고 오류가 적게 발생하는가에 따라 모델 성능을 평가
		- *정확도 (Accuracy), 정밀도(Precision), 재현율(Recall), F1 score, ROC-AUC 등*
	- 회귀의 경우 실제 값과 예측 값의 오차 평균값에 기반한 평가 지표가 사용됨
		- *MAE(Mean Absolute Error), MSE(Mean Squred Error), RMSE(Root Mean Squared Error) 등*

#### 분류 평가 지표
- 이진 분류 : 결정 클래스 값 종류의 유형에 따라 긍정/부정과 같은 2개의 결괏값만을 가짐
- 멀티 분류 : 여러 개의 결정 클래스 값을 가지는 것

## 정의
-  **정확도(Accuracy)**: 전체 예측 중 실제 값과 일치하는 예측의 비율.
-  **오차 행렬(Confusion Matrix)**: 분류 모델의 성능을 평가하는 도구로, 예측 오류 유형을 나타냄 (TP, TN, FP, FN).
-  **정밀도(Precision)**: Positive로 예측된 데이터 중 실제 Positive인 비율.
-  **재현율(Recall)**: 실제 Positive 중에서 올바르게 예측된 비율.
-  **F1 스코어**: 정밀도와 재현율의 조화 평균을 나타내는 지표.
-  **ROC 곡선(ROC Curve)**: FPR 대비 TPR의 변화를 나타내는 곡선.
- **AUC**: ROC 곡선 아래 면적을 의미하며, 분류 모델의 성능을 평가.

---

# 📝새로 배운 개념

## 정확도 (Accuracy)
- 실제 데이터에서 예측 데이터가 얼마나 같은지를 판단하는 지표
- $$Accuracy = \frac{예측 결과가 동일한 데이터 건수}{전체 예측 데이터 건수}$$
- *직관적*으로 모델 예측 성능을 나타내는 평가지표
- 이진 분류의 경우 데이터 구성에 따라 ML모델의 성능을 왜곡할 수 있음
	- 특히 정확도는 **불균형한 (imbalanced) 레이블 값 분포**에서 ML모델의 성능을 판단할 경우 적합한 평가 지표가 아님

```python
from sklearn.metrics import accuracy_score
print(accuracy_score(y_test, pred))
```

## 오차 행렬 (Confusion Matrix)
- 이진 분류에서 성능 지표로 잘 활용되는 오차행렬
	- 학습된 분류 모델이 예측을 수행하면서 얼마나 헷갈리고(confused) 있는지도 함께 보여주는 지표
- 이진 분류의 예측 오류가 얼마인지와 더불어 어떠한 유형의 예측 오류가 발생하고 있는지를 함께 나타내는 지표
- 오차 행렬은 4분면 행렬에서 실제 레이블 클래스 값과 예측 레이블 클래스 값이 어떠한 유형을 가지고 매핑되는지를 나타냄
	- TN (True Negative) : 예측값을 Negative 값 0으로 예측했고 실제 값 역시 Negative 값 0
	- FP (False Positive) : 예측값을 Positive 값 1로 예측했는데 실제 값은 Negative 값 0
	- FN (False Negative) : 예측값을 Negative 값 0으로 예측했는데 실제 값은 Positive 값 1
	- TP (True Positive) : 예측값을 Positive 값 1로 예측했는데 실제 값 역시 Positive 값 1

```python
from sklearn.metrics import confusion_matrix
confusion_matrix(y_test , pred)
```
- 출력된 오차행렬은 ndarray형태, 이진분류의 TN, FP, FN,FP는 상단 도표와 동일한 위치를 가지고 array에서 가져올 수 있음
- TP, TN, FP, FN 값은 Classifier 성능의 여러 면모를 판단할 수 있는 기반 정보를 제공
	- 이 값을 조합해 Classifier의 성능을 측정할 수 있는 주요 지표인 정확도, 정밀도, 재현율 값을 알 수 있음
- $$정확도 = \frac{예측 결과와 실제 값이 동일한 건수}{전체 데이터 수} = \frac{TN + TP}{TN + FP + FN + TP}$$
- 불균형한 이진 분류 데이터 세트에서는 Positive데이터 건수가 매우 작기 때문에 Negative로 예측 정확도가 높아지는 경향이 발생
	- 정확도 지표는 이러한 불균형한 데이터 세트에서 Positive에 대한 예측 정확도를 판단하지 못한 채 Negative에 대한 예측 정확도만으로 분류의 정확도가 매우 높게 나타나는 수치적인 판단 오류를 일으킬 수 있음
	- 이러한 한계를 극복하기 위해 정밀도(Precision)와 재현율(Recall)을 활용

## 정밀도(Precision)와 재현율(Recall)
- $$정밀도 = \frac{TP}{FP + TP}$$

- $$재현율 = \frac{TP}{FN + TP}$$
- 정밀도 : 예측을 Positive로 한 대상 중에 예측과 실제 값이 Positive로 일치한 데이터의 비율
	- Positive예측 성능을 더 정밀하게 측정하기 위한 평가 지표
	- 양성 예측도라고도 불림
- 재현율 : 실제 값이 Positive인 대상 중에 예측과 실제 값이 Positive로 일치한 데이터의 비율
	- 민감도(Sensitivity) 또는 TRP(True Positive Rate)로 불림
	- 민감도와 재현율은 같은 의미로 사용됨

- 정밀도가 상대적으로 더 중요한 지표인 경우는 실제 Negative 음성인 데이터 예측을 Positive양성으로 잘못 판단하게 되면 큰 영향이 발생하게 된다.
- 재현율이 상대적으로 더 중요한 지표인 경우는 실제 Positive 양성인 데이터 예측을 Negative로 잘못 판단하게 되면 큰 영향이 발생
- 재현율과 정밀도 모두 TP를 높이는데 동일하게 초점을 맞추지만, 재현율은 FN를 낮추는 데 ,정밀도는 FP를 낮추는데 초점을 맞춤
- 재현율과 정밀도는 **상호 보완적인 지표** 로 분류의 성능을 평가하는 데 적용

```python
from sklearn.metrics import accuracy_score, precision_score , recall_score , confusion_matrix

def get_clf_eval(y_test , pred):
	confusion = confusion_matrix( y_test, pred)
	accuracy = accuracy_score(y_test , pred)
	precision = precision_score(y_test , pred)
	recall = recall_score(y_test , pred)
	print('오차 행렬')
	print(confusion)
	print('정확도: {0:.4f}, 정밀도: {1:.4f}, 재현율: {2:.4f}'.format(accuracy , precision ,recall))
```

### 정밀도/재현율 Trade-off
- 분류 특성상 정밀도 또는 재현율이 특별히 강조돼야 할 경우 분류의 결정 임곗값(Threshold)을 조정해 정밀도 또는 재현율의 수치를 높일 수 있음
- 하지만 정밀도와 재현율은 상호 보완적인 평가 지표이기 떄문에 어느 한쪽을 강제로 높이면 **다른 하나의 수치는 덜어지기 쉬움**
- 이를 **정밀도/재현율의 트레이드 오프**라고 부름
- 사이킷런은 개별 데이터별로 예측 확률을 반환하는 메서드인 `predict_porba()`를 제공
	- 이를 이용하면 분류 결정 임곗값을 조정해 정밀도 또는 재현율의 수치를 높일 수 있음

| 입력 파라미터 |                                                         predict() 메서드와 동일하게 보통 테스트 피처 데이터 세트를 입력                                                          |
| :-----: | :-------------------------------------------------------------------------------------------------------------------------------------------------------: |
|  반환 값   | 개별 클래스의 예측 확률을 ndarray m x n (m : 입력 값의 레코드 수, n : 클래스 값 유형) 형태로 반환, 각 열은 개별 클래스의 예측 확률 입니다. 이진 분류에서 첫 번째 칼럼은 0 Negative의 확률, 두 번째 칼럼은 1 Positive의 확률을 의미 |
```python
pred_proba = lr_clf.predict_proba(X_test)
pred = lr_clf.predict(X_test)
print('pred_proba()결과 Shape : {0}'.format(pred_proba.shape))
print('pred_proba array에서 앞 3개만 샘플로 추출 \n:', pred_proba[:3])

# 예측 확률 array 와 예측 결과값 array 를 concatenate 하여 예측 확률과 결과값을 한눈에 확인
pred_proba_result = np.concatenate([pred_proba , pred.reshape(-1,1)],axis=1)
print('두개의 class 중에서 더 큰 확률을 클래스 값으로 예측 \n',pred_proba_result[:3])

```
- 반환된 결과인 ndarray는 0과 1에 대한 확률을 나타내므로 첫 번째 칼럼 값과 두 번째 칼럼 값을 더하면 1이 됨
- 그리고 맨 마지막 줄의 `predict()` 메서드의 결과 비교에서도 나타나듯이, 두개의 칼럼 중에서 더 큰 확률 값으로 predict() 메서드가 최종 예측
- `predict()` 는 `predict_proba()` 호출 결과로 반환된 배열에서 분류 결정 임곗값보다 큰 값이 들어 있는 칼럼의 위치를 받아서 최종적으로 예측 클래스를 결정하는 메서드 (이것을 이해하면 어떻게 정밀도/재현율 트레이드 오프를 구현했는지 도움이 된다.)
- 사이킷런은 분류 결정 임곗값을 조절해 정밀도와 재현율의 성능 수치를 상호 보완적으로 조정할 수 있음

### `precision_recall_curve()`를 이용하여 임곗값에 따른 정밀도-재현율 값 추출

| 입력 파라미터 | y_true : 실제 클래스 값 배열 (배열 크기 = [데이터 건수]) | probas_pred : Positive 칼럼의 예측 확률 배열 (배열 크기 = [데이터 건수]) |
| :-----: | :-------------------------------------: | :----------------------------------------------------: |
|  반환 값   |        정밀도 : 임계값별 정밀도 값을 배열로 반환         |                재현율 : 임계값별 재현율 값을 배열로 반환                |
- 임곗값을 계속 증가시킬수록 재현율 값이 낮아지고 정밀도 값이 높아지는 반대의 양상

### 정밀도와 재현율의 맹점
- Positive 예측의 임곗값을 변경함에 따라 정밀도와 재현율의 수치가 변경됨
- 이러한 변경은 업무 환경에 맞게 두 개의 수치를 상호 보완할 수 있는 수준에서 적용돼야 함
#### 정밀도가 100%가 되는 방법
- 확실한 기준이 되는 경우만 Positive로 예측하고 나머지는 Negative로 예측
#### 재현율이 100%가 되는 방법
- 모든 환자를 Positive로 예측하면 됨

## F1 스코어
- 정밀도와 재현율을 결합한 지표
- 정밀도와 재현율이 어느 한쪽으로 치우치지 않는 수치를 나타낼 때 상대적으로 높은 값을 가짐

- $$F1 = \frac{2}{\frac{1}{정밀도} + \frac{1}{재현율}} = 2 * \frac{정밀도 * 재현율}{정밀도 + 재현율}$$
```python
# f1_score 메서드
from sklearn.metrics import f1_score
f1 = f1_score(y_test , pred)
print('F1 스코어: {0:.4f}'.format(f1))
```

## ROC곡선과 AUC
- 이진 분류의 예측 성능 측정에서 중요하게 사용되는 지표
- ROC 곡선(Receiver Operation Characteristic Curve) : FPR(False Positive Rate)이 변할 때 TPR(True Positive Rate)이 어떻게 변하는지 나타내는 곡선

- `TPR`은 재현율을 나타내며, 민감도라고도 불림 ( $\frac{TP}{FN + TP}$ )
- `TNR(True Negative Rate)`은 특이성을 나타내며, 특이성이 높을수록 FPR은 낮음 ( $\frac{TN}{FP + TN}$ )
- ROC 곡선은 `FPR`을 X축으로, TPR을 Y축으로 잡으면 FPR 변화에 따른 TPR의 변화가 곡선 형태로 나타남

- $$FPR = \frac{FP}{FP + TN} = 1 - TNR = 1 - 특이성$$
### roc_curve() API
- `roc_curve()` : 사이킷런에서 ROC 곡선을 구하기 위한 API
- 입력 파라미터 : `y_true`(실제 클래스 값 배열), `y_score`(Positive 칼럼의 예측 확률 배열)
- 반환 값 : FPR, TPR, 임곗값
	- FPR : $fpr = FP / (FP + TN) = 1 - TNR = 1 - 특이성$
	- TPR : $tpr = TP / (FN + TP) = 재현율$
	- 임곗값 : roc_curve()는 일반적으로 FPR, TPR, 임곗값을 반환하며, 임곗값은 roc_curve()를 호출하면 반환값으로 받을 수 있음

```python
from sklearn.metrics import roc_curve

# 레이블 값이 1일때의 예측 확률을 추출
pred_proba_class1 = lr_clf.predict_proba(X_test)[:, 1]
fprs , tprs , thresholds = roc_curve(y_test, pred_proba_class1)

# 반환된 임곗값 배열에서 샘플로 데이터를 추출하되, 임곗값을 5 Step으로 추출.
# thresholds[0]은 max(예측확률)+1로 임의 설정됨. 이를 제외하기 위해 np.arange는 1부터 시작
thr_index = np.arange(1, thresholds.shape[0], 5)
print('샘플 추출을 위한 임곗값 배열의 index:', thr_index)
print('샘플 index로 추출한 임곗값: ', np.round(thresholds[thr_index], 2))

# 5 step 단위로 추출된 임계값에 따른 FPR, TPR 값
print('샘플 임곗값별 FPR: ', np.round(fprs[thr_index], 3))
print('샘플 임곗값별 TPR: ', np.round(tprs[thr_index], 3))
```

```python
# FPR의 변화에 따른 TPR의 변화를 ROC곡선으로 시각화
def roc_curve_plot(y_test , pred_proba_c1):
	
	# 임곗값에 따른 FPR, TPR 값을 반환 받음.
	fprs , tprs , thresholds = roc_curve(y_test ,pred_proba_c1)

	# ROC Curve를 plot 곡선으로 그림.
	plt.plot(fprs , tprs, label='ROC')

	# 가운데 대각선 직선을 그림.
	plt.plot([0, 1], [0, 1], 'k--', label='Random')

	# FPR X 축의 Scale을 0.1 단위로 변경, X,Y 축명 설정등
	start, end = plt.xlim()
	plt.xticks(np.round(np.arange(start, end, 0.1),2))
	plt.xlim(0,1); plt.ylim(0,1)
	plt.xlabel('FPR( 1 - Specificity )'); plt.ylabel('TPR( Recall )')
	plt.legend()
	plt.show()
	
roc_curve_plot(y_test, lr_clf.predict_proba(X_test)[:, 1] )
```

```python
from sklearn.metrics import roc_auc_score
pred_proba = lr_clf.predict_proba(X_test)[:, 1]
roc_score = roc_auc_score(y_test, pred_proba)
print('ROC AUC 값: {0:.4f}'.format(roc_score))
```
---

# ✨
- 정확도, 오차행렬, 정밀도, 재현율, F1스코어, ROC/AUC REMIND

---
