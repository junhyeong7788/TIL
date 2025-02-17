# 🚀 학습 키워드
## 키워드 
- TabNet 모델 학습 후 예측 결과를 test.csv파일의 target값으로 주어주고 submission.csv 파일에 저장 후 제출하여 F1 score 확인하는 부분에서 많은 시간을 할애했다.

---

# 📝새로 배운 인사이트

## 개념 : 모델 저장 및 모델 불러오기 및 예측 수행

```python
# prompt: TabNetClassifier 모델 저장 및 모델 불러오기 및 예측 수행

# 모델 저장
saving_path_name = "/content/drive/MyDrive/tabnet_model_test_1"
saved_filepath = clf.save_model(saving_path_name)

# 모델 불러오기
loaded_clf = TabNetClassifier()
loaded_clf.load_model(saved_filepath)
```

## 개념 : 열 개수가 안맞으면 여분 열을 추가하여 target값을 저장

```python
# 모델이 48개의 특징을 기대하므로, 1개의 특징을 추가합니다.
df_test_x['extra_feature'] = 0 # 예를 들어 임의의 값을 넣을 수 있습니다.

# 예측 시도
target = loaded_clf.predict(df_test_x.values)
df_test_x['target'] = target
```

# 개념 : 제출 파일 작성

```python
# 제출 데이터 읽어오기 (df_test는 전처리된 데이터가 저장됨)
df_sub = pd.read_csv("submission.csv")
df_sub["target"] = df_test_x

# 제출 파일 저장
df_sub.to_csv("submission.csv", index=False)
```

# 잘못 파악한 부분 : 예측 변수 저장

```python
# 예측 및 정확도 평가
pred = clf.predict(X_test)
accuracy = np.round(accuracy_score(y_test, pred), 4)
train_size = X_train.shape[0]
test_size = X_test.shape[0]
```
- 위 부분에서 pred 변수는 train_date 셋에서 가져온것 -> (940, )
	- df_test_x -> (17361, 47)
- 그래서 예측을 시도하고 `df_test_x['target']`에 저장할 때는 아래와 같이 진행하여야한다.
```python
# 예측 시도
target = loaded_clf.predict(df_test_x.values)
df_test_x['target'] = target
```

---

# ✨느낀 점
- 변수와 함수에 대해 생각하고 이해하기
- LG Aimers을 진행하면서 코딩 실력이 상당히 부족하다는 것을 깨닫고 있다.
- 프로그램 끝나고 다시 차근차근 복습하는 과정을 가지면 아주 좋을 것 같다.

---