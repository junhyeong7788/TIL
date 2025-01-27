# 🚀 학습 키워드

## 키워드

- `SSH는 보안되지 않는 네트워크에서도 네트워크 서비스를 안전하게 운영하기 위한 암호화 기반 네트워크 프로토콜을 말한다`

---

# 📝새로 배운 개념

## Github, Gitlab

- Git을 사용할 경우 필수라고 할 수 있는 온라인 저장소 서비스들이 모두 SSH를 기본으로 지원

## MacOS : SSH Key 생성 및 사용

1. SSH 확인
   - `ls -al ~/.ssh` -> 해당 디렉토리에 아무것도 없으면 SSH Key가 없는 것
2. SSH Key 생성
   - `ssh-keygen` -> 맥OS는 유닉스 계열 운영체제로 OpenSSH를 기본으로 포함하고 있기 때문에 위와 같이 간단하게 생성할 수 있다.
   - 이후 `Enter file in which to save the key (/Users/.../.ssh/id_rsa):` 이와 같이 키 쌍을 저장할 파일 이름을 입력하라고 나온다.
   - 보통의 경우 엔터키를 눌러서 디폴트 값인 is_rsa를 사용, 비밀번호를 입력하지 않고 넘어간다.
3. SSH Key 확인
   - `$ cat ~/.ssh/id_ras.pub` 파일 내 키 존재

## Public Key 등록

- `id_rsa` 는 ssh 버전 2 RSA 사용자 인증 정보 (authentication identity of the user)를 담고 있다. `유지 외의 다른 사람은 읽으면 안된다.`
- `id_rsa.pub` 는 ssh 버전 2 RSA 퍼블릭 키 인증 정보를 담고 있다. `~/.ssh/authroized_keys` 이 퍼블릭 키를 이용해 로그인하려는 모든 곳의 `.ssh`에 추가되어야한다.

---

# 🔗레퍼런스

## 참고 강의/글

- [macOS: 맥에서 SSH 키 생성하고 사용하기](https://mark340.tistory.com/59)
- [블로그](https://xho95.github.io/macos/security/openssh/ssh/gitlab/2017/02/22/Using-SSH-on-Mac.html)
- [ssh: rsa 방식 key로 접속하기](https://potato-y.github.io/linux/ssh-rsa-key/)
