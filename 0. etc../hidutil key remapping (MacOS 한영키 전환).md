# 🚀 맥북의 특정 키보드를 Function키로 맵핑하는 방법

- `hidutil`을 사용하여 맥북의 특정 키보드를 Function키로 맵핑할 수 있다.
- `hidutil`은 macOS에서 HID(인간-컴퓨터 인터페이스) 장치를 제어하기 위한 유틸리티이다.
- `hidutil key remapping generator for Mac OS를 사용

## right_command -> F18 / right_option -> F18로 맵핑하는 코드

- **맥북** 으로 사용할때는 Right command를 F18키로 사용
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

## 이후 과정

1. `cd ~/Library/LaunchAgents`로 이동
2. vi편집기로 `com.local.KeyRemapping.plist` 파일을 생성
3. 위의 코드를 복사하여 붙여넣고 파일 저장 (재부팅 시 자동으로 실행되도록 설정하는 과정)
4. 맥북 재부팅
5. "시스템 설정" -> "키보드" -> "키보드 단축키" -> "입력 소스"로 이동하여 "이전 입력소스 선택" 부분을 더블클릭한 후 맥북 키보드의 오른쪽 `command`키를 누르면 `F18`키로 변환된다.
6. 이제 오른쪽 `command`키로 한/영 자판 변환이 된다. (오류 시 재부팅 후 확인)

---

# ✨

- 지금까지 Karabiner-Elements를 사용하여 키보드 맵핑하고 한영키 변환했다.
- Karabiner-Elements를 사용하는 동안 한영키 변환 속도가 느려서 빠른 타자시 오타확률이 높았다.
- 프로그램을 사용하지 않고 OS 자체에서 키보드 맵핑하는 것이 장점이다.

---

# 🔗레퍼런스

## 참고 강의/글

- [hidutil key remapping generator for MacOS 사이트](https://hidutil-generator.netlify.app/)
- [Karabiner 설치없이 오른쪽 CMD키로 한/영 변환하기](https://my.bestie.co.kr/cmd%ED%82%A4-%ED%95%9C%EC%98%81-%EB%B3%80%ED%99%98/)
