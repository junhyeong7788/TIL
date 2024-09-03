# 🚀 학습 키워드

## 정의
- 예외를 발생시키는 예외처리랑 비슷하지만, 예외처리는 에러가 발생했을때 어떤 처리를 하기 위한 코드이고, 이 assert(가정 설정문)은 **어떤 조건이 True임을 보증하기 위해서 사용**하는 것
- `assert [조건], [오류메시지]`

## 키워드 
- 조건이 참일때 코드는 내가 보장, 하지만 조건이 거짓일때는 내가 보증하지 않는 동작이다.
	- Assertion Error 발생!

---

# 📝새로 배운 개념

## 개념 
- 치명적인 오류를 막기 위해 사용
- assert 구문이 들어가는 코드부분에서 어떤 조건이 참임을 확고히 하는 것
	- 그 조건이 거짓이면 에러 상황으로 실행을 계속하지 못하게 하는 것

## 예제 (두수의 차)

```python
def solution(num1, num2):
    def validate_input(x, lower, upper): # 제한조건
        if x >= lower and x <= upper:
            return True
        return False
    num_list = [num1, num2]
    assert all([validate_input(x, -50000, 50000) for x in num_list])
    answer = num1 - num2
    return answer
```

- `all()` 내장함수 : 모든 값이 참인지를 확인할 수 있는 함수
	- 반복문으로 순회할 수 있는 (iterable) 모든 객체를 인자로 받을 수 있음.
	- 인자로 넘어온 자료구조 내의 모든 요소가 참일 때만 `True`를 반환 (거짓인 요소가 하나라도 있으면 `False` 반환)
- `for x in num_list` : num_list에 있는 각 요소를 차례대로 x에 할당하면서 반복문 실행, `validate_input(x, -50000, 50000)` 이 호출되며, 각 x값이 함수의 매개변수로 전달되어 검증이 이루어짐
 ---
# ✨
- assert구문, all(), 리스트 컴프리헨션
- 함수안에 함수를 정의하여 assert구문을 통해 조건의 참과 거짓을 판단할 수 있는 방법을 배웠다.

---

# 🔗레퍼런스

## 참고 강의/글

- [[python]파이썬 assert(가정 설정문)에 대해서](https://blockdmask.tistory.com/553)
- [파이썬의 내장함수all() 사용법](https://www.daleseo.com/python-all/)
