# 🚀 학습 키워드

## 정의
- 람다 형식 
	- 이름이 없는 함수로 일반적으로 함수를 한 번만 사용하거나 함수를 인자로 전달해야 하는 경우에 매우 유용하게 사용된다.
	- 인공지능 분야나 AutoCAD라는 설계프로그램에서 쓰이는 Lisp언어에서 물려받음
- `lambda 매개변수 : 표현식`

## 키워드 
- 함수를 딱 한 줄만으로 만들게 해주는 함수 , 익명함수(anonymous function)라고도 불린다.

---

# 📝새로 배운 개념

## 두 수의 차
```python
def solution(num1, num2):
        answer = num1 - num2
        return answer
```
- `solution = lambda num1, num2 : num1 - num2` 해당 식으로 표현 할 수 있다.

람다 함수의 특징
- 간결성 : 단순한 표현식
- 익명성 : 함수에는 이름이 없으며, 필요한 곳에 즉시 정의하고 사용할 수 있다.
- 제한된 기능 : 단순한 표현식만을 포함할 수 있으며, **복잡한 논리나 여러 줄에 걸친 코드를 작성하는데**는 적합하지 않다.

## 예제
- map() - `map(함수, 리스트)`
```python
map(lambda x: x ** 2, range(5)) # [0, 1, 4, 9, 16]
list(map(lambda x : X ** 2, range(5))) # [0, 1, 4, 9, 16]
```

- reduce() - `reduce(함수, 시퀀스)` : 시퀀스(문자열, 리스트, 튜플)의 원소들을 누적적으로 함수에 적용시킴
```python
from functools import reduce
reduce(lambda x, y: x + y, [0, 1, 2, 3, 4]) # 10

reduce(lambda x, y: y + x, 'abcde') # 'edcba' 
```

- filter() - `filter(함수, 리스트)` 
```python
# 0부터 9까지의 리스트중 5보다 작은 것만 돌려주는 예제
filter(lambda x: x < 5, range(10)) # [0, 1, 2, 3, 4]
list(filter(lambda x: x < 5, range(10))) # [0, 1, 2, 3, 4]
```

---

# ✨느낀 점
- programmers에서 두수의 차 문제를 풀이 후 다른 사람의 풀이를 보다가 보게 되었다.
- 함수형 프로그래밍에서 중요한 개념 중 하나이다.

---

# 🔗레퍼런스

## 참고 강의/글

- [3.5 람다](https://wikidocs.net/64)
- 자세한 내용 : [32.1 람다 표현식으로 함수 만들기](https://dojang.io/mod/page/view.php?id=2359)
