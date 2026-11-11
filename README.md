# Cognitive Partner

**Version 1.0.0** — An Agent Skill for better work through active human–AI reasoning.

AI가 모든 판단을 완성한 뒤 사용자의 승인을 받는 대신, 직접적인 피드백으로 사용자의
가설, 예측, 대안, 검증 기준을 이끌어내고 실제 산출물에 반영하는 협업 지침입니다.

**1.0.0은 배포 버전입니다. 사고력 향상이나 실무 성과가 입증됐다는 뜻은 아닙니다.**
동작 규칙은 v0.2와 같으며, 평가 자료는 eval-r1의 수정 내용을 유지합니다.

## 사용 방식

```text
$cognitive-partner 내 요청과 현재 자료에서 중요한 전제나 놓친 관점을 직접 지적해줘.
내가 생각할 가치가 있는 지점 하나를 함께 검토하고, 내 판단을 실제 작업과 검증에 반영해줘.
```

막연한 퀴즈, 프롬프트 점수, 강제적인 찬반 토론을 만들지 않습니다. 이미 제시된 추론은
다시 묻지 않고 활용합니다. 단순 작업은 바로 수행하고, 긴급 대응을 훈련 때문에 늦추지 않습니다.

흐름은 **맥락 확인 → 직접 피드백 → 사용자 사고 → 근거와 대조 → 산출물 반영 → 결과 확인**입니다.
필요한 사실과 답을 숨기지 않으며, AI의 지적이 틀렸다면 수정합니다.

## 예시

합성 디버깅 자료에서 반복 횟수는 증가하지만 요청 전송 횟수는 0이라고 가정합니다.
사용자가 재연결을 늘리자고 하면, 에이전트는 연결 문제로 단정할 근거가 부족함을 설명합니다.
사용자가 전송 전 준비 조건을 의심하면 해당 가설을 분기 관측과 재현 실험에 반영합니다.
실제 관측이 가설과 다르면 양쪽의 판단을 수정합니다. 이 예시는 학습 효과의 증거가 아닙니다.

[다중 턴 예시](cognitive-partner/references/examples.md)와
[도움 수준 지침](cognitive-partner/references/intervention-guide.md)을 참고하세요.

## 설치

`cognitive-partner/` 폴더 전체가 설치 단위입니다. `evals/`는 실행 중 읽을 자료가 아닙니다.
[로컬 설치와 제거](docs/install.md)를 참고하세요. 이 패키지를 만드는 과정에서 설치는 수행하지 않았습니다.

## 로컬 검증

Python 3.10 이상에서:

```sh
python3 -m venv .venv
. .venv/bin/activate
python -m pip install -r requirements-dev.txt
python -B validate_package.py
python -B audit/test_validator_contract.py
```

두 검사는 LLM을 호출하지 않습니다. 파일, YAML, 평가 자료 계약, 고장 주입과 원본 지침의
보존 여부를 확인할 뿐, 실제 모델 동작이나 사람의 사고력 향상을 검증하지 않습니다.
28개 합성 사례는 이미 노출된 개발/회귀 자료이며 독립 holdout이 아닙니다.
[평가 계획](evals/PROTOCOL.md)과 [검증 범위](docs/verification.md)를 함께 보세요.

## 배포

저장소 후보는 `ChoMinGi/cognitive-partner`, 태그는 `v1.0.0`입니다.
[게시 절차](docs/publishing.md)와 [릴리스 노트](RELEASE_NOTES.md)를 제공합니다.
이 로컬 배포본이 준비됐다는 사실은 GitHub 업로드 완료를 의미하지 않습니다.

## 개인정보와 권한

Skill은 새 도구 권한, 저장 권한, 상시 실행 능력을 부여하지 않습니다.
실제 업무 자료, 계정 비밀, 개인 능력 프로필을 공개 저장소에 추가하지 마세요.
사용자의 동의 없이 전역 설정이나 지속 기억을 변경하지 않습니다.
배포본에서 공개 라이선스를 임의로 선택하지 않았습니다.
[LICENSE](LICENSE)는 소유자가 라이선스를 선택하기 전까지 이용 허락을 부여하지 않는다는 상태 표시입니다.
