# 🚀 Cursor Rules

### 🎯 주요 키워드

프로젝트의 특정 파일이나 폴더에 맞춘 Ai 행동을 정의하는 방식

---

## 🏷 Cursor Global Rules

- 위치 : Cursor Setting > General > Rules for AI
- 예시 :
  - 모든 프로젝트 Ai 응답을 한국어로 설정
  - 코드 응답을 길게 또는 짧게 요약하도록 설정

## 🏷 Cursor Project Rules (= `.cursorrules`)

- 위치 : `.cursor/rules/` 디렉토리에 저장
- 장점 : 세밀한 파일 패턴 적용 가능, Ai 자동 컨텍스트 추가 가능, 버전 관리 가능

  - 이전 : `.cursorrules` 파일 하나만 사용
  - 정책 변경으로 여러 파일로 분리 가능

- 예시 : 해당 프로젝트 루트 디렉토리에 `.cursor/rules/` 디렉토리 생성
  ```
  .cursor/rules/
  ├── project_rules.mdc
  ├── project_rules_v2.mdc
  └── project_rules_v3.mdc
  ```
- 해당 파일 내 내용
  - 아래 레퍼런스 깃허브 링크 참고
  - 미리 작성되어있는 Rules 파일을 가져다 사용 가능
  - 또는 직접 작성 가능

---

# 🔗 레퍼런스

## 참고 강의/글

- [Github - Awesome CursorRules](https://github.com/PatrickJS/awesome-cursorrules)

- [CURSOR 잘 사용하기(0.46 버전 기준)-25.03.03 (.cursorrules / .cursorindexingignore, .cursorignore)](https://data-newbie.tistory.com/1019)
