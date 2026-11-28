---
name: i2r
description: i2r 제품을 프로그램하거나 개발 환경을 만들 때 쓴다. i2r 제품은 IoT PLC 보드 i2r-02/03/04, Otto I2R 로봇(i2r-05 보드), i2r 서버와 시뮬레이터, AI 챗봇(i2r-05 + i2r-shield-03)이다. 사용자가 "i2r 개발을 도와줘", "otto 개발을 도와줘", "plc 개발을 도와줘", "서버 개발을 도와줘", "시뮬레이터 켜 줘", "챗봇 개발을 도와줘", i2r, i2r-plc, 오토 로봇, I2R_PLC, I2R_IoT, OttoI2R을 말하면 이 스킬을 쓴다.
---

# i2r 개발 도우미

1. **먼저 최신 안내판을 읽고 그대로 따른다**: https://raw.githubusercontent.com/kdi6033/i2r/main/AGENTS.md
   - 명령을 실행할 수 있으면 `curl -sL <주소>`로 원문 전체를 읽는다(요약하지 말 것).
   - 안내판이 저장소 지도, 채팅과 Claude Code에서 하는 일, 안전 규칙을 정한다.
2. 사용자가 연 폴더가 작업 폴더다. 키트는 그 안에 바로 받고, `i2r-github` 같은 새 폴더를 만들지 않는다(안내판 4.1). 작업 폴더에 이미 `i2r-plc/`, `otto/`, `i2r-server/`, `i2r-05/`가 있으면 다시 받지 말고, 그 폴더의 CLAUDE.md를 읽고 바로 작업한다.
3. 사용자는 초보자다. 한국어로 짧고 쉽게 말한다.
4. 받을 키트를 말하지 않았으면("i2r 개발을 도와줘"만) 안내판 1.1장 질문을 그대로 한 번 묻는다: "1. 모두 다 (PLC + Otto 로봇 + 시뮬레이터·서버 + AI 챗봇) ← 추천 / 2. 골라서 받기". "모두", "전부"라고 했으면 묻지 않고 넷 다 받는다.
5. 그냥 "plc"라고만 하고 다른 회사 PLC(지멘스, LS 등)일 수도 있으면 "i2r PLC(i2r-02/03/04)인가요?"라고 한 번 묻는다.

## 안내판을 읽을 수 없을 때

| 말 | 저장소 | AI용 안내서 |
|---|---|---|
| plc, i2r-02/03/04 | https://github.com/kdi6033/i2r-plc | https://raw.githubusercontent.com/kdi6033/i2r-plc/main/AGENTS.md |
| otto, 오토 로봇 | https://github.com/kdi6033/otto | https://raw.githubusercontent.com/kdi6033/otto/main/AGENTS.md |
| 서버, 시뮬레이터 | https://github.com/kdi6033/i2r-server | 저장소의 CLAUDE.md |
| 챗봇, LLM, i2r-shield-03 | https://github.com/kdi6033/i2r-05 (`--depth 1`, 예제는 examples/) | https://raw.githubusercontent.com/kdi6033/i2r-05/main/docs/chatbot.md |

- Claude Code라면 고른 저장소를 연 폴더 안에 바로 `git clone`하고, 그 안의 CLAUDE.md를 읽고 "처음 한 번 환경 만들기"를 한다.
- 채팅이라면 안내서를 읽고 전체 코드를 주어 사용자가 Arduino IDE로 올리게 한다.
- 릴레이와 모터가 연결될 수 있으니 업로드 전에 무엇이 연결되어 있는지 묻는다. i2r-02/04 입력에는 전압을 넣으라고 하지 않는다.
