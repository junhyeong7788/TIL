# 🚀 학습 키워드

## 정의

`from pprint import pprint`:
- 목적 : pprint 모듈은 "pretty-print"를 의미하며, 파이썬 데이터 구조를 더 읽기 쉽게 출력하는 방법을 제공
	- 특히 중첩되거나 복잡한 데이터 구조(예 : 딕셔너리 및 리스트)에 유용
- 주요 용도
	- 읽기 쉬운 출력 : 데이터를 더 쉽게 이해할 수 있도록 표시해야 할 때 사용
	- 디버깅 : 디버깅 중에 복잡한 중첩데이터구조를 검사하는 과정을 단순화한다.


## 키워드 

```python
from pprint import pprint

# pprint 사용 예제
data = {
    'name': 'Alice',
    'age': 30,
    'children': [
        {'name': 'Bob', 'age': 8},
        {'name': 'Charlie', 'age': 5}
    ],
    'pets': ['dog', 'cat']
}

# pprint로 데이터 출력하여 가독성 향상
pprint(data)
```

---

# 📝새로 배운 개념

## 개념 

위 예제 코드의 실행 결과는 아래와 같이 나온다.  
```
{'age': 30, 
 'children': [{'age': 8, 'name': 'Bob'}, {'age': 5, 'name': 'Charlie'}], 
 'name': 'Alice', 
 'pets': ['dog', 'cat']}
```

print를 한 결과는 아래와 같이 나온다.
```
{'name': 'Alice', 'age': 30, 'children': [{'name': 'Bob', 'age': 8}, {'name': 'Charlie', 'age': 5}], 'pets': ['dog', 'cat']}
```

---

# ✨느낀 점

- **pprint**: 복잡한 데이터 구조를 더 읽기 쉽게 출력하여 그 내용을 **한눈에** 이해하기 쉽게 한다.

---

# 🔗레퍼런스

## 참고 강의/글

- ChatGPT4o 