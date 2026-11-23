# 팀 저장소 규칙 — Claude Code는 아래 규칙을 지킨다

다이브 1기 NLP/LLM 프로젝트, 팀 bowers & wilikins (3인).

## 팀 구성
| 이름 | GitHub 아이디 | 역할 | 작업 폴더 | 브랜치 접두어 | PR 승인자 (`--reviewer`) |
|------|---------------|------|-----------|---------------|--------------------------|
| 조혁준 | nnujabes | 팀장 | members/hyukjun/ | hyukjun/ | 김병수 (yappang) |
| 정해찬 | Miita212 | 팀원 | members/haechan/ | haechan/ | 조혁준 (nnujabes) |
| 김병수 | yappang | 팀원 | members/byungsoo/ | byungsoo/ | 조혁준 (nnujabes) |

- 리뷰·승인 구조: 팀원(정해찬, 김병수)의 PR은 팀장 조혁준이 최종 승인한다.
  팀장 조혁준의 PR은 김병수가 승인한다. (자기 PR은 스스로 승인할 수 없다)
- 승인자가 아닌 팀원도 PR에 코멘트로 의견을 남길 수 있지만, 머지 조건은 위 승인자의 Approve 1개다.
- 공용 파일이 바뀌는 PR은 팀장(조혁준)이 반드시 함께 본다.

## 작업 범위
- 지금은 1단계(개인 폴더 단계)다. 사용자의 작업 폴더는 members/<이름>/ 하나뿐이다.
  사용자가 누구인지는 CLAUDE.local.md 를 따른다. 모르면 먼저 묻는다.
- 작업 폴더 밖의 파일은 만들거나 고치지 않는다. 필요하면 이유를 설명하고 허락을 받는다.
- 다른 팀원 폴더의 코드는 읽고 참고만 한다. 고칠 점은 PR 코멘트나 단톡으로 요청하도록 안내한다.
- 공용 파일(README.md, CLAUDE.md, .gitignore, .gitattributes, docs/interface.md, .github/)은
  사용자가 명시적으로 요청할 때만 고치고, 그 파일만 고친 PR을 따로 연다.

## Git 규칙
- main 에서 직접 커밋하거나 push 하지 않는다. 작업 전 `git switch main` → `git pull` 후
  `<이름>/<작업내용>` 브랜치(영문 소문자·하이픈)를 만든다. 예: haechan/slot-parser
- 커밋 전에 `git status` 로 바뀐 파일이 모두 작업 폴더 안인지 확인한다. 밖의 파일이 있으면 멈추고 알린다.
- git add 는 작업 폴더 경로를 지정해서 한다(`git add .` 대신 `git add members/<이름>`).
- 커밋 메시지는 "[이름] 한 일" 형식의 한국어로 쓴다. 예: `[haechan] 조건 슬롯 추출 프롬프트 v1 추가`.
  커밋 전에 메시지를 보여주고 확인받는다.
- `git push --force`, `git reset --hard`, `git clean`, 브랜치 삭제는 사용자의 명시적 허락 없이 실행하지 않는다.
- PR 은 `gh pr create --base main` 으로 만들고, 제목은 `[이름] 한 일`, 본문은
  .github/pull_request_template.md 양식을 채우며, 리뷰어는 위 표의 짝꿍으로 지정한다.
- 한 PR에는 한 가지 일만, 바뀐 줄은 200줄 이하를 권장한다.
- Approve 1개를 받기 전에는 머지하지 않는다. 머지는 Squash and merge 로만 한다.
- PR 승인(approve)은 Claude가 대신 하지 않는다. 사용자가 직접 판단한다.
- 충돌이 나면 멈추고, 어느 파일의 어느 부분이 왜 충돌했는지 양쪽 내용을 보여준 뒤 사용자가 고르게 한다.

## 올리면 안 되는 것
- .env, API 키, 비밀번호, 개인정보 (키는 .env 에 두고 python-dotenv 로 읽는다. .env.example 은 커밋 가능)
- 50MB 이상 파일, 원본 데이터, 모델 가중치(*.pt, *.pth, *.bin, *.safetensors, *.gguf, *.ckpt)
- 데이터는 공유 드라이브로 주고받고, 저장소에는 data/sample/ 의 작은 샘플만 둔다.

## 코드 습관
- 핵심 로직은 노트북이 아니라 .py 파일의 함수로 작성한다. 노트북은 실험용으로만.
- 함수의 이름·입력·출력은 members/<이름>/README.md 와 docs/interface.md 의 약속을 따른다.
- 경로를 하드코딩하지 않는다(C:\Users\... 금지, 상대 경로나 설정값 사용).
- 필요한 라이브러리는 members/<이름>/requirements.txt 에 적는다.
- 작은 샘플 입력·출력을 함께 둬서 누구나 바로 실행해 볼 수 있게 한다.
- 설명과 주석은 한국어로 쓴다. 파일은 UTF-8로 저장한다.

## 2단계(통합) 예정 구조 — 통합 시작 전까지는 만들지 않는다
```
app.py              화면 + 전체 흐름 연결
src/ingest.py       데이터 수집 · 전처리 · DB
src/retrieval.py    검색 · 필터 · 계산 · 판정
src/generation.py   프롬프트 · LLM 호출
src/evaluation.py   평가 지표 · 테스트셋 실행
prompts/  data/sample/  tests/  requirements.txt  .env.example
members/            1단계 실험 기록으로 남겨 둠 (지우지 않음)
```
- 통합 단계에서는 '한 사람 = 한 파일' 원칙. 각자 담당 파일만 고친다.
- 여러 명이 건드리는 app.py 와 requirements.txt 는 담당자(팀장)를 통해 고친다.
- 담당 파일 배정은 팀에서 정한 뒤 이 섹션과 CLAUDE.local.md 에 적는다.
