# Beginner_Project

코드잇 AI 15기 팀 프로젝트와 Git 협업 연습 저장소입니다.

## 실행 환경: Google Colab

팀 노트북은 Google Colab의 호스팅 런타임에서 실행합니다. 각자 PC의 Python·uv 가상환경을 Colab 커널로 사용하는 방식은 아닙니다.

2026-10-21 Google Colab 기본 CPU 런타임에서 아래 환경을 직접 확인했습니다.

| 항목 | 확인한 버전 |
|---|---|
| Python | 3.13.16 |
| torch | 2.11.0+cpu |
| torchvision | 0.26.0+cpu |
| Pillow | 11.3.0 |
| numpy | 2.1.3 |
| pandas | 2.2.3 |
| scikit-learn | 1.6.1 |
| matplotlib | 3.10.0 |
| tqdm | 4.67.3 |

8개 패키지 import, 이미지→텐서 변환, 작은 선형 모델의 예측·손실 계산·역전파, F1 계산, DataFrame 생성·진행률 표시를 확인했습니다. 실제 프로젝트 데이터 학습과 GPU 실행은 아직 확인하지 않았습니다. 이 런타임은 CUDA 없음·GPU 사용 불가 상태였습니다.

requirements에는 직접 확인한 버전을 기록했습니다. torch·torchvision은 GPU 런타임에서도 사용할 수 있도록 CPU 전용 접미사 `+cpu`를 제외한 공개 버전을 적었습니다. 따라서 이 파일만으로 CPU/GPU 빌드까지 동일해지는 것은 아닙니다. GPU 학습 시에는 해당 런타임의 두 패키지와 CUDA 조합을 별도로 확인합니다.

## 1. 노트북 열기

1. [Google Colab](https://colab.research.google.com/)에 접속합니다.
2. GitHub에서 열기를 선택하고 `https://github.com/yy-0401/Beginner_Project`를 검색합니다.
3. 작업할 개인 브랜치를 선택하고 노트북을 엽니다. 저장소가 검색되지 않으면 노트북 파일을 내려받아 Colab에 업로드합니다.
4. 모델 학습에 GPU가 필요하면 런타임 설정에서 GPU를 선택합니다. 할당 여부는 Colab 사용 상태에 따라 달라집니다.

## 2. 첫 셀에서 환경 확인하기

```python
import sys
import importlib.metadata as metadata

print("Python:", sys.version)
packages = ["torch", "torchvision", "Pillow", "numpy", "pandas",
            "scikit-learn", "matplotlib", "tqdm"]
for name in packages:
    try:
        print(name, metadata.version(name))
    except metadata.PackageNotFoundError:
        print(name, "미설치")

import torch
print("GPU 사용 가능:", torch.cuda.is_available())
print("PyTorch CUDA:", torch.version.cuda)
```

이 출력과 선택한 런타임을 팀에 공유합니다. 위 검증 환경과 비교하고, 다른 버전에서 문제가 생기면 실행 환경과 오류를 함께 공유합니다.

## 3. 필요한 패키지 설치하기

Colab에는 여러 라이브러리가 미리 설치돼 있습니다. 먼저 위 셀로 확인하고 부족한 패키지만 설치합니다.

```python
# 예: scikit-learn이 미설치인 경우
%pip install scikit-learn
```

버전을 맞춰야 할 경우 requirements 파일을 Colab에 업로드하고 다음처럼 설치할 수 있습니다. 이번 검증은 기본 설치 패키지를 사용했으며 이 명령으로 재설치하는 과정까지 검증한 것은 아닙니다.

```python
%pip install -r /content/requirements.txt
```

기본 환경이 위 버전과 같다면 재설치할 필요가 없습니다. torch·torchvision을 임의 업그레이드하지 않습니다. 변경이 필요하면 두 패키지와 CUDA 조합을 함께 확인합니다. 설치 후 런타임 재시작 안내가 나오면 재시작하고 위에서부터 다시 실행합니다.

| 패키지 | 사용할 곳 |
|---|---|
| torch | 모델 학습·예측 |
| torchvision | 이미지 전처리·증강·사전학습 모델 |
| Pillow | 이미지 열기·변환 |
| numpy | 배열·수치 계산 |
| pandas | 알약 정보·라벨 CSV 정리 |
| scikit-learn | 데이터 분할·F1·혼동행렬 |
| matplotlib | 이미지·학습 그래프 |
| tqdm | 진행률 표시 |

`ipykernel`은 로컬 VS Code 가상환경 연결용으로, 이번 Colab 설치 목록에서는 제외했습니다. W&B를 사용하게 되면 `wandb` 설치·연동을 확인하고 목록에 추가합니다. API 키는 노트북 출력이나 Git에 남기지 않습니다.

## 4. 저장하고 PR 만들기

1. Colab에서 수정·실행한 노트북을 저장합니다. 런타임이 종료돼도 필요한 코드·결과가 남도록 파일 저장 여부를 확인합니다.
2. GitHub에 저장할 때는 `practice/본인이름` 브랜치를 선택합니다. `main`에 바로 저장하지 않습니다.
3. GitHub 저장이 어려우면 `.ipynb`를 내려받아 로컬 개인 브랜치에서 커밋·push합니다.
4. 개인 브랜치 → `main` 방향으로 PR을 만들고 바꾼 내용·실행 환경·실행 결과를 적습니다.
5. 다른 팀원이 확인한 뒤 합칩니다. 같은 노트북을 동시에 수정하기 전에 담당을 정합니다.

비밀번호·API 키·개인정보·대용량 데이터·모델 가중치가 노트북 출력에 포함돼 있지 않은지 업로드 전에 확인합니다. 충돌 표시가 남은 파일은 합치지 않습니다.

## 로컬 uv와의 관계

Git 파일 작업이나 로컬에서 별도 실험할 때는 uv를 사용할 수 있습니다. 하지만 로컬 uv 설치가 Colab 서버의 실행 환경을 자동으로 맞춰주지는 않습니다. 팀 공통 실행 검증은 Colab에서 진행합니다.

`requirements.example.txt`는 초기 작성법 예시이며 실제 팀 목록은 `requirements.txt`를 사용합니다.

## 참고

- [Colab 런타임 버전 안내](https://research.google.com/colaboratory/runtime-version-faq.html)
- [Colab 자주 묻는 질문](https://research.google.com/colaboratory/faq.html)
