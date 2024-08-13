# Python 가상 환경과 패키지 관리 Q&A

## 가상 환경 설정

**Q: env를 이용해서 가상환경을 설정하는 방법을 알려줘.**

A: Python에서 가상 환경을 설정하는 방법은 다음과 같습니다:

1. 가상 환경 생성:
   ```
   python -m venv 환경이름
   ```

2. 가상 환경 활성화:
   - Windows: `환경이름\Scripts\activate`
   - macOS/Linux: `source 환경이름/bin/activate`

3. 가상 환경 사용: 활성화 후 pip로 패키지 설치 및 Python 스크립트 실행

4. 가상 환경 비활성화: `deactivate`

**Q: 가상환경에 설치된 라이브러리를 어떻게 확인해?**

A: 가상환경을 활성화한 후, 다음 명령어를 사용할 수 있습니다:
- `pip list`: 설치된 모든 패키지와 버전 확인
- `pip freeze`: 설치된 패키지를 requirements.txt 형식으로 출력
- `pip freeze > requirements.txt`: 패키지 목록을 파일로 저장

**Q: poetry로 가상환경을 만들 때랑 venv로 가상환경을 만들 때랑 무슨 차이야? 장단점이 있어?**

A: venv와 Poetry의 주요 차이점과 장단점은 다음과 같습니다:

venv:
- 장점:
  1. 파이썬과 함께 제공됨 (별도 설치 불필요)
  2. 사용하기 쉬움
  3. 가벼움
- 단점:
  1. 패키지 관리가 조금 불편함
  2. 프로젝트 정보 관리가 어려움

Poetry:
- 장점:
  1. 패키지 관리가 쉬움
  2. 프로젝트 정보를 깔끔하게 관리
  3. 패키지 만들기와 공유하기가 쉬움
  4. 가상 환경을 자동으로 생성
- 단점:
  1. 별도 설치 필요
  2. 처음에는 배우기 어려울 수 있음
  3. 기존 방식과 달라 적응 필요

선택 방법:
- 간단한 프로젝트: venv
- 큰 프로젝트나 팀 작업: Poetry
- 패키지 제작 및 공유: Poetry
- 초보자: venv로 시작 후 Poetry로 전환

## Python 문법과 함수

**Q: split()은 어떤 라이브러리에서 나온 메서드야?**

A: `split()`은 Python의 내장 문자열(string) 메서드입니다. 별도의 라이브러리 import 없이 모든 문자열 객체에서 사용할 수 있습니다.

**Q: max(segments, key=len)에서 max에 입력하는 파라미터 값이 궁금해. key=len은 필수야? 어떤 의미야?**

A: `max()` 함수에서:
- `segments`: 최대값을 찾을 이터러블(예: 리스트)
- `key=len`: 선택적 인자로, 각 항목을 비교할 때 사용할 함수 지정
  - `len`은 객체의 길이를 반환하는 Python 내장 함수
  - `key=len`을 사용하면 각 항목의 길이를 기준으로 비교
  - 필수는 아니지만, 길이를 기준으로 최대값을 찾고자 할 때 사용

**Q: key에는 len 말고 어떤 값이 들어갈 수 있어?**

A: `key` 매개변수에는 다양한 함수나 람다식이 들어갈 수 있습니다:

1. 내장 함수: `abs`, `sum` 등
2. 람다 함수: `lambda x: x[-1]`
3. 사용자 정의 함수
4. 클래스의 메서드
5. 딕셔너리의 특정 키: `lambda s: s['grade']`
6. `operator` 모듈의 함수: `operator.itemgetter(1)`
7. `attrgetter`를 사용한 객체 속성

## Pandas와 데이터 처리

**Q: apply()에는 정의한 함수명만 넣으면 작동해? 함수의 매개변수는 따로 입력하지 않아도 돼?**

A: `apply()` 메서드의 기본 동작:
- 함수명만 넣으면 작동합니다.
- DataFrame의 각 행(또는 열)이 자동으로 함수의 인자로 전달됩니다.
- 추가 매개변수가 필요한 경우 lambda 함수를 사용하거나 `apply()`의 추가 인자를 활용할 수 있습니다.

예시:
```python
# 기본 사용
df['new_column'] = df['column'].apply(function_name)

# 추가 매개변수 사용
df['new_column'] = df['column'].apply(lambda x: function_name(x, extra_param=value))
# 또는
df['new_column'] = df['column'].apply(function_name, args=(extra_param,))
```