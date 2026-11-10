# S-Tec-Business-Site-Overview

**v1.7.1** · 에스텍베스트 본사와 동부·서부·남부·중부 4개 지사가 관리하는 고객사 사업장의 위치, 인원구성, 근무형태를 지도로 보는 현장관리 서비스입니다. 본사·지사 직원과 관리 지사장이 현장에 갈 때 사업장 위치와 현황을 바로 확인하도록 만들었습니다.

- 웹 주소: https://sadness500-boop.github.io/S-Tec-Business-Site-Overview/
- 안드로이드 앱: [stec-sitemap.apk 내려받기](https://github.com/sadness500-boop/S-Tec-Business-Site-Overview/releases/latest/download/stec-sitemap.apk)
- 아이폰: 위 웹 주소를 사파리로 열고 「홈 화면에 추가」

> 이 저장소는 공개 저장소입니다. 개인정보 보호를 위해 **휴대폰 번호 뒷자리 4개는 `????`로 가렸습니다**(예: 010-1234-????). 전체 번호가 들어 있는 사내용 파일·앱은 저장소에 올리지 말고 사내에서만 공유하세요.

## 주요 기능

| 기능 | 설명 |
|---|---|
| 사업장 지도 | 사업장마다 업무에 맞는 3D 피규어 핀, 지사별 색, 멀리서 보면 묶음 표시 |
| 사업장 팝업 | 관리자·직책, 연락처(뒷자리 가림), 근무형태, 인원구성(총원·남녀·보안/미화/기타), 계약일, 카카오맵 길찾기 |
| 본사·지사 | 본사 마커와 4개 지사 연결선, 지사별 투입인원 |
| 내 위치 | 휴대폰은 GPS, PC는 IP → 위치 허용 시 Wi-Fi 위치. 이동하면 실시간으로 따라감 |
| 현장 라이브 | 현재 시각·주야간 근무 현황, 오늘의 현장, 가까운 현장 |
| 다운로드 QR · 친구초대 | 사이트 주소 QR(북마크·홈 화면 추가), 주소 복사·카톡·문자 공유 |
| 제작자 관리 (v1.7.0) | 로그인·가입 승인·접속 차단·사용기한·임시 비밀번호·강제 로그아웃·접속기록·기기 관리·앱 전체 잠금, 여러 기기 화면 설정 동기화 |
| 함께 쓰는 사이트 | 오늘의 뽑기판 · 팔도 제철맛길 · 팔도 축제길 바로가기 |
| 내장 경계 지도 | 인터넷 배경지도가 막혀도 시·군·구·읍·면·동 경계 지도로 표시 |

## 파일 구성

```
index.html                     지도 앱 전체 (한 파일)
auth-config.json               로그인 서버 연결 설정 (제작자가 수정, 처음엔 꺼짐)
server/supabase_setup.sql      로그인 서버(Supabase) 설정 SQL
docs/                          사용 매뉴얼 · 제작자관리 사용매뉴얼 (Word · PPT)
manifest.webmanifest, sw.js    홈 화면에 앱으로 설치(PWA)·오프라인 열기
icons/                         앱 아이콘
package.json, capacitor.config.json
.github/workflows/android-apk.yml   안드로이드 앱 자동 빌드
.nojekyll
```

## 처음 한 번 설정

1. **웹 주소 켜기**: 저장소 Settings → Pages → Source를 `Deploy from a branch`, Branch를 `main` / `/ (root)`로 저장합니다. 몇 분 뒤 위 웹 주소가 열립니다.
2. **안드로이드 앱 빌드 권한**: Settings → Actions → General → Workflow permissions를 `Read and write permissions`로 저장합니다.
3. **안드로이드 앱 만들기**: `index.html`을 올리면 자동으로 빌드됩니다. 바로 만들려면 Actions 탭 → `Android APK` → `Run workflow`를 누릅니다. 5~10분 뒤 Releases에 `stec-sitemap.apk`가 붙습니다.

## 제작자 관리 (로그인)

로그인 · 사용 권한 · 관리자 페이지 · 여러 기기 동기화. 서버는 무료 **Supabase**를 씁니다. S-Tec short estimate 와 **같은 서버를 함께 써도** 됩니다(아이디 하나로 두 프로그램).

- **켜는 법:** ① Supabase 프로젝트 준비 → ② SQL Editor에서 [`server/supabase_setup.sql`](server/supabase_setup.sql) 실행(제작자 이메일 한 곳 수정) → ③ [`auth-config.json`](auth-config.json)에 Project URL · publishable(anon) 키 입력, `"enabled": true` → ④ 제작자 이메일로 가입(또는 견적 프로그램 아이디로 로그인)하면 **제작자(owner)**.
- **끄는 법:** `auth-config.json` 의 `"enabled": false` — 다음 실행부터 로그인 없이 사용.
- 안드로이드·아이폰 앱도 이 저장소의 `auth-config.json` 을 읽습니다.
- 비밀번호는 서버에 암호화(bcrypt) 저장되어 제작자도 볼 수 없습니다. **service_role · secret 키는 절대 저장소·앱에 넣지 마세요.**
- 자세한 순서: [제작자관리 사용매뉴얼 (Word)](docs/S-Tec-Business-Site-Overview_제작자관리_사용매뉴얼_v1.7.0.docx) · [PPT](docs/S-Tec-Business-Site-Overview_제작자관리_사용매뉴얼_v1.7.0.pptx)
- 직원용: [사용 매뉴얼 (Word)](docs/S-Tec-Business-Site-Overview_사용매뉴얼_v1.7.0.docx) · [PPT](docs/S-Tec-Business-Site-Overview_사용매뉴얼_v1.7.0.pptx)

## 휴대폰에 설치하기

**안드로이드**
1. 위 apk 링크를 엽니다(휴대폰에서).
2. 내려받은 `stec-sitemap.apk`를 눌러 설치합니다.
3. 「출처를 알 수 없는 앱」 안내가 나오면 **이 출처 허용**을 켜고 다시 설치합니다.
4. 처음 실행할 때 위치 권한을 **허용**하면 내 위치가 실시간으로 표시됩니다.

**아이폰**
1. 사파리로 웹 주소를 엽니다(QR을 찍어도 됩니다).
2. 아래쪽 **공유 버튼** → **홈 화면에 추가**를 누릅니다.
3. 홈 화면의 **S-Tec-Business-Site-Overview** 아이콘으로 앱처럼 실행합니다. 위치를 물으면 **허용**을 누릅니다.

> 앱스토어에 올리는 정식 아이폰 앱은 맥(Xcode)과 애플 개발자 계정(연 99달러)이 있어야 만들 수 있습니다. 이 저장소에는 그 준비(Capacitor 설정)가 들어 있어, 맥에서 `npm install && npm run www && npx cap add ios && npx cap open ios`로 이어서 만들 수 있습니다.

## 내용 고치기

사업장 현황이 바뀌면 새 사업장 주소록 엑셀로 `index.html`을 다시 만들어 이 저장소의 같은 파일을 바꿔 올립니다. 올리면 웹 주소와 안드로이드 앱이 함께 새 버전이 됩니다(안드로이드는 apk를 다시 설치).

---
자료: 에스텍베스트 사업장 주소록 · 좌표: 카카오맵 주소 검색 · 경계: 통계청 · 배경지도: Esri

*Designed & Developed by Rat Rae Choi*
