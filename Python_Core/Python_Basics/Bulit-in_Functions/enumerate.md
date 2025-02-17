# 🚀 학습 키워드

## 정의

`enumerate()` : 반복 가능한(iterable) 객체의 각 요소에 인덱스를 부여하여 (인덱스, 값) 형태의 튜플을 반환하는 내장 함수

---

# 📝 개념

## 기본 문법

- `enumerate(iterable, start=0)`
  - iterable : 순회할 (반복 가능한) 객체
  - start (선택적) : 인덱스 시작 값 (default = 0)

## 예제

```python
# 1: 리스트에서 인덱스와 값 함께 출력
fruits = ["사과", "바나나", "체리"]

for index, value in enumerate(fruits):
    print(index, value)
```

```python
# 2: 인덱스 시작 값 지정
fruits = ["사과", "바나나", "체리"]

for index, value in enumerate(fruits, start=1):
    print(index, value)
```

```python
# 3: enumerate()를 리스트로 변환
numbers = [100, 200, 300]
result = list(enumerate(numbers))

print(result)
```

```python
# 4: enumerate()를 활용한 딕셔너리 변환
names = ["Alice", "Bob", "Charlie"]
name_dict = dict(enumerate(names, start=1))

print(name_dict)
```

---

# ✨ 정리

- enumerate()는 인덱스를 자동으로 부여하며, (인덱스, 값) 형태의 튜플을 반환
- 기본적으로 인덱스는 0부터 시작하지만, start 인자를 통해 변경 가능
- for 문에서 인덱스를 추출할 때 유용하며, range(len(iterable))보다 가독성이 뛰어남
