# 🚀 학습 키워드

- 원하는 행/렬 추출하기
- Pandas는 DataFrame의 로우나 칼럼을 지정하여 데이터를 선택할 수 있는 인덱싱 방식으로 `iloc[]` 와 `loc`를 제공한다.

## 정의
- `df.loc`: `df.loc[행 인덱싱 값, 열 인덱싱 값`
	- Access a group of rows and columns by label(s) or a boolean array.
	- 명칭(label)기반으로 데이터를 추출
	- loc : location

- `df.lioc`: `df.lioc[]`
	- Purely integer-location based indexing for selection by position.
	- 위치(location)기반으로 데이터 추출
	- iloc : integer location

## 키워드 
`loc vs. iloc: df.loc[]은 명칭(label) 기반으로 데이터를 추출하며, 슬라이싱, 팬시 인덱싱, 불리언 인덱싱을 지원하고, df.iloc[]은 정수 기반 위치 인덱싱으로 데이터를 추출하며, 슬라이싱과 팬시 인덱싱은 지원하지만 불리언 인덱싱은 제공하지 않는다.`

---

# 📝새로 배운 개념

## `df.loc[]`
- 데이터 프레임 행/열을 라벨을 통해 가져오는 방법
- 슬라이싱과 팬시인덱싱, 불리언 인덱싱을 제공
	- 슬라이싱 : 레이블을 사용해 데이터 특정 범위 선택
	- 팬시 인덱싱 : 리스트나 ndarray(배열)로 인덱스 집합을 지정해 데이터 선택
	- 불리언 인덱싱 : 조건식을 `[] 안에` 기입하여(조건에 맞는) 그에 해당하는 데이터 선택

|              `loc[]` 연산 유형               | 설명 및 반환 값                                                                   |
| :--------------------------------------: | --------------------------------------------------------------------------- |
|        `df.loc['three', 'Name']`         | 인덱스 값 three인 행의 Name 칼럼의 단일 값 반환                                            |
|   `df.loc['one':'two', 'Name','Year']`   | 인덱스 값 one부터 two까지 행의 Name과 Year칼럼에 해당하는 DataFrame반환                         |
| `df.loc['one',:'three','Name':'Gender']` | 인덱스 값 one 부터 three까지 행의 Name부터 Gender 칼럼까지의 DataFrame반환                     |
|               `df.loc[:]`                | 모든 데이터 값                                                                    |
|        `df.loc[df.Year >= 2014]`         | `iloc[]` 와 다르게 `loc[]` 는 불린 인덱싱이 가능, Year칼럼의 값이 2014이상인 모든 데이터를 불린 인덱싱으로 추출 |


## `df.iloc[]`
- 데이터 프레임 행/열의 순서를 나타내는 정수를 통해 가져오는 방법
- 정수 기반 위치 기반 인덱싱만 허용(interger-location)
- 행과 열 정수 인덱스 위치/ 0을 출발점으로 하는 세로축, 가로축 좌표 정숫값으로 지정하는 방식
- 슬라이싱과 팬시 인덱싱을 제공하나 명확한 위치 기반 인덱싱이 사용되어야하는 제약으로 인해 **불린 인덱싱은 제공하지 않는다.**

|    `iloc[]` 연산 유형    | 설명 및 반환 값                                                                |
| :------------------: | ------------------------------------------------------------------------ |
|    `df.iloc[1,0]`    | 두번째 행의 첫번째 열 위치에 있는 단일 값반환                                               |
|    `df.iloc[2,1]`    | 세번째 행의 두번째 열 위치에 있는 단일 값 반환                                              |
| `df.iloc[0:2,[0,1]]` | 0:2 슬라이싱 범위의 첫번째에서 두번째 행과 첫번째, 두번째 열에 해당하는 DataFrame 반환                  |
| `df.iloc[0:2, 0:3]`  | 0:2 슬라이싱 범위의 첫번째에서 두번째 행의 0:3 슬라이싱 범위의 첫번째부터 세번째 열 범위에 해당하는 DataFrame 반환 |
|     `df.iloc[:]`     | 전체 DataFrame 반환                                                          |
|    `df.iloc[:,:]`    | 전체 DataFrame 반환                                                          |



---

# ✨
- loc와 iloc REMIND

---
# 🔗레퍼런스

## 참고 강의/글
- [# [pandas] 원하는 행/렬 추출하기 (loc, iloc)](https://velog.io/@cualquier/pandas-loc-iloc)
