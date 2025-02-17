# 🚀 학습 키워드

## 정의
- Pandas 파이썬 라이브러리 : 데이터 분석 라이브러리
- Pandas를 사용하면 행과 열로 이루어진 데이터 객체를 만들어 다룰 수 있게 되며 보다 안정적으로 대용량의 데이터들을 처리하는데 매우 편리한 라이브러리이다.
## 키워드 
- `데이터 조작 및 분석을 위한 강력하고 유연한 파이썬 라이브러리`

---

# 📝새로 배운 개념

## 개념 : Pandas 자료구조 
- 기본적으로 정의되는 자료구조인 Series와 DataFrame을 사용
- `Series`: 일차원 배열과 유사한 자료구조, 데이터 값과 각각의 값에 대응하는 인덱스로 구성된 레이블이 붙은 배열
- `DataFrame` : 2차원 테이블 형태의 자료구조로, 행과 열로 구성된 데이터 집합
	- 각각의 열이 *Series*로 구성, 각 열은 서로 다른 데이터 타입을 가질 수 있다.
	- `Index` : RDBMS의 PK처럼 개별 데이터를 고유하게 식별하는 Key값


## 개념
- `type(df), df.shape, df.info(), df.describe()`
- `df['column].value_counts()
- DataFrame과 리스트, 딕셔너리, 넘파이 ndarray 상호변환 가능
	- `df.values`: DataFrame -> ndarray
	- `df.values.tolist()` : DataFrame -> list
	- `df.to_dict('list') : DataFrame의 각 열을 키(key)로 하고, 해당 열의 값들을 리스트(list)로 변환하여 사전형태로 반환`
- DataFrame 데이터 삭제 
	- `DataFrame.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')
- index 객체 : 데이터프레임의 Series의 레코드를 고유하게 식별하는 객체
	- Series에서 index 객체만 추출하려면 DataFrame.index 또는 Series.index속성을 통해 가능
-  `[ ] 연산자 = 컬럼지정 연산자`  : DataFrame 또는 Series 객체에 대해 특정 데이터를 선택하거나 필터링하는 데 사용되는 기본적인 연산자
- DataFrame `iloc[ ]` 연산자 : 정수기반 위치 인덱싱을 통한 인덱싱 메서드
- DataFrame `loc[ ]`연산자 : 명칭(레이블)기반 인덱싱을  통한 인덱싱 메서드
 - 정렬 : `sort_values()`
 - Aggregation 함수 : `min(), max(), sum(), count() 등`
 - `groupby()` : by인자로 groupby 하려는 칼럼을 입력하면 대상 컬럼으로 groupby된 DataFrame groupby객체를 반환
 - 결손데이터 처리
 - apply lambda (python lambda 식)
---

# ✨
- Pandas라이브러리는 데이터 조작과 분석에 필수적인 도구
- 다양한 자료구조와 인덱싱 방법 제공, 대용량 데이터 처리와 분석을 간결하고 효율적으로 수행가능

---
# 🔗레퍼런스

## 참고 강의/글

- [# [Python]Pandas(판다스)란?](https://velog.io/@hsjung2015/PythonPandas%ED%8C%90%EB%8B%A4%EC%8A%A4%EB%9E%80)
