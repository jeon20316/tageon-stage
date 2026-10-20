# 타건 무대

K-POP 곡 컨셉에 맞춰 화면이 바뀌는 한글 타자 연습 웹앱.

## 실행
- 그냥 보기: `index.html` 더블클릭 (스포티파이 연동만 빼고 전부 동작)
- 스포티파이까지: `python -m http.server 8000 --bind 127.0.0.1` 실행 후 http://127.0.0.1:8000 접속, 또는 GitHub Pages 주소

## GitHub Pages 배포
1. GitHub에 새 저장소(Public) 만들기
2. 이 폴더를 push (`git init` → `git add .` → `git commit` → `git remote add origin ...` → `git push -u origin main`)
3. Settings → Pages → Branch `main` / root → Save

## 스포티파이 연결
1. 앱 설정에서 Redirect URI 복사
2. developer.spotify.com/dashboard → Create app → Redirect URI 붙여넣기, Web API 체크
3. Client ID를 앱 설정에 붙여넣고 연결
4. 권한 오류가 나면 앱의 User Management에 내 스포티파이 이메일 추가
