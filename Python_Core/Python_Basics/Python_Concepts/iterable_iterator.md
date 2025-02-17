# 🚀 학습 키워드

## 정의

- `iterable` : 내부에 `__iter__` 메서드가 있는 모든 객체이며, 순회할 수 있는 객체이고 재사용이 가능
- `iterator` : iterable객체에서 `__iter__` 메서드를 통해 생성되는 객체, 상태가 존재하기 때문에 한번 순회하면 재사용할 수 없음

## 키워드 1

- 학습 내용을 정리해보세요.

---

# 📝새로 배운 개념

## 개념 1 : Iterable 객체 확인하는 방법
- iterable 에는 list, 문자열, dictionary, tuple, set과 같은 자료 유형이 해당
```python
from typing import Iterable

print(isinstance([1,2,3], Iterable)) # True
print(isinstance('python', Iterable)) # True
print(isinstance({1 : 'one', 2  : 'two'}, Iterable)) # True
print(isinstance((5,6,7), Iterable)) # True
print(isinstance(set([5,6,7]), Iterable)) # True
```

- 내부에 `__iter__` 메서드가 있으면  모드 Iterable객체로 인식할까?
```python
class Temp:
	def __init__(self):
		pass
	def __iter__(self, start, end):
		pass

print(isinstance(Temp(), Iterable)) # True
```

## 개념  2 : Iterator객체 확인하는 방법
- Iterable 객체에서 `__iter__` 메서드를 통해 생성되는 객체, 상태가 존재하기 때문에 한번 순회하면 재사용할 수 없다.
	- 내부에  존재하는 `__next__` 메서드를 통해 다음 값을 하나씩 차례대로 반환한다. 마지막 원소까지 접근하여, 더 이상 반환할 수 있는 값이 없다면 StopIteration에서를 반환하며 순회를 종료
```python
L = [1,2,3,4,5]
itorator_L = L.__iter__()

print(type(itorator_L)) # <class 'list_iterator'>
```

```python
# iterator 객체인지 확인하는 방법
from typing import Iterator
print(isinstance(itorator_L,Iterator)) # True
```

## 차이점
1. 
- iterable 객체의 경우, 순회 당하는 객체
- iterator 객체는 순회를 주관하는 객체

2. 
- iterable은 재사용할 수 있지만, iterator는  재사용할 수 없다.
```python
L = [1,2,3,4,5]
iterator_L = L.__iter__()
```
```python
for i in iterator_L:
	print(i, end = '') # 12345 다시 실행하면 아무 결과값이 나오지 않는다.
```


---

# ✨
- iterable 객체는 순회당하고, iterator 객체는 순회를 주관

---
# 🔗레퍼런스

## 참고 강의/글

- [# [파이썬] iterable과 iterator 의 차이가 뭐예요?](https://velog.io/@clueless_coder/%ED%8C%8C%EC%9D%B4%EC%8D%AC-iterable%EA%B3%BC-iterator-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EA%B0%80-%EB%AD%90%EC%98%88%EC%9A%94)

## 읽을 예정

- 읽을 예정인 글의 링크를 붙여 넣으세요.
