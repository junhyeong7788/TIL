# 🚀 MacOS 키맵핑하는 방법 (hidutil)

## 정의

- `hidutil`
  - macOS에 내장된 **명령줄 유틸리티 (command-line tool)** 로, 키보드 입력을 재매핑하는 기능을 제공
  - 라이브러리가 아닌 실행 가능한 시스템

## 사용이유

- 기본 한영변환하는 방법인 tab키 전환 시 딜레이 발생
- **Karabiner-Elements**(프로그램)를 사용하여 키보드 맵핑 시 한영키 변환 딜레이 발생
  - -> **OS 자체에서 키보드 맵핑**을 하면 속도가 빠르고, **프로그램을 사용하지 않아도 되는 장점**이 있음

## 사용법

1. `hidutil key remapping generator for Mac OS` 사이트를 이용하여 키보드 맵핑 코드를 생성 (맨 아래 1번 링크 참조)
2. terminal을 열고 `cd ~/Library/LaunchAgents`로 이동
3. `com.local.KeyRemapping.plist` 파일을 생성

4. 1번에서 생성한 코드를 파일에 저장 (재부팅 시 자동으로 실행되도록 설정하는 과정)
5. 맥북 재부팅
6. "시스템 설정" -> "키보드" -> "키보드 단축키" -> "입력 소스"로 이동하여 "이전 입력소스 선택" 부분을 더블클릭한 후 맥북 키보드의 오른쪽 `command`키를 누르면 `F18`키로 변환
7. 이제 오른쪽 `command`키로 한/영 자판 변환이 된다. (오류 시 재부팅 후 확인)

- _(더 자세한 설명은 2번 링크 참조)_

## 😁 작성자가 사용하는 방법 ✍️

- **right_command -> F18 / right_option -> F18로 맵핑**
  - **맥북**으로 사용할때는 Right command를 F18키로 사용
  - **외장키보드(75배열)** 사용할때는 Right option을 F18키로 사용

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>com.local.KeyRemapping</string>
    <key>ProgramArguments</key>
    <array>
        <string>/usr/bin/hidutil</string>
        <string>property</string>
        <string>--set</string>
        <string>{"UserKeyMapping":[
            {
              "HIDKeyboardModifierMappingSrc": 0x7000000E7,
              "HIDKeyboardModifierMappingDst": 0x70000006D
            },
            {
              "HIDKeyboardModifierMappingSrc": 0x7000000E6,
              "HIDKeyboardModifierMappingDst": 0x70000006D
            }
        ]}</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
</dict>
</plist>
```

---

# 🔗레퍼런스

## 참고 강의/글

1. [hidutil key remapping generator for MacOS 사이트](https://hidutil-generator.netlify.app/)
2. [Karabiner 설치없이 오른쪽 CMD키로 한/영 변환하기](https://my.bestie.co.kr/cmd%ED%82%A4-%ED%95%9C%EC%98%81-%EB%B3%80%ED%99%98/)
