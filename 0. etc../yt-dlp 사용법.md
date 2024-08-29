# 🚀 

## 정의

- yt-dlp : Youtube와 기타 다양한 비디오 및 오디오 플랫폼에서 콘텐츠를 다운로드 할 수 있는 오픈소스 명령줄 프로그램

## 설치

- `brew install ffmpeg`
- `brew install yt-dlp/taps/yt-dlp

## 사용방법

- `yt-dlp -F 'URL'` : 포맷 목록 보기
- `yt-dlp -f 영상해상도번호+음질음원번호 'URL'`: 특정 포맷 다운로드
- `yt-dlp -f 영상해상도 번호 'URL' --recode-video mp4 'URL'`: mp4형식으로 변환 후 다운로드
- `yt-dlp -f 음질음원번호 --audio-format mp3 'URL'`: mp3포맷으로 음원 다운로드

---

# 🔗레퍼런스

## 참고 강의/글

- [yt-dlp 사용법 (맥, 윈도우)](https://madanhambo.tistory.com/entry/yt-dlp-%EC%82%AC%EC%9A%A9%EB%B2%95)
- [yt-dlp : 깃허브](https://github.com/yt-dlp/yt-dlp)