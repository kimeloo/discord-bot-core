# Discord Bot Core

Discord 봇 프레임워크 - 플러그인 방식으로 여러 앱을 동적으로 로드하여 실행합니다.

## 📋 구조

```
discord-bot-core/
├── apps/
│   ├── bot/              # 기본 봇 설정
│   ├── assistant/        # AI 어시스턴트 앱 (서브모듈)
│   ├── idea-thread/      # 아이디어 워크플로우 앱 (서브모듈)
│   ├── manage.py         # 앱 관리 및 동적 로딩
│   └── config.py         # 설정 관리
├── main.py               # 메인 진입점
└── README.md
```

## 🚀 설치 방법

### 1. 저장소 클론 (서브모듈 포함)

```bash
git clone --recurse-submodules https://github.com/kimeloo/discord-bot-core.git
cd discord-bot-core
```

기존 저장소를 이미 클론했다면:
```bash
git submodule update --init --recursive
```

### 2. 의존성 설치

```bash
pip install -r requirements.txt
```

### 3. 환경변수 설정

`.env` 파일을 생성하고 다음 내용을 추가:
```
DISCORD_BOT_TOKEN=your_bot_token_here
CHANNEL_DISCUSSION=your_channel_id_here
OPENAI_API_KEY=your_openai_key_here
OPENAI_ASSISTANT_ID=your_assistant_id_here
```

## 📦 포함된 앱

### 1. **assistant** (AI 어시스턴트)
- OpenAI Assistant API를 활용한 대화형 AI 봇
- **명령어**:
  - `!gpt` - 대화를 시작할 카테고리 설정
  - `!chat <주제>` - 주제로 스레드 생성 및 AI와 대화 시작
- 스레드 내에서 계속 대화 가능
- Streaming 방식으로 실시간 응답

### 2. **idea-thread** (아이디어 워크플로우)
- idea 채널의 메시지를 discussion 채널로 자동 승격
- **동작 방식**:
  - idea 채널에서 ✅ 이모지 반응 추가
  - discussion 채널에 자동으로 스레드 생성
  - 7일 후 자동 보관
- **명령어**:
  - `!ping` - 봇 동작 확인

## 🔧 새 앱 추가하기

1. 새 앱을 서브모듈로 추가:
```bash
git submodule add <repository-url> apps/<app-name>
```

2. 앱 디렉토리에 `main.py` 파일 생성:
```python
def run(bot):
    # 봇 설정 및 이벤트/명령어 추가
    return bot
```

3. 봇 재시작 - 자동으로 감지되어 로드됩니다!

## 🛠 요구사항

- Python >= 3.9
- requests==2.32.3
- discord==2.3.2
- python-dotenv==1.0.1
- openai (assistant 앱 사용 시)

## 📚 참고자료

- [discord.py 한국어 문서](https://discordpy-ko.github.io/api.html)

## 📝 라이선스

[LICENSE](LICENSE) 파일 참조
