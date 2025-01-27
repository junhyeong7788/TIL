# 🚀 학습 키워드

## 정의

- SSH(Secure Shell) : 네트워크 프로토콜 중 하나로, 암호화된 통신 세션을 통해 네트워크 서비스를 안전하게 제공하는 프로토콜이다.
  - 원격지 호스트 컴퓨터에 접속하기 위해 사용되는 인터넷 프로토콜 중 하나
  - 컴퓨터가 공공 네트워크를 통해 로그인하거나 원격시스템에서 명령을 실행하고 다른 시스템으로 파일을 복사할 수 있도록 해주는 응용 프로그램, 프로토콜을 말한다.

## 키워드

- `원격 시스템 접속 및 명령 실행, 파일 전송 시 보안을 제공`

---

# 📝새로 배운 개념

## 통신 방법, Key

- SSH Key는 공개키(Public Key)와 비공개키(Private Key)로 구성

  - 공개키는 원격지, 비공개키는 로컬에 위치
  - SSH 접속을 시도하면 로컬의 비공개키와 원격 서버의 비공개키를 비교해서 일치하는지 인증과정을 거치고 접속을 할 수 있게 해준다.

  - Public Key : 공개되어도 안전한 키, 복호화 불가
  - Private Key : 외부 노출되면 안되는 키, 로컬 컴퓨터 내부에 저장, 암호화 정보 복호화
  - 포트 번호 : 기본적으로 22번 포트 사용

## SSH 명령어와 예제

### SSH 서버 원격 접속

- `ssh user@hostname` : SSH를 통해 서버에 원격 접속
  - user : 서버의 사용자 계정 이름
  - hostname : 접속할 서버의 도메인 이름 또는 IP 주소

### SSH 공개키 인증 설정

1. 클라이언트에서 공개키 생성
   - `ssh-keygen -t rsa -b 4096`
     - -t : 키 타입
     - -b : 키 길이
     - 생성된 공개키(`~/.ssh/id_rsa.pub`)를 서버에 등록
2. 서버에 공개키 추가
   - `ssh-copy-id user@hostname` : 서버의 `~/.ssh/authorized_keys`파일에 공개키 추가
   - 이후 비밀번호 없이 접속 가능
3. scp (Secure Copy) : SSH를 통해 파일을 복사
   - `scp [옵션] source_file user@hostname:/path/to/destination`
     - source_file : 로컬에 있는 복사할 파일 경로
     - destination : 서버의 저장 경로
4. SFTP (Secure File Transfer Protocol) : SSH 기반 파일 전송 프로토콜
   - `sftp user@hostname`
     - 대화형 파일 관리 기능
5. SSH 포트 포워딩
   - `ssh -L [local_port]:[remote_host]:[remote_port] user@hostname`
     - -L : 로컬 포트 포워딩
     - SSH 터널링을 통해 특정 포트를 로컬과 원격 서버 간 연결

---

# ✨

- **네트워크 보안 -> 암호화 통신 프로토콜 -> SSH**
- 네트워크 보안
  - 네트워크 상에서 데이터의 안전성과 무결성을 보장하는 기술과 방법론
- 암호화 통신 프로토콜 (SSH 포함 위치)
  - 네트워크 보안의 하위 개념, 데이터를 안전하게 송수신하기 위해 암호화 방식을 사용하는 프로토콜

---

# 🔗레퍼런스

## 참고 강의/글

- [SSH 기초 개념정리](https://developsd.tistory.com/114)

## 읽을 예정

- 암호화 통신 프로토콜의 종류 : SSH, TLS/SSL, IPSec, HTTPS, SFTP, FTPS, Kerberos, VPN, SMTPS, DoH, DoT 등이 존재
