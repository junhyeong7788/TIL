# 🚀 학습 키워드

- 과적합 (overfitting) : 모델이 학습데이터에만 과도하게 최적화되어, 실제 예측을 다른 데이터로 수행할 경우에는 예측 성능이 과도하게 떨어지는 것
- 데이터는 이상치, 분포도, 다양한 속성값, 피처 중요도 등 여러가지 ML에 영향을 미치는 요소를 가지고 있다.
- 특정 ML 알고리즘에서 최적으로 동작할 수 있도록 데이터를 선별해 학습한다면 실제 데이터 양식과는 많은 차이가 있을 것이다 => 성능저하

## 정의

- `교차 검증 (cross-validation)` : 데이터 편중을 막기 위해 별로 여러 세트로 구성된 학습 데이터 세트와 검증 데이터 세트에서 학습과 평가를 수행하는 것
  - 대부분의 ML 모델의 성능 평가는 교차 검증 기반(`학습데이터를 학습과 검증데이터로 나눠서`)으로 1차 평가를 한 뒤에 최종적으로 테스트 데이터 세트에 적용해 평가하는 프로세스
  - ML에 사용되는 데이터 세트를 세분화해서 학습, 검증, 테스트 데이터 세트로 나눔

## 키워드

`교차 검증 (Cross Validation): 모델의 일반화 성능을 높이기 위해 학습 데이터를 여러 세트로 나누어 반복 평가하는 기법으로, K-fold, LOOCV, Shuffle Split 등 다양한 방식이 있으며, 연산 비용이 높은 대신 데이터 편중을 방지하여 정확한 성능 평가가 가능하다.`

---

# 📝새로 배운 개념

## 교차 검증 방법의 종류

- `K-fold 교차 검증`
  - K개의 폴드 세트를 만들어서 k번의 학습과 검증을 마치고, 각 검증 평가의 평균을 낸 것인 최종 검증 평가
  - 1.  순서대로 나열된 레이블에 적요한 교차검증 (k-fold)
  - 2.  클래스의 분포 비율에 맞게 폴드를 만드는 교차 검증 (stratified k-fold)
- `LOOCV (Leave-one-out Cross-validation)` : 폴드 하나에 샘플 하나만 들어있는 k-겹 교차 검증
  - 총 N(샘플 수)번의 모델을 만들고, 각 모델을 만들 때 전체 train dataset중에 하나만의 데이터만 validation dataset으로 두고, 나머지는 모두 train dataset으로 사용
- `임의 분할 교차 검증(shuffle split)` : train_size만큼의 포인트로 훈련 세트를 만들고, test_size만큼의 (train dataset과 중첩되지 않는)포인트로 테스트 세트를 만들도록 분할한다.
- `그룹별 교차 검증(Group K-fold)` : 데이터 안에 매우 연관된 그룹이 있을 때 그룹별 교차검증을 사용
- `반복 교차 검증(Repeated Stratified K-fold)` : cross_val_score함수의 cv매개변수에 전달하여 교차 검증을 반복할 수 있다. 반복할 때마다 서로 다른 분할이 생성된다는 것이 특징

### 교차 검증의 장단점

- 장점
  - 모델의 일반화를 평가하기 위해 test data로 정확도 평가로 사용하는데 `분류하기 어려운 샘플들`이 모두 테스트 데이터로 들어간다면 그 모델의 정확도는 떨어진다
  - 위 경우를 막기 위해 교차 검증 방법을 사용하면 적어도 모든 샘플 데이터는 폴드 중 하나에 속하고, 한 번씩 테스트 데이터 세트가 되기 때문에 일반화를 평가하기 좋다.
  - 각 폴드별로 정확도의 평균을 구하는 것이기 때문에 결국 테스트 셋에 있는 모든 샘플에 대해 모델이 잘 일반화되어야한다.
- 단점 : 한번의 검증만 거쳐서 평가하는 것이 아니라 여러 번 검증을 하며 전체 평균을 내는 것이기 때문에 연산 비용이 늘어난다는 단점

## 교차검증 간편하게 - cross_val_score()

- `cross_val_score()` : 위의 과정을 한꺼번에 수행해주는 API
- API의 선언형태 : `cross_val_score(estimator, X, y=None, scoring=None, cv=None, n_jobs=1, verbose=0, fit_params=None, pre_dispatch='2*n_jobs')`
  - estimator : 사이킷런의 분류 알고리즘 클래스인 Classifier 또는 회귀 알고리즘 클래스인 Regressor
  - X : 피처 데이터 세트
  - y : 레이블 데이터 세트
  - scoring : 예측 성능 평가 지표
  - cv : 교차 검증 폴드 수
  - 반환값 : scoring 파라미터로 지정된 성능 지표 측정값을 배열 형태로 반환

```python
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import cross_val_score , cross_validate
from sklearn.datasets import load_iris

iris_data = load_iris()
dt_clf = DecisionTreeClassifier(random_state=156)

data = iris_data.data
label = iris_data.target

# 성능 지표는 정확도(accuracy) , 교차 검증 세트는 3개
scores = cross_val_score(dt_clf , data , label , scoring='accuracy',cv=3)
print('교차 검증별 정확도:',np.round(scores, 4))
print('평균 검증 정확도:', np.round(np.mean(scores), 4))
```

- `cross_val_score()`는 cv로 지정된 횟수만큼 `scoring` 파라미터로 지정된 평가 지표로 평가 결과값을 배열로 반환
- 일반적으로 `cross_val_score()`는 평가 결과값의 평균을 평가 수치로 사용
  - 코드를 수행한 예제와 Stratified KFold가 각 교차 검증별 정확도와 평균 검증 정확도가 모두 동일 (= 내부적으로` Stratified KFold`를 이용한다는 것을 알 수 있다.)

---

# ✨

- 교차 검증 방법의 종류, 교차 검증의 장단점, cross_val_score()
- 교차검증은 데이터편중을 방지하여 정확한 성능평가가 가능하다.

---

# 🔗레퍼런스

## 참고 강의/글

- [### 교차 검증(Cross Validation)이란? 교차 검증의 종류 및 사용법](https://day-to-day.tistory.com/32)
- [TIL K-Fold, StratifiedKFold.md](https://github.com/junhyeong7788/TIL/blob/77b3e6ca41efbf56d47549a7da56cf49920530c6/Python/Scikit-Learn/K-Fold%2C%20StratifiedKFold.md)
