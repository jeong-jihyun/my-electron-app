# my-electron-app

**Electron(일렉트론) 공식 튜토리얼의 "메뉴로 숫자 올리고 내리기" 예제를 따라 만든 데스크톱 앱**입니다. (2023-08)
창 하나에 `Current value: 0`이 표시되고, **상단 메뉴의 `Increment` / `Decrement`** 를 누르면 숫자가 1씩 오르내립니다. 바뀐 숫자는 터미널(Node 콘솔)에도 출력됩니다.

## 동작 방식

| 파일 | 역할 |
| --- | --- |
| `main.js` | 앱의 본체(메인 프로세스). 창과 메뉴를 만들고, 메뉴를 누르면 화면 쪽으로 `update-counter` 신호(+1 / -1)를 보냄. 화면이 돌려준 `counter-value`를 콘솔에 출력. 개발자 도구를 항상 함께 엶 |
| `preload.js` | 화면에 `window.electronAPI.handleCounter`만 안전하게 열어 주는 다리 (`contextBridge`) |
| `renderer.js` | 화면(렌더러) 쪽 코드. 신호를 받으면 숫자를 바꾸고 새 값을 메인 쪽으로 돌려보냄 |
| `index.html` | 화면. `Current value: <숫자>` 한 줄. 외부 스크립트를 막는 보안 설정(CSP) 포함 |

```
메뉴 클릭 → main.js가 update-counter(±1) 전송 → renderer.js가 숫자 변경 → counter-value 회신 → main.js가 콘솔에 출력
```

## 사용 기술

| 구분 | 내용 |
| --- | --- |
| 데스크톱 앱 | Electron 26 |
| 실행·패키징 도구 | Electron Forge 6 (`@electron-forge/cli`) |
| 화면 | 순수 HTML + JavaScript |

## 실행 명령

| 명령 | 설명 |
| --- | --- |
| `npm start` | 앱 실행 (`electron-forge start`) |
| `npm run package` | 실행 파일로 묶기 |
| `npm run make` | 설치 파일 만들기 |

## 실행 방법

```bash
git clone https://github.com/jeong-jihyun/my-electron-app.git
cd my-electron-app
npm install
npm start
```

화면이 있는 컴퓨터(윈도우·맥·리눅스 데스크톱)에서 실행해야 합니다.

## 확인 내역 (2026-10)

| 점검 | 결과 |
| --- | --- |
| `main.js`, `preload.js`, `renderer.js` 문법 검사 | 이상 없음 |
| `npm ci` (Electron 실행 파일 내려받기 제외) | 성공 |
| 앱 실행 | 이 작업 환경에는 화면이 없고 Electron 실행 파일도 받을 수 없어 **실행해 보지 못했습니다** (코드를 읽고 동작을 설명했습니다) |
| 코드 오류 | 발견하지 못해 코드는 수정하지 않았습니다 |

## 앞으로 손보면 좋은 점

- `mainWindow.webContents.openDevTools()`가 항상 실행됩니다. 배포할 때는 제거하세요.
- `package.json`의 `description`이 비어 있습니다.
- `npm run package`, `make`에 쓰는 Forge 설정이 없어 기본값으로 동작합니다. 앱 이름·아이콘 등을 지정하려면 `forge.config.js`를 추가하세요.
- 테스트 코드가 없습니다.
