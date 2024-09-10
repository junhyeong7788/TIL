# 🚀 학습 키워드

## 정의
- `K-Fold cross_validation` : K개의 데이터 폴드 세트를 만들어 K번 만큼 각 폴드 세트에 학습과 검증 평가를 반복적으로 수행하는 방법

## 키워드 
`K-Fold 교차 검증: 데이터를 K개의 폴드로 나누어 각 폴드마다 학습과 검증을 반복해 모델 성능을 평가하는 방법으로, 불균형한 데이터에서는 Stratified K-Fold를 사용하여 레이블 분포를 균일하게 유지한다.`

---

# 📝새로 배운 개념

## K-Fold
- K개의 예측 평가를 구했으면 이를 평균해서 K폴드 평가 결과로 반영
	- ex : K=5, 총 5개의 폴드세트에 5번의 학습과 검증 평가 반복 수행
- 사이킷런은 KFold와 StratifiedKFold 클래스를 통해 교차 검증 분할을 수행할 수 있는 클래스 제공

```python
from sklearn.model_selection import KFold

iris = load_iris()
features = iris.data
label = iris.target
dt_clf = DecisionTreeClassifier(random_state=156)

# 5개의 폴드 세트로 분리하는 KFold 객체와 폴드 세트별 정확도를 담을 리스트 객체 생성
kfold = KFold(n_splits=5) # n_splits : int, default=5 (최소 2이상)
cv_accuracy = []
print('붓꽃데이터 세트 크기 : ', features.shape[0])

import numpy as np
n_iter = 0

# KFold 객체의 split()를 호출하면 폴드별 학습용, 검증용 테스트의 로우 인덱스를 array로 반환
for train_index, test_index in kfold.split(features):
	# kfold.spilt()으로 반환된 인덱스를 이용해 학습용, 검증용 테스트 데이터 추출
	X_train, X_test = features[train_index], features[test_index]
	y_train, y_test = label[train_index], label[test_index]

	#학습 및 예측
	dt_clf.fit(X_train, y_train)
	pred = dt_clf.predict(X_test)
	n_iter += 1

	# 반복 시마다 정확도 측정
	accuracy = np.round(accuracy_score(y_test, pred), 4)
	train_size = X_train.shape[0]
	test_size = X_test.shape[0]

	print('\n#{0} 교차 검증 정확도 :{1}, 학습 데이터 크기: {2}, 검증 데이터 크기: {3}'.format(n_iter, accuracy, train_size, test_size))
	print('#{0} 검증 세트 인덱스 :{1}'.format(n_iter, test_index))
	cv_accuracy.append(accuracy)

# 개별 iteration별 정확도를 합하여 평균 정확도 계산
print('\n## 평균 검증 정확도:', np.mean(cv_accuracy) )
```
- 위 과정의 검증 세트의 인덱스를 보면 교차검증 시마다 split()함수가 어떻게 인덱스를 할당하는지 알 수 있다.
## Stratified K-Fold
- 불균형한(imbalanced)분포도를 가진 레이블 데이터 집합을 위한 K fold 방식
	- 불균형한 분포도를 가진 레이블 데이터 집합 : 특정 레이블 값이 특이하게 많거나 매우 적어서 값의 분포가 한 쪽으로 치우치는 것
	- 레이블 데이터 집합이 원본 데이터 집합의 레이블 분포도를 학습 및 테스트 세트에 제대로 분배하지 못하는 경우의 문제를 해결
	- 원본 데이터의 레이블 분포도를 먼저 고려한 뒤 이 분포와 동일하게 학습 검증 데이터 세트를 분배

```python
# Stratified Kfold
from sklearn.model_selection import StratifiedKFold

skf = StratifiedKFold(n_splits=3)
n_iter=0

for train_index, test_index in skf.split(iris_df, iris_df['label']):
	n_iter += 1
	label_train= iris_df['label'].iloc[train_index]
	label_test= iris_df['label'].iloc[test_index]
	print('## 교차검증: {0}'.format(n_iter))
	print('학습 레이블 데이터 분포:\n' , label_train.value_counts())
	print('검증 레이블 데이터 분포:\n', label_test.value_counts())

df_clf = DecisionTreeClassifier(random_state=156)
skfold = StratifiedKFold(n_splits=3)
n_iter = 0
cv_accuracy = []

# StratifiedKFold의 split()호출 시 반드시 레이블 데이터 세트도 추가 입력 필요
for train_index, test_index in skfold.split(features, label):

	# split()으로 반환된 인덱스를 이용해 학습용, 검증용 테스트 데이터 추출
	X_train, X_test = features[train_index], features[test_index]
	y_train, y_test = label[train_index], label[test_index]

	# 학습 및 예측
	dt_clf.fit(X_train, y_train)
	pred = dt_clf.predict(X_test)

	# 반복 시마다 정확도 측정
	n_iter += 1
	accuracy = np.round(accuracy_score(y_test, pred), 4)
	train_size = X_train.shape[0]
	test_size = X_test.shape[0]

	print('\n#{0} 교차 검증 정확도 : {1}, 학습 데이터 크기 : {2}, 검증 데이터 크기 : {3}'.format(n_iter, accuracy, train_size, test_size))
	print('#{0} 검증 세트 인덱스:{1}'.format(n_iter, test_index))
	cv_accuracy.append(accuracy)

# 교차 검증별 정확도 및 평균 정확도 계산
print('\n## 교차 검증별 정확도:', np.round(cv_accuracy, 4))
print('\n## 평균 검증 정확도:', np.round(np.mean(cv_accuracy), 4))
```

- 분류에서의 교차검증은 Stratified K폴드 방식으로 분할되어야 한다.
	- 회귀의 결정값은 이산값 형태의 레이블이 아니라 연속된 숫자이기 때문에 결정값별로 분포를 정하는 의미가 없기 때문이다.

---
# ✨
### 교차 검증의 과정 요약
1. 폴드 세트 설정
2. for 루프 반복으로 학습 및 테스트 데이터의 인덱스 추출
3. 반복적 학습과 예측을 수행, 예측 성능을 반환
4. 폴드 세트별로 예측 성능을 평균하여 최종 성능 평가

---
# 🔗레퍼런스

## 참고 강의/글

- [### 교차 검증(Cross Validation)이란? 교차 검증의 종류 및 사용법](https://day-to-day.tistory.com/32)
- [[cross-validation]]
