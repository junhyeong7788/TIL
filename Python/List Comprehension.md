# 🚀 학습 키워드

## 정의
- 리스트 컴프리헨션 : 직관적으로 리스트를 생성하는 방법
	- 대괄호 `"[","]"`로 감싸고 내부에 for문과 if문을 사용하여 반복하며 조건에 만족하는 것만 자유롭게 리스트로 생성할 수 있다.

## 키워드 
- 리스트 컴프리헨션을 사용하면 직관적이고 여러줄 쓸걸 한줄에 만들어준다. 심지어 속도도 빠름

---

# 📝새로 배운 개념

## 개념 

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
- 리스트컴프리헨션 개념 정리

---
# 🔗레퍼런스

## 참고 강의/글

- [## [[Python의 꽃] 리스트 컴프리헨션(List Comprehension)](https://bio-info.tistory.com/28)](https://bio-info.tistory.com/28)
