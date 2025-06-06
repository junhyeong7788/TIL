# 🚀 학습 키워드

## 정의

Built-in Function : 파이썬 인터프리터에 기본적으로 포함된 함수

- 어떤 객체에도 종속되지 않고 독립적으로 사용됨

---

# 📝새로 배운 개념

## 특징

- 파이썬이 기본적으로 제공하는 함수, 별도의 import 없이 사용 가능
- 특정 데이터 타입이나 객체에 종속되지 않고 범용적으로 사용됨
- `print()`, `len()`, `sum()` 처럼 전역 네임스페이스에 존재하는 함수

## 예제

```python
# len(): 리스트, 문자열 등 다양한 자료형에서 사용 가능
print(len([1, 2, 3, 4]))  # 4
print(len("Python"))      # 6

# sum(): 숫자 리스트의 합을 계산
print(sum([10, 20, 30]))  # 60

# max(), min(): 최댓값과 최솟값 찾기
print(max([3, 7, 2, 5]))  # 7
print(min([3, 7, 2, 5]))  # 2
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

# ✨ 대표적인 내장 함수 목록

- 출력 및 형 변환 관련: print(), input(), str(), int(), float(), bool()
- 수학 연산 관련: abs(), pow(), round(), divmod(), sum(), max(), min()
- 자료형 및 컬렉션 관련: len(), type(), sorted(), range(), enumerate(), zip()
- 파일 및 입출력 관련: open(), repr(), format()
- 논리 및 조건 관련: all(), any(), isinstance()
- 객체 관련: id(), dir(), vars()
