# AGENTS.md — i2r 안내판 (AI가 먼저 읽는 파일)

이 파일은 **AI(Claude, ChatGPT, Gemini, Cursor 등)가 i2r 개발을 시작할 때 처음 읽는 안내판**입니다.
i2r 제품마다 저장소가 따로 있습니다. 여기서는 **어느 저장소로 갈지**와 **처음 준비하는 순서**만 정합니다.
실제 하드웨어 정보와 규칙은 각 저장소의 AGENTS.md, CLAUDE.md에 있으니 거기를 따르세요.

> **이 파일과 키트 안내서는 원문 그대로 읽습니다.** 명령을 실행할 수 있으면 `curl -sL https://raw.githubusercontent.com/kdi6033/i2r/main/AGENTS.md`처럼 받아 읽습니다. 웹 페이지 읽기 도구(WebFetch 등)는 요약만 돌려주어 규칙을 놓칩니다.

사용자는 보통 이렇게 시작합니다.

```
https://github.com/kdi6033/i2r 읽고 i2r 개발을 도와줘
https://github.com/kdi6033/i2r 읽고 i2r 개발을 도와줘. 모두 받아 줘
https://github.com/kdi6033/i2r 읽고 i2r 개발을 도와줘. plc 개발 환경을 만들어 줘
https://github.com/kdi6033/i2r 읽고 i2r 개발을 도와줘. i2r-03 온도 30도 넘으면 출력 1 켜 줘
i2r 개발을 도와줘 / otto 개발을 도와줘     (i2r 스킬을 설치한 뒤에는 주소 없이)
```

사용자는 대부분 학생과 초보자입니다. **한국어**로, 짧고 쉽게, 다음에 무엇을 하면 되는지 알려 주세요.

---

## 1. 저장소 지도

| 사용자가 말하는 것 | 저장소 | 내용 |
|---|---|---|
| plc, i2r-02, i2r-03, i2r-04, 릴레이, 입력/출력, 온습도 제어 | [kdi6033/i2r-plc](https://github.com/kdi6033/i2r-plc) | IoT PLC AI 코딩 키트 |
| otto, 오토, Otto 로봇, 걷는 로봇, i2r-05 로봇 | [kdi6033/otto](https://github.com/kdi6033/otto) | Otto I2R 로봇 AI 코딩 키트 |
| 챗봇, AI 챗봇, LLM, Gemini, 음성 대화, 음성 인식(STT), 음성 출력(TTS), 챗봇 성격·말투 바꾸기, 말로 LED·로봇 움직이기, i2r-shield-03, step1·step2·step3, llm.ino | [kdi6033/i2r-05](https://github.com/kdi6033/i2r-05) 의 `file/chatbot/` | i2r-05 보드 + i2r-shield-03 AI 챗봇 키트 (예제: step1 → step2 → step3 → llm) |
| 서버, 시뮬레이터, 가상 보드, 프로토콜 시험, 대시보드, PLC 웹 제어(휴대폰으로 PLC, 보드 웹서버, standalone, 스케줄, 입력 규칙, 센서 트리거), Otto 휴대폰 조종(otto.local) | [kdi6033/i2r-server](https://github.com/kdi6033/i2r-server) | 시뮬레이터, 연결 방식 세 가지: `standalone/` 보드 혼자 웹서버 ✅ (PLC `i2r-02/03/04`, Otto 로봇 `i2r-otto` → `http://otto.local`), `local/` 현장 서버(i2r-05), `aws/` 아마존 서버 (만드는 중) |

라이브러리는 보통 **받지 않습니다.** 각 키트가 아두이노 라이브러리 매니저로 설치합니다.
사용자가 라이브러리 자체를 고치고 싶다고 할 때만 받습니다.

| 라이브러리 | 저장소 | 쓰는 곳 |
|---|---|---|
| I2R_PLC | [kdi6033/I2R_PLC](https://github.com/kdi6033/I2R_PLC) | i2r-02/03/04 입출력, 타이머, 온습도 |
| I2R_IoT | [kdi6033/I2R_IoT](https://github.com/kdi6033/I2R_IoT) | Wi-Fi, MQTT, 시간 (보드 쪽 통신) |
| OttoI2R | [kdi6033/OttoI2R](https://github.com/kdi6033/OttoI2R) | Otto 로봇 동작 |

- i2r 통신 프로토콜(MQTT 토픽, JSON 명령, 축약 코드의 뜻)의 **원본은 [i2r-server/protocol.md](https://github.com/kdi6033/i2r-server/blob/main/protocol.md)** 입니다. 원문을 읽습니다: `curl -sL https://raw.githubusercontent.com/kdi6033/i2r-server/main/protocol.md`
  - 이 저장소 README 5장은 요약과 링크만 있습니다. 예전 5장 표의 `t`(숫자), `rm`(0/1), `start`·`end`(분), `df`는 실제와 다르니 쓰지 않습니다.
  - 사용자 스케치는 JSON을 직접 만들지 않고 각 키트의 라이브러리 함수를 씁니다. protocol.md는 라이브러리, 서버, 시뮬레이터를 고칠 때 봅니다.
- **그냥 "plc"라고만 하면** 다른 회사 PLC(지멘스, LS 등)일 수 있으니 "i2r PLC(i2r-02/03/04)인가요?"라고 한 번 묻습니다.
- **그냥 "otto"라고만 하면** 이 안내판을 통해 왔다면 Otto I2R 로봇으로 봅니다. 일반 Otto DIY(아두이노 나노) 이야기가 분명하면 i2r 키트를 쓰지 않습니다.

### 1.1 무엇을 받을지 정하기

| 사용자가 말한 것 | 받을 키트 |
|---|---|
| "plc", "otto", "서버", "시뮬레이터", "챗봇"처럼 키트를 말함 | **묻지 않고** 그 키트만 (여러 개 말하면 그것들) |
| "모두", "전부", "다 받아 줘" | **묻지 않고** 넷 다: i2r-plc, otto, i2r-server, i2r-05(챗봇) |
| 키트를 말하지 않음 ("i2r 개발을 도와줘"만) | 아래 질문을 **한 번만**, 이 문장 그대로 묻습니다 |

```
어떤 개발 환경을 만들까요?
 1. 모두 다 (PLC + Otto 로봇 + 시뮬레이터·서버 + AI 챗봇) ← 추천
 2. 골라서 받기 (PLC / Otto 로봇 / 시뮬레이터·서버 / AI 챗봇 중 여러 개 선택)
```

- 선택 질문 도구(AskUserQuestion 등)가 있으면 그것으로 묻습니다. 2번을 고르면 네 키트를 여러 개 고를 수 있게 한 번 더 묻습니다.
- 이 단계에서 보드(i2r-02/03/04 등)는 묻지 않습니다. 보드는 프로그램을 만들 때 각 키트의 안내대로 묻습니다.
- 사용자에게 물을 수 없는 상황(자동 실행)이면 1번(모두 다)으로 하고, 마지막에 그렇게 했다고 알립니다.
- 나중에 "otto도 받아 줘"처럼 말하면 그 키트만 더 받습니다 (4.1, 이미 있는 키트는 다시 받지 않음).

## 2. 지금 어디서 대화하는지 판단

| 상황 | 하는 일 |
|---|---|
| **채팅** (claude.ai, ChatGPT, Gemini: 명령을 실행할 수 없음) | 3장 |
| **명령을 실행할 수 있음** (Claude Code, Codex, Cursor 등) | 4장 |

## 3. 채팅에서

1. 1장 지도에서 고른 키트의 AGENTS.md 원문을 읽고 그대로 따릅니다.
   - PLC: https://raw.githubusercontent.com/kdi6033/i2r-plc/main/AGENTS.md
   - Otto: https://raw.githubusercontent.com/kdi6033/otto/main/AGENTS.md
   - AI 챗봇: https://raw.githubusercontent.com/kdi6033/i2r-05/main/file/chatbot/CLAUDE.md (예제 코드는 같은 폴더의 step1/step1.ino 등을 원문으로 읽음)
2. 코드는 처음부터 끝까지 전체를 주고, 사용자가 Arduino IDE로 올리게 합니다. 처음이면 그 키트 README의 "처음 한 번 준비"(Arduino IDE, 보드 설정, 라이브러리)를 안내합니다.
3. 시뮬레이터와 서버는 채팅에서 켤 수 없습니다. [i2r-server README](https://github.com/kdi6033/i2r-server)의 "직접 켜기"를 안내하거나 Claude Code를 권합니다.
4. 다음부터 주소 없이 쓰고 싶다고 하면 6장을 안내합니다.

## 4. 명령을 실행할 수 있을 때 (Claude Code 등)

### 4.1 작업 폴더 보기

사용자가 연 폴더(**지금 대화를 시작한 폴더**, `pwd`로 확인)가 **작업 폴더**입니다. 먼저 안을 봅니다.

- 저장소는 **반드시 작업 폴더 안에** 받습니다. 홈 폴더, `/tmp`, `~/tmp`, 임시 폴더 같은 다른 곳에 받지 않습니다. 명령을 실행할 때마다 작업 폴더 경로를 그대로 씁니다.

- `i2r-plc/`, `otto/`, `i2r-server/`, `i2r-05/`가 이미 있으면 **다시 받지 않습니다.** 필요하면 그 폴더에서 `git pull --ff-only`만 합니다.
- 작업 폴더 자체가 키트 저장소(예: 폴더 안에 바로 `AGENTS.md`, `examples/`)라면 그 키트로 바로 작업하고, 다른 키트는 상위 폴더가 아니라 **사용자에게 물어서** 받을 곳을 정합니다.
- 비어 있거나 키트가 없으면 4.2로 갑니다.

### 4.2 필요한 키트 받기

1. `git --version`으로 Git을 확인합니다. 없으면 https://git-scm.com 설치를 안내합니다.
2. 1.1에서 정한 키트만 작업 폴더 안에 받습니다.
   ```
   git clone https://github.com/kdi6033/i2r-plc
   git clone https://github.com/kdi6033/otto
   git clone https://github.com/kdi6033/i2r-server
   git clone --depth 1 https://github.com/kdi6033/i2r-05
   ```
   AI 챗봇(i2r-05)은 사진이 많아 `--depth 1`로 받습니다. 챗봇 예제는 `i2r-05/file/chatbot/` 에 있습니다.
   이 i2r 저장소는 받지 않아도 됩니다(사진이 많아 큽니다). 이 안내판은 주소로 읽습니다.
3. **바로 작업 폴더 맨 위에 작업 폴더 안내(4.3)를 만듭니다.** 설치 도중에 멈춰도 다음에 이어서 할 수 있게, 키트를 받은 직후에 만듭니다.
4. 받은 키트 폴더의 **CLAUDE.md(없으면 AGENTS.md)를 읽고** (AI 챗봇은 `i2r-05/file/chatbot/CLAUDE.md`), 거기 적힌 "처음 한 번 환경 만들기"를 그대로 합니다.
   - i2r-plc, otto: arduino-cli, esp32 보드 패키지, 라이브러리 설치, 예제 컴파일
   - i2r-server: Python, paho-mqtt 확인, 서버 고르기, 시뮬레이터 켜기
   - AI 챗봇: esp32 보드 패키지, ESP32-audioI2S-master 라이브러리, step1 컴파일. Gemini API 키와 Wi-Fi는 업로드할 때 묻습니다
   - 시뮬레이터처럼 **계속 켜져 있는 프로그램은 백그라운드로** 실행합니다. 앞에서 실행하면 대화가 멈춥니다.
   - **여러 키트를 받았으면** 같은 것은 한 번만 합니다: esp32 보드 패키지는 한 번 설치하고, 라이브러리는 두 키트의 목록을 합쳐 한 번에 설치하고, 예제는 키트마다 하나씩 컴파일합니다. i2r-server는 Python, paho-mqtt만 확인하고, 시뮬레이터는 사용자가 켜 달라고 할 때 서버를 물어 켭니다.
   - 사용자에게 물을 수 없는 상황(자동 실행)이면 기본값(서버 1번 등)으로 하고, 무엇을 골랐는지 마지막에 알려 줍니다.
5. 6장 i2r 스킬 설치를 제안합니다.
6. 끝나면 "✅ 준비 완료", 받은 키트와 설치한 것 목록, 다음에 말해 볼 문장 하나를 보여 줍니다.

### 4.3 작업 폴더 안내 (작업 폴더 맨 위 CLAUDE.md)

다음에 이 폴더를 열었을 때 Claude가 처음부터 무엇이 있는지 알도록, 작업 폴더 맨 위에 `CLAUDE.md`를 만듭니다.
이미 있으면 덮어쓰지 말고, 아래 내용이 없을 때만 덧붙입니다. 받은 키트만 표에 적습니다.

```markdown
# i2r 작업 폴더

i2r 개발을 하는 폴더입니다. 전체 안내판: https://raw.githubusercontent.com/kdi6033/i2r/main/AGENTS.md

| 폴더 | 내용 | 먼저 읽을 파일 |
|---|---|---|
| i2r-plc/ | IoT PLC 키트 (i2r-02/03/04) | i2r-plc/CLAUDE.md |
| otto/ | Otto I2R 로봇 키트 | otto/CLAUDE.md |
| i2r-server/ | 시뮬레이터, 서버 | i2r-server/CLAUDE.md |
| i2r-05/file/chatbot/ | AI 챗봇 키트 (i2r-05 + shield-03, Gemini) | i2r-05/file/chatbot/CLAUDE.md |

- 사용자가 무엇을 하려는지 보고, 그 폴더의 CLAUDE.md를 먼저 읽고 따른다.
- 표에 없는 키트가 필요하면 안내판 1장을 보고 이 폴더 안에 받은 뒤 표에 더한다.
- "전부 최신으로 업데이트해 줘": 표의 폴더마다 `git pull --ff-only`, 새로 들어온 것을 3줄 이내로 알려 준다.
- 사용자가 만든 프로그램은 각 키트의 my_sketches/ 안에 둔다.
```

## 5. 업데이트

- "최신으로 업데이트해 줘", "전부 최신으로": 작업 폴더 안의 키트마다 `git pull --ff-only`를 합니다.
- 사용자가 고친 파일 때문에 받지 못하면 **지우거나 되돌리지 말고** 어떤 파일인지 알려 줍니다.
- 이 안내판과 i2r 스킬은 주소로 읽으므로 따로 업데이트할 것이 없습니다.

## 6. 다음부터 주소 없이 쓰기 (i2r 스킬)

### Claude Code

사용자에게 "다음부터 주소 없이 'otto 개발을 도와줘'처럼 말할 수 있게 이 PC에 i2r 스킬을 설치할까요?"라고 묻고, 좋다고 하면 설치합니다.

- 원본: https://raw.githubusercontent.com/kdi6033/i2r/main/skills/i2r/SKILL.md
- 설치할 곳: 사용자 폴더의 `.claude/skills/i2r/SKILL.md` (Windows: `%USERPROFILE%\.claude\skills\i2r\SKILL.md`, macOS/Linux: `~/.claude/skills/i2r/SKILL.md`)
- 원본을 그대로 받아 저장합니다(예: `curl -sL <원본 주소> -o <설치할 곳>`, 폴더가 없으면 먼저 만듦).
- 설치한 뒤 "**새 대화**부터 어느 폴더에서나 'otto 개발을 도와줘', 'plc 개발을 도와줘', '서버 개발을 도와줘'라고 말하면 됩니다"라고 알려 줍니다.

### claude.ai 채팅

AI가 설정을 대신 바꿀 수 없으므로 사용자에게 안내만 합니다.

1. https://github.com/kdi6033/i2r/raw/main/skills/i2r.zip 을 내려받습니다.
2. claude.ai **설정 → 기능 → 스킬**에서 **스킬 업로드**로 zip을 올립니다(압축은 풀지 않음).
3. 새 대화에서 "otto 개발을 도와줘"처럼 말합니다.

### ChatGPT

설정 → 맞춤 설정(Custom instructions)에 아래 한 줄을 넣도록 안내합니다.

```
내가 otto, plc, i2r 서버 개발을 말하면 https://raw.githubusercontent.com/kdi6033/i2r/main/AGENTS.md 를 먼저 읽고 따라 줘.
```

## 7. 안전 (꼭 지키기)

- 릴레이(PLC)에는 220V 장치가, Otto에는 움직이는 모터가 연결될 수 있습니다. 업로드 전에 각 키트의 안전 확인을 그대로 합니다.
- **i2r-02, i2r-04 입력은 무전압 접점입니다.** 전압을 넣으라고 안내하지 않습니다.
- 공개 MQTT 서버는 누구나 볼 수 있습니다. 실제 보드의 MAC, 그룹, Wi-Fi 비밀번호를 파일에 적거나 커밋하지 않습니다.
- 사용자가 알려 준 비밀번호는 `secrets.h` 같은 정해진 곳에만 넣고, 다른 파일이나 출력에 옮겨 적지 않습니다.
- 키트의 `examples/`, `boards/`는 사용자가 요청할 때만 고칩니다. 새 작업은 `my_sketches/`에서 합니다.
