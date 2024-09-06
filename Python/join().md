# 🚀 학습 키워드

## 정의
- `.join()`: 파이썬에서 리스트를 문자열로 일정하게 합쳐주는 join함수
	- 문자열을 다룰 때 유용하게 사용 할 수 있는 함수

## 키워드
- `.join() 함수는 리스트의 문자열 요소를 구분자와 함께 결합해 하나의 문자열로 변환하는 데 유용`

---

# 📝새로 배운 개념

## REMIND
- `in` : in 연산자의 결과는 bool타입, 확인하고자 하는 데이터가 있는 경우 True, 없는 경우 False를 반환
- `not in` : not in 연산자는 확인하고자 하는 데이터가 있으면 False, 없으면 True를 반환
## 개념 
- `''.join(리스트)`
	- 매개변수로 들어온 `['a','b','c']` 이런 식의 리스트를 'abc'의 문자열로 합쳐서 반환해주는 함수
- `'구분자'.join(리스트)` 
	- 리스트의 값과 값 사이에 '구분자'에 들어온 구분자를 넣어서 하나의 열로 합쳐준다.
	- ex `'_'.join(['a','b','c'])라 하면 "a_b_c"와 같은 형태로 반환

## 예시
```python
def solution(my_string):
    word = ("a", "e", "i", "o", "u")
    return ''.join([i for i in my_string if i not in word])
```

- `i for i in my_sting`: my_string의 각 문자를 i로 하나씩 순회
- `if i not in word`: 현재 순회 중인 문자 i가 word(모음 리스트)안에 포함 되어 있지 않은 경우에만 그 문자를 결과 리스트에 추가
- `''.join()` : 리스트 안의 문자열 요소들을 하나의 문자열로 합쳐주는 매서드 (여기서는 빈 문자열 사용)

---

# ✨
- `.join` 함수 리마인드
- ` in, not in` 연산자 리마인드

---
# 🔗레퍼런스

## 참고 강의/글

- [[python] 파이썬 join 함수 정리 및 예제 (문자열 합치기)](https://blockdmask.tistory.com/468)
- [# [Python] 파이썬 join 함수 정리(join)](https://velog.io/@roope97/Python-%ED%8C%8C%EC%9D%B4%EC%8D%AC-join-%ED%95%A8%EC%88%98-%EC%A0%95%EB%A6%ACjoin)
