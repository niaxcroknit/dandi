# 단디 – 대체실 사이즈 계산기

원작실 대신 내 실로 뜰 때, 원하는 사이즈가 나오려면 도안의 어느 사이즈를 떠야 하는지 알려주는 뜨개 계산기예요.

- 앱 ID: `com.nia.dandiknit`
- 현재 버전: 1.3 (versionCode 8)
- 최소 Android 7.0 (SDK 24), 대상 SDK 36

## 폴더 구성

| 위치 | 내용 |
|---|---|
| `/` (저장소 맨 위) | Android Studio 프로젝트. 이 폴더를 그대로 Open 하면 돼요 |
| `app/src/main/assets/public/index.html` | 앱 화면 전체 (계산기 코드) |
| `docs/` | 웹앱(PWA) 버전. GitHub Pages로 https://niaxcroknit.github.io/dandi/ 에 공개돼요 |
| `store/` | 스토어 설명, 출시 노트, 개인정보처리방침, 스크린샷 |

Node.js 없이 빌드되도록 Capacitor와 플러그인(광고, 결제) 코드를 프로젝트 안에 넣어 두었어요.

## 빌드하기 (Android Studio만 있으면 돼요)

1. 이 저장소를 내려받아 Android Studio에서 **Open** 해요.
2. Gradle Sync가 끝나면 ▶로 폰에서 확인해요.
3. **Build › Generate Signed App Bundle**에서 기존 키스토어(`.jks`)를 골라 .aab를 만들어요.
   키스토어 파일은 절대 이 저장소에 올리지 마세요 (`.gitignore`로 막아 두었어요).

새 버전을 낼 때는 `app/build.gradle`의 `versionCode`를 1씩, `versionName`을 올려요.

## 광고 (Google AdMob)

- 앱 ID: `app/src/main/res/values/strings.xml`의 `admob_app_id`
- 배너 광고 단위 ID: `app/src/main/assets/public/index.html`의 `AD_UNIT_ID`
- 광고는 안드로이드 앱에서만 나오고, 웹 버전에는 없어요.
- 광고를 못 불러오면 광고 자리는 자동으로 사라져요.

## 프리미엄 (앱 내 결제) – 지금은 꺼져 있어요

- 상품 ID `dandi_premium` (₩1,000, 한 번 결제): 프로젝트 무제한 + 광고 없음
- Play Console에서 이 상품을 **활성화하기 전까지** 앱에는 결제 버튼과 프로젝트 10개 한도가 나타나지 않아요.
- 상품을 활성화하면 앱을 다시 올리지 않아도 자동으로 켜져요. 산 기록은 앱을 켤 때와 내 보관함을 열 때 자동으로 되살려요.
- 결제를 켜기 전에 할 일: 통신판매업 신고번호를 Play Console 계정 세부정보에 넣기, 결제 프로필 만들기, 콘텐츠 등급의 "디지털 상품 구매"를 예로 바꾸기, 개인정보처리방침에 결제 항목 추가하기.

## 웹 버전

GitHub 저장소 Settings › Pages에서 Source를 `Deploy from a branch`, Branch를 `main` / `/docs`로 두면 https://niaxcroknit.github.io/dandi/ 로 열려요.

## 웹 버전 고치기

화면을 고칠 때는 `app/src/main/assets/public/index.html`과 `docs/index.html`이 같은 내용이에요. 한쪽을 고치면 다른 쪽에도 똑같이 복사해 주세요. 웹 버전을 고친 뒤에는 `docs/sw.js`의 `CACHE` 이름을 바꿔야 사용자 폰에서 새 버전으로 바뀌어요.
