# 🚀 
## 맥북의 특정 키보드를 Function키로 맵핑하는 방법

- `hidutil`을 사용하여 맥북의 특정 키보드를 Function키로 맵핑할 수 있다.
- `hidutil`은 macOS에서 HID(인간-컴퓨터 인터페이스) 장치를 제어하기 위한 유틸리티이다.
- `hidutil key remapping generator for Mac OS를 사용

## right_command -> F18 / right_option -> F19로 맵핑하는 코드

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
3. 위의 코드를 복사하여 붙여넣기
4. 그러면 이제 재부팅시 자동실행되어 맵핑이 적용된다.


---

# ✨느낀 점

- 지금까지 Karabiner-Elements를 사용하여 키보드 맵핑을 했었다.
- Karabiner-Elements는 가끔씩 한영키 반응속도가 느렸다.

---

# 🔗레퍼런스

## 참고 강의/글
- [hidutil key remapping generator for MacOS 사이트](https://hidutil-generator.netlify.app/)
- [Karabiner 설치없이 오른쪽 CMD키로 한/영 변환하기](https://my.bestie.co.kr/cmd%ED%82%A4-%ED%95%9C%EC%98%81-%EB%B3%80%ED%99%98/)