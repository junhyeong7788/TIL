# 🚀 학습 키워드

## 정의

`zip()` : 여러 개의 반복 가능한 (iterable) 객체의 요소를 순서대로 묶어서 튜플 형태로 반환하는 파이썬의 내장 함수

---

# 📝 개념

## 기본 문법

- `zip(iterable1, iterable2, ...)`
  - 각 iterable (리스트, 튜플 등)의 동일한 인덱스에 있는 요소를 묶어서 튜플을 생성
  - 길이가 다른 iterable을 전달하면 가장 짧은 iterable의 길이에 맞춰짐 (초과하는 요소는 무시)
  - 반환값은 zip 객체(반복자)로,` list()` 또는 `tuple()`로 변환하여 사용 가능

## 예제

```python
# 두개의 리스트 묶기
names = ["철수", "영희", "민수"]
scores = [85, 90, 88]

zipped = zip(names, scores)
print(list(zipped))  # [('철수', 85), ('영희', 90), ('민수', 88)]
```

```python
# 여러 개의 iterable 묶기
numbers = [1, 2, 3]
letters = ['A', 'B', 'C']
words = ["apple", "banana", "cherry"]

zipped = zip(numbers, letters, words)
print(list(zipped))
```

```python
# 길이가 다른 list 묶기
a = [1, 2, 3]
b = ['x', 'y']

print(list(zip(a, b)))  # [(1, 'x'), (2, 'y')]
```

```python
# zip을 활용한 언패킹
zipped = [(1, 'A'), (2, 'B'), (3, 'C')]
numbers, letters = zip(*zipped)

print(list(numbers))  # [1, 2, 3]
print(list(letters))  # ['A', 'B', 'C']
```

---

# ✨ 정리

- zip()은 여러 iterable을 병렬로 묶어주는 함수이다.
- zip()의 결과는 가장 짧은 iterable의 길이에 맞춰진다.
- zip(\*zipped)을 사용하면 언패킹이 가능하다.
- 딕셔너리 변환, 정렬, 여러 리스트 순회 등에 유용하게 활용 가능.
