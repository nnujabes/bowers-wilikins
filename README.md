# bowers-wilikins

다이브 1기 NLP/LLM 프로젝트 — 팀 bowers & wilikins

## 팀원
| 이름 | GitHub | 역할 | 폴더 | PR 승인자 |
|------|--------|------|------|-----------|
| 조혁준 | [@nnujabes](https://github.com/nnujabes) | 팀장 | `members/hyukjun/` | 김병수 (`yappang`) |
| 정해찬 | [@Miita212](https://github.com/Miita212) | 팀원 | `members/haechan/` | 조혁준 (`nnujabes`) |
| 김병수 | [@yappang](https://github.com/yappang) | 팀원 | `members/byungsoo/` | 조혁준 (`nnujabes`) |

> 팀원 PR은 팀장(조혁준)이 최종 승인, 팀장 PR은 김병수가 승인합니다.

## 저장소 구조 (1단계 · 한 사람 = 한 폴더)
```
bowers-wilikins/
├─ README.md                      팀 소개 · 규칙 · 실행 방법 (팀장 관리)
├─ CLAUDE.md                      Claude Code가 지킬 팀 규칙
├─ .gitignore                     올리면 안 되는 파일 목록
├─ .gitattributes                 Windows↔Linux 줄바꿈 통일
├─ .github/pull_request_template.md   PR 작성 양식
├─ docs/interface.md              함수 · 데이터 형식 약속 (통합용)
└─ members/
   ├─ hyukjun/   ← 조혁준만 수정
   ├─ haechan/   ← 정해찬만 수정
   └─ byungsoo/  ← 김병수만 수정
```

## 처음 한 번 (팀원)
```powershell
mkdir $HOME\dev; cd $HOME\dev
git clone https://github.com/nnujabes/bowers-wilikins.git
cd bowers-wilikins
claude
```
그다음 Claude Code에게 저장소 루트에 `CLAUDE.local.md` 를 만들어 달라고 하세요(내 이름·폴더·브랜치 접두어·리뷰어). 이 파일은 GitHub에 올라가지 않아요.

## 매일의 작업 흐름
```powershell
git switch main; git pull                    # ① main 최신화
git switch -c 내이름/작업내용                  # ② 브랜치
# ③ members/내이름/ 안에서만 작업
git status                                    # ④ 내 폴더만 바뀌었는지 확인
git add members/내이름                         # ⑤ 커밋
git commit -m "[내이름] 한 일"
git push -u origin 내이름/작업내용              # ⑥ 푸시 (두 번째부터는 git push)
gh pr create --base main --fill --reviewer 짝꿍아이디   # ⑦ PR → 짝꿍 Approve
# ⑧ Squash and merge 후 정리
git switch main; git pull --prune; git branch -D 내이름/작업내용
```

## 7가지 약속
1. 내 폴더(`members/내이름/`)만 고친다
2. main에 직접 push하지 않는다 (브랜치 → PR → 리뷰 → 머지)
3. 시작 전엔 `git pull`
4. 작게, 자주 PR (하루 1~2개, 200줄 이하)
5. 공용 파일(README.md, CLAUDE.md, .gitignore, .gitattributes, docs/interface.md)은 팀장을 통해
6. 비밀(.env, API 키)과 대용량(데이터, 모델 가중치)은 올리지 않는다
7. `git push --force`, `git reset --hard`, `git clean` 은 쓰지 않는다
