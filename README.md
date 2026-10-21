# Beginner_Project

코드잇 AI 15기 팀 프로젝트와 Git 협업 연습 저장소입니다.

## 처음 시작하기

```bash
git clone https://github.com/yy-0401/Beginner_Project.git
cd Beginner_Project
```

이미 개인 브랜치가 있다면 해당 브랜치로 이동합니다.

```bash
git fetch origin
git switch practice/본인이름
```

개인 브랜치가 없다면 최신 main에서 만듭니다.

```bash
git switch main
git pull --ff-only origin main
git switch -c practice/본인이름
```

`본인이름`은 자신의 브랜치 이름으로 바꿉니다. 예: `practice/soonwoo`.

## 파이썬 환경 만들기

팀에서 사용하는 환경 관리 도구는 uv입니다. [공식 설치 안내](https://docs.astral.sh/uv/getting-started/installation/)에 따라 uv를 설치합니다. Python 버전은 팀에서 정한 버전을 사용하며, 확정 후 여기에 기록합니다.

현재는 `requirements.txt` 방식으로 라이브러리를 관리합니다. `pyproject.toml`과 `uv.lock`을 사용하는 방식으로 전환할 때는 팀과 먼저 합의합니다.

macOS / Linux:

```bash
uv venv
source .venv/bin/activate
uv pip install -r requirements.txt
```

Windows PowerShell:

```powershell
uv venv
.\.venv\Scripts\Activate.ps1
uv pip install -r requirements.txt
```

현재 출력 연습 코드는 추가 라이브러리 없이 실행할 수 있습니다.

```bash
python 1.py
```

새 라이브러리를 사용하게 되면 팀과 버전을 확인해 `requirements.txt`에 추가합니다.

## 작업한 내용 공유하기

```bash
git status
git add 수정한파일명
git commit -m "수정한 내용 설명"
git push -u origin practice/본인이름
```

GitHub에서 내 브랜치 → `main` 방향으로 PR을 만듭니다. 바꾼 내용과 실행 결과를 적고, 함께 검토한 뒤 합칩니다. 내 PR은 다른 사람이 확인합니다.

- 같은 노트북을 수정하기 전에 담당을 정합니다.
- 충돌 표시(`<<<<<<<`, `=======`, `>>>>>>>`)가 남은 파일은 합치지 않습니다.
- 비밀번호·API 키·개인 환경 폴더는 올리지 않습니다.

## requirements 작성 예시

`requirements.example.txt`는 NumPy(숫자 계산), pandas(표 데이터), Matplotlib(그래프)를 나열한 학습용 예시입니다. 현재 팀 코드의 필수 패키지나 확정 버전 목록은 아닙니다.

```text
numpy
pandas
matplotlib
```

버전을 생략하면 설치 시점과 Python 환경에 따라 선택되는 버전이 달라질 수 있습니다. 팀이 실제로 함께 실행해 확인한 뒤 `패키지이름==버전번호` 형태로 `requirements.txt`에 적습니다. `uv pip freeze` 출력은 참고할 수 있지만 개인 환경의 불필요한 패키지까지 그대로 공유하지 않습니다.
