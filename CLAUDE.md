# 타건 무대 (tageon-stage)

K-POP 곡 컨셉별로 화면 디자인이 바뀌는 한글 타자 연습 웹앱. 개인용(사용자: 예원). 새로 산 기계식 키보드로 재밌게 타자 치려는 목적.

## 구조
- `index.html` 단일 파일. HTML + CSS + JS 전부 인라인, 빌드 도구 없음. 외부 리소스는 Google Fonts뿐.
- 배포: GitHub Pages (`main` 브랜치 루트). 스포티파이 OAuth 때문에 https 주소 필요.
- 로컬 실행: `python -m http.server 8000 --bind 127.0.0.1` 후 http://127.0.0.1:8000 (스포티파이는 `localhost`가 아니라 `127.0.0.1`만 허용)

## 코드 지도 (index.html `<script>` 안, 섹션 주석 `/* ───────── ... ───────── */` 기준)
- `THEMES` — 컨셉 테마 17종. 색 토큰(c), 배경(bgimg), 폰트(fd/ft), 배경 애니메이션(amb), 타건 파티클(key), 오버레이(deco: grain/chrome/scan/vignette/cam), 타이틀 효과(title), 오리지널 연습 문장(lines)
- `SONGS` — 곡 카탈로그 `[id, 제목, 아티스트, 영문명, 세대, 테마, 다른제목[], 다른아티스트명[]]`. 2~5세대, 스트레이키즈 제외, 영어 적은 곡 위주
- hangul — 자모 분해(`keysOf`), IME 조합 중 판정(`composingOk`). 타수는 자모 기준
- lyric cleanup — `processLyrics`: LRC 타임스탬프 파싱, [Verse] 태그 제거, 괄호 애드립 제거, 영어 처리(keep/words/lines), 긴 줄 분할
- session — `newSession`, `onInput`, `advance`, `finish`. 모드: practice / karaoke(LRC 타이밍)
- canvases — `AMB`(배경 애니메이션), `FXD`(타건 파티클), 박자(BPM 탭) 펄스는 CSS 변수 `--pulse`
- Spotify — Authorization Code + PKCE, 클라이언트만. scope `user-read-currently-playing user-read-playback-state`. 3초 폴링, 곡 매칭(`matchTrack`) 후 테마 자동 전환 + 노래방 싱크

## 저장 (localStorage)
`tg.settings`, `tg.lyrics`, `tg.records`(키: `songId|concept|lyrics|karaoke`), `tg.sp`(토큰), `tg.pkce`. 백업 내보내기/불러오기 있음.

## 원칙
- 실제 가사 원문을 코드에 넣지 않는다. 가사는 실행 중 LRCLIB(lrclib.net, CORS 허용)에서 가져오거나(`findLyrics`/`autoLyrics`, 스포티파이 곡 매칭 시 자동) 사용자가 붙여넣는다. 연습용 기본 문장은 각 테마의 오리지널 문장.
- 공식 로고/앨범아트/캐릭터 사용 금지. 컨셉 분위기만 색·폰트·질감으로 재현.
- 효과음 없음(키보드 소리 즐기는 용도). 시각 이펙트만.
- `prefers-reduced-motion` 존중. 모바일 폭(400px)에서도 깨지지 않게.
- 2026-02 스포티파이 정책: 새 Dev Mode 앱은 Premium 필요, 사용자 5명 제한, 일부 엔드포인트만. 사용자는 네이버 멤버십 연동 Premium 베이직.

## 할 일 후보
- GitHub Pages 배포 후 스포티파이 currently-playing 실제 동작 확인
- 곡 추가 요청 반영
- LRC 싱크 미세조정 UX
