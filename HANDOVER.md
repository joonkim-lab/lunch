# 오늘점심 (lunch) — HANDOVER

## 무엇을 만드는가
학교 점심 신청앱. 행정선생님 1명의 취합·프린트 업무를 없애는 것이 목표.
제작 주체 표기: 하단에 작게 `Educclesia Group`, 상단바는 앱 이름 `오늘점심`.

## 확정된 규칙 (바꾸지 말 것, 바꾸려면 사용자 확인)
- 급식 요일: **월·화·목·금** (수요일 없음)
- 메뉴 3종: **한식 / 샐러드 / 샐러위치** (샐러위치 = 샌드위치+샐러드 세트)
- 학생 선택지는 4개: 위 3종 + **안 먹음**
- 마감: **금요일 13:00 KST**, 다음주 분을 신청
- 마감 후 미신청자는 **한식 자동 배정**. 단 출력물에서 이름 옆에 `○` 표시 (런치듀티는 동일하게 배부, 관리쌤만 식별)
- **대회 제외**: 운동특기 학생이 대회로 점심이 필요 없는 날 → 운영진/관리쌤이 표에서 일괄 체크. 체크된 날은 학생 화면에서 잠기고, 자동 한식 배정·독촉·출력·수량표에서 모두 빠짐
- 학생 수 100명 이하
- 역할 3개: `admin`(관리쌤) / `staff`(운영진, 코치 포함) / `student`

## 스택
- 단일 파일 `index.html` (모듈 스크립트, 빌드 없음) → GitHub Pages
- Firebase Auth(구글 로그인) + Firestore
- 기존 Qum 프로젝트 재사용, 컬렉션 접두사 `lunch_` 로 분리
- admin 이메일: `joon.kim@educclesia.com`

## Firestore 스키마
```
lunch_users/{email}        { name, role, active, discordId? }
lunch_weeks/{YYYY-MM-DD}   { menu:{mon:{korean,salad,salawich},...}, excluded:{email:[요일키]}, published }
lunch_orders/{week}_{email}{ week, email, name, choices:{mon:"korean"|...|"none"}, submittedAt }
```
주 ID는 그 주 **월요일 날짜**. 마감 = 월요일 - 3일 + 13시 KST.

## 진행 단계
- [x] 1단계 — 학생 신청 + 관리 화면 + 대회 제외 + PDF 5장 출력
- [ ] 2단계 — 업체 메뉴 이미지 업로드 → Claude 비전으로 12칸 자동 판독 → 관리쌤이 확인 후 게시 (Cloudflare Workers 프록시 경유, API 키 노출 금지)
- [ ] 3단계 — 디스코드 미신청자 자동 독촉 (Workers 크론: 목 09시, 금 09시, 금 12시 / 대회 제외자는 제외)
- 캘린더 연동은 **하지 않기로 함** (오버스펙)

## 작업 방식
- 한 번에 한 단계씩, 진행 전 사용자 확인
- 커밋은 작게, GitHub이 단일 소스 (mac-mini `~/work` 기준)
