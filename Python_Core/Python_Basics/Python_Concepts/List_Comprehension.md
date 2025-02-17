# 🚀 학습 키워드

## 정의
- 리스트 컴프리헨션 : 직관적으로 리스트를 생성하는 방법
	- 대괄호 `"[","]"`로 감싸고 내부에 for문과 if문을 사용하여 반복하며 조건에 만족하는 것만 자유롭게 리스트로 생성할 수 있다.
- 리스트 컴프리헨션을 사용하면 직관적이고 여러줄 쓸걸 한줄에 만들어준다. 
## 키워드 
- `“간결하고 효율적으로 리스트를 생성하는 파이썬 문법.”`

---

# 📝새로 배운 개념

## 개념 
- 리스트 컴프리헨션의 기본 구조 : `[expression for item in iterable if condition]` 
	- expression : 생성될 리스트의 요소를  결정하는 표현식
	- for item in iterable : 리스트, 문자열, 튜플, range 등 반복가능한 객체 / iterable의 각 요소를 순회하며 item으로 사용
	- if condition : (선택사항) 이 조건이 참일 경우에만 expression이 리스트에 포함
### 기초
```python
li = [] # [1,2,3,4,5]
for i in range(5):
	li.append(i)
```

```python
[i for i in range(5)] # [1,2,3,4,5]
```
### 조건문 사용
```python
[i for i in range(5) if i%2==0]
```

```python
[i for i in range(5) if i%2==0 if i%4==0]
```

```python
[i if i%2==0 else 'odd' for i in range(5)] # 왼쪽 if문 사용할때, 반드시 else와 같이 사용
```

## 예시

```python
# 짝수의 합
# 정수 `n`이 주어질 때, `n`이하의 짝수를 모두 더한 값을 return 하도록 solution 함수를 작성
def solution(n):
    answer = 0
    for i in range(n+1):
        if i%2 == 0:
            answer += i
    return answer
```

```python
def solution(n):
	return sum([i for i in range(n+1) if i%2==0]) # 리스트 컴프리헨션
```

```python
def solution(n):
return sum([i for i in range(2, n + 1, 2)]) 
# 2부터 n까지의 짝수를 생성, 그 짝수들을 i에 저장하여 [i for i in range(2, n+1, 2)]로 리스트를 생성
```

---

# ✨
장점
- 코드가 간결하고 명확해진다.
- 일반적으로 for 루프보다 빠르게 동작한다.
단점
- 복잡한 경우, 가독성이 떨어짐
- 너무 복잡한 표현식은 피하는 것이 좋다.

---
# 🔗레퍼런스

## 참고 강의/글

- [## [[Python의 꽃] 리스트 컴프리헨션(List Comprehension)](https://bio-info.tistory.com/28)](https://bio-info.tistory.com/28)
