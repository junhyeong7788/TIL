# 🚀 학습 키워드

- 교차검증과 최적 하이퍼 파라미터 튜닝
- 하이퍼 파라미터 : 머신러닝 알고리즘을 구성하는 주요 구성 요소, 이 값을 조정해 알고리즘의 예측 성능을 개선할 수 있다.
- 머신러닝을 할 때 데이터에 적합한 모델을 선택하는 것도 중요하지만 그것보다 더 중요한 것은 **최적의 하이퍼 파라미터 튜닝**을 하는 것
  - 하이퍼 파라미터를 직접 하나하나 넣고 결과를 도출하는 과정을 반복해야하는데 이럴때 유용하게 쓰인다.
- Grid(격자) : 촘촘하게 파라미터를 입력하면서 테스트를 하는 방식
  - 파라미터의 집합을 만들고 이를 순차적으로 적용하면서 최적의 파라미터를 찾는 방식

## 정의

- `GridSearchCV` : Classifier과 Regressor와 같은 알고리즘에 사용되는 하이퍼 파라미터를 순차적으로 입력하면서 최적의 파라미터를 도출할 수 있는 방안을 제공

- `GridSearchCV(estimator, param_grid, scoring, cv, refit=True, return_train_score=False)`
	  - estimator : classifier, regressor, pipeline
	  - param_grid : key + 리스트 값을 가지는 딕셔너리 (estimator 튜닝을 위한 파라미터)
	  - scoring : 예측 성능을 측정할 평가 방법
	  - cv : 교차 검증을 위해 분할되는 학습/테스트 세트의 개수
	  - refit : 최적의 하이퍼 파라미터를 찾은 뒤 입력된 estimator 객체를 해당 하이퍼 파라미터로 재학습 여부
	  - return_train_score : 학습 데이터에 대한 성능을 반환할지 여부

## 키워드
`GridSearchCV: 하이퍼 파라미터 튜닝을 위해 가능한 모든 파라미터 조합을 대상으로 교차 검증을 수행하여 최적의 매개변수를 찾는 방법으로, 일반화 성능을 높이는 데 유용하다.`

---

# 📝새로 배운 개념

## Grid Search

- 관심있는 매개변수들을 대상으로 가능한 모든 조합을 시도해보며 최적 하이퍼 파라미터 튜닝을 하는 것
- 알고리즘에 사용되는 하이퍼 파라미터를 순차적으로 입력하면서 편리하게 최적의 파라미터를 도찰할 수 있는 방안을 제공해주는 모듈

- Grid(격자) : 촘촘하게 파라미터를 입력하면서 테스트를 하는 방식
	  - 파라미터의 집합을 만들고 이를 순차적으로 적용하면서 최적의 파라미터를 찾는 방식

```python
grid_parameters = {'max_depth' : [1, 2, 3],
				   'min_samples_split' : [2, 3]} # 3 * 2 = 6개의 파라미터 조합
```

| 모델 훈련  | 매개변수 선택 | 모델 평가 |
| :--------: | :-----------: | :-------: |
| train data |  validation   | test data |

- Grid Search를 할 때 여러 가지 매개변수 값으로 많이 시도해보고 테스트 세트 정확도가 가장 높은 조합을 선택해야 함
- 만약 데이터가 train과 test데이터로만 나눴더라면 테스트 세트를 이미 사용했기 때문에 모델이 얼마나 좋은지 평가하는데 사용하지 못함.
- 그래서 train, validation, test set으로 나눠 `모델 훈련, 매개변수 선택, 최종 모델 평가` 를 각각 다른 데이터로 진행하면 더 정확한 모델을 만들 수 있다.

## GridSearch CV

- train과 validation, test를 나누는 방법에 모델은 민감하다.
- 일반화 성능을 더 잘 평가하려면 훈련 세트와 검증 세트를 한번만 나누지 않고, **교차검증을 사용해서 각 매개변수 조합의 성능을 평가**할 수 있다.
- 교차 검증을 같이하면서 그리드 서치를 한 번에 해주는 모델이 GridSearchCV이다.

```python
grid_parameters = {'max_depth' : [1, 2, 3],
				   'min_samples_split' : [2, 3]} # 3 * 2 = 6개의 파라미터 조합
```

- `3 * 2 = 6` , cv폴드를 3개로 나눴다면 `6 * 3 = 18` 이 되어 학습/검증하는 수행횟수가 총 18번됨

### DecisionTreeClassifier 예시

```python
from sklearn.datasets import load_iris
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import GridSearchCV

# 데이터를 로딩하고 학습데이타와 테스트 데이터 분리
iris = load_iris()
X_train, X_test, y_train, y_test = train_test_split(iris_data.data, iris_data.target, test_size=0.2, random_state=121)

dtree = DecisionTreeClassifier()

### parameter 들을 dictionary 형태로 설정
parameters = {'max_depth':[1,2,3],
              'min_samples_split':[2,3]}
```

- max_depth : 트리의 최대 깊이
- min_samples_split : 노드를 분할하기 위한 최소한의 샘플 데이터 수
	- 테스트할 하이퍼 파라미터 세트는 딕셔너리 형태, 하이퍼 파라미터의 명칭은 문자열 Key값으로, 하이퍼 파라미터의 값은 리스트 형태로 설정

```python
import pandas as pd

# param_grid의 하이퍼 파라미터들을 3개의 train, test set fold 로 나누어서 테스트 수행 설정.
### refit=True 가 default 임. True이면 가장 좋은 파라미터 설정으로 재 학습 시킴.
grid_dtree = GridSearchCV(dtree, param_grid=parameters, cv=3, refit=True)

# 붓꽃 Train 데이터로 param_grid의 하이퍼 파라미터들을 순차적으로 학습/평가.
grid_dtree.fit(X_train, y_train)

# GridSearchCV 결과 추출하여 DataFrame으로 변환
scores_df = pd.DataFrame(grid_dtree.cv_results_)
scores_df[['params', 'mean_test_score', 'rank_test_score', 'split0_test_score', 'split1_test_score', 'split2_test_score']]

print('GridSearchCV 최적 파라미터:', grid_dtree.best_params_)
print('GridSearchCV 최고 정확도: {0:.4f}'.format(grid_dtree.best_score_))

# GridSearchCV의 refit으로 이미 학습이 된 estimator 반환
estimator = grid_dtree.best_estimator_

# GridSearchCV의 best_estimator_는 이미 최적 하이퍼 파라미터로 학습이 됨
pred = estimator.predict(X_test)
print('테스트 데이터 세트 정확도: {0:.4f}'.format(accuracy_score(y_test,pred)))
```

- 일반적으로 학습 데이터를 GridSearchCV를 이용해 최적 하이퍼 파라미터 튜닝을 수행한 뒤에 별도의 테스트 세트에서 이를 평가하는 것이 일반적인 머신러닝 모델 적용 방법

---

# ✨
- GridSearchCV

---

# 🔗레퍼런스

## 참고 강의/글

- [GridSearchCV 공식문서](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)
