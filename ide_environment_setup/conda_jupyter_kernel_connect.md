# 🚀 학습 키워드

## 문제

- 아나콘다 가상환경 생성 후 vscode 주피터노트북 Select Kernel에 가상환경이 뜨지 않는 문제

## 키워드

- 가상환경은 개발을 수행함에 있어서 각 프로젝트 별로 요구하는 패키지가 다를 때 유용하게 사용한다.
- 특정 가상환경에 맞는 Jupyter Notebook을 실행하기 위해서는 가상환경에 주피터노트북을 설치해줘야한다.

---

# 📝새로 배운 개념

## 개념

- 주피터노트북 설치 : `pip install jupyter notebook`
- 연결할 가상환경 이름과 주피터노트북에 표시할 이름 적용
  - `python -m ipykernel install --user --name 가상환경이름 --display-name "표시할 커널이름`
- 이후 커널 재시작을 해주면 vscode kernel select 목록에 새롭게 생성된 가상환경이 뜬다.

---

# 🔗레퍼런스

## 참고 강의/글

- [[Python] 아나콘다 가상환경 구성 및 주피터 노트북 커널 연결](https://taehooh.tistory.com/48)
