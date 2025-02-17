# 🚀 학습 키워드

## 정의

Method : 특정(Object)에 속한 함수로, 객체를 통해 호출해야만 사용할 수 있다.

---

# 📝새로 배운 개념

## 특징

- 특정 데이터 타입 (객체)에 속한 함수
- 객체.메소드() 형태로 사용
- str, list, dict 등의 내장 자료형에도 다양한 메소드가 제공됨

## 예제

```python
# 문자열 메소드
text = "hello world"
print(text.upper())   # "HELLO WORLD"
print(text.replace("world", "Python"))  # "hello Python"

# 리스트 메소드
numbers = [1, 2, 3, 4]
numbers.append(5)  # 리스트 끝에 5 추가
print(numbers)  # [1, 2, 3, 4, 5]

numbers.sort()  # 리스트 정렬
print(numbers)  # [1, 2, 3, 4, 5]

# 딕셔너리 메소드
student = {"name": "Alice", "age": 25}
print(student.keys())   # dict_keys(['name', 'age'])
print(student.values()) # dict_values(['Alice', 25])
```

## 내장 함수와 메소드의 차이점

|       구분       |                 내장 함수                  |                메소드                |
| :--------------: | :----------------------------------------: | :----------------------------------: |
|       정의       | 파이썬 인터프리터에 기본적으로 포함된 함수 |  특정 객체에 종속되어 사용되는 함수  |
|       사용       |        함수명(인자)형태로 직접 호출        |    객체.메소드명(인자)형태로 호출    |
|      독립성      |         특정 객체에 종속되지 않음          |    특정 객체(자료형)에 속해 있음     |
|    호출 예시     |               len([1, 2, 3])               |         [1, 2, 3].append(4)          |
| 예제 함수/메소드 |           print(), len(), sum()            | "Hello".upper(), [1, 2, 3].append(4) |

```python
# 내장 함수 사용
my_list = [1, 2, 3, 4]
print(len(my_list))  # 4  (내장 함수 사용)

# 메소드 사용
my_list.append(5)  # 리스트의 append() 메소드 호출
print(my_list)  # [1, 2, 3, 4, 5]
```

---

# ✨ 자료형별 대표적인 메소드

- 문자열(str) 관련 메소드: upper(), lower(), replace(), split(), join()
- 리스트(list) 관련 메소드: append(), extend(), pop(), sort(), reverse()
- 딕셔너리(dict) 관련 메소드: keys(), values(), items(), get(), update()
- 집합(set) 관련 메소드: add(), remove(), union(), intersection(), difference()
