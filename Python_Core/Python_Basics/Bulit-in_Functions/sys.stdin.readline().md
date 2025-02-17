# 🚀 학습 키워드

## 정의
- 반복문으로 여러줄을 입력 받아야할 때는 `input()` 으로 입력 받는다면 시간초과가 발생할 수 있다.(= `input()` 메소드는 매우 느리다.)
	- 여러줄 입력받는 상황에서는 반드시 `sys.stdin.readline()` 을 사용해야 시간초과가 발생하지 않는다.
	- 코랩이나 주피터노트북에서 `sys.stdin.readline()`가 동작하지 않는다.
	- 백준
- `sys.stdin.readline()` 은 매 줄의 끝에 있는 개행 문자를 포함하여 반환해준다는 것
 
## 키워드 

```python
# 사용 예시 , 임의의 개수의 정수를 n줄 입력받아 리스트 저장
import sys
input = sys.stdin.readline

n = int(input()) # 받을 문자의 개수
data = []

for _ in range(n):
	line = input().strip() #  한 줄을 입력받아 줄 바꿈 문자 제거
	data.append(line)

print(data)
```


---

# 📝새로 배운 개념

## 개념 : input() 내장 함수
- parameter로 prompt message를 받을 수 있다.
- 입력 받은 값의 개행 문자를 삭제시킨 뒤 리턴한다.
- 즉, 입력받은 문자열에 rstrip()함수를 적용시켜서 리턴하기 때문에 다소 느리다.

## 개념 : sys.stdin.readline()
- prompt message를 인수로 받지 않는다.
- sys.stdin.readline()은 개행 문자를 포함한 값을 리턴한다.
- 또한 *입력 크기에 제한*을 줌으로써 한번에 읽어들일 문자의 수를 정할 수 있다.

### 개행 문자 제거 방법
1. type을 int(정수형)로 바꿔서 개행  문자를 받지 못하도록 하기
2. 개행 문자를 제거해주는 함수 사용

```
- rstrip() : 오른쪽 공백을 삭제
- lstrip() : 왼쪽 공백을 삭제
- strip() : 왼쪽, 오른쪽 공백을 삭제
```

### 해당 함수 정의 요약
- 파이썬 표준 입출력 시스템과 관련된 내부 동작을 설명
- 특히 표준 스트림이 어떻게 설정되고, 초기화된 후에 변경될 수 있는지, 그리고 이러한 변경이 발생했을 때 원래 상태를 어떻게 유지하는지에 대해 다룬다.
- 이는 고급파이썬 프로그래밍에서 중요한 개념으로, 특히 표준 스트림을 재정의하거나 조작해야 하는 상황에서 유용하다.

---
# 🔗레퍼런스

## 참고 강의/글

- [input()과 sys.stdin.readline()의 차이](https://djm03178.tistory.com/21)
- [input() vs sys.stdin.readline()](https://bentist.tistory.com/99)
