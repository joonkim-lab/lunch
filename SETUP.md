# 오늘점심 — 설치 순서 (1단계)

1. **Firebase 콘솔** (기존 Qum 프로젝트 재사용)
   - 프로젝트 설정 → 웹 앱 → `firebaseConfig` 복사 → `index.html` 상단 `PASTE_HERE` 6곳에 붙여넣기
   - Authentication → Sign-in method → Google 켜져 있는지 확인
   - Authentication → Settings → 승인된 도메인에 `joonkim-lab.github.io` 추가
   - Firestore → 규칙 탭 → 기존 규칙 안의 `match /databases/{db}/documents {` 블록에 `firestore.rules`의 세 `match` 블록과 함수 4개를 합쳐 넣기 (기존 컬렉션 규칙은 그대로 두기)
2. **GitHub**: `joonkim-lab/lunch` 저장소 만들고 `index.html` 푸시 → Settings → Pages → main 브랜치
3. **첫 로그인**: `joon.kim@educclesia.com`으로 들어가면 바로 관리쌤 화면
4. **학생 명단** 탭에서 `이름, 이메일` 붙여넣기 → 등록
5. **메뉴 입력** 탭에서 다음주 메뉴 12칸 채우고 게시
6. 학생들에게 링크 전달 → 금요일 13:00 자동 마감 → **신청 현황** 탭 → 출력

컬렉션은 `lunch_users` / `lunch_weeks` / `lunch_orders` 세 개라 기존 플랫폼 데이터와 섞이지 않습니다.
