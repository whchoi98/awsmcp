# LAB 03. Kiro CLI

***

## 01. Kiro CLI 탐색(Exploring Kiro CLI)

이 실습에서는 Kiro CLI의 에이전트(Agentic) 기능을 본격적으로 탐색합니다.

본 실습은 모든 사전 요구 사항(prerequisites)을 충족하고 Kiro CLI 설치가 완료된 상태를 전제로 진행됩니다.

***

### 1.1 인터랙티브(Agentic) Chat 소개

Kiro CLI를 실행하면 터미널에서 AI와 자연스럽게 대화할 수 있는 대화형(interactive) Chat 모드가 활성화됩니다.

이 기능은 “AI 기반 개발 지원(Agentic Development)” 기능을 터미널로 가져와, 사용자의 워크플로우를 자연어 기반으로 확장할 수 있게 합니다.

또한 Kiro CLI는 영어뿐 아니라 여러 언어를 지원하며, 한국어로도 자연스러운 개발 대화를 수행할 수 있습니다.

***

### Task-01 — Kiro CLI 실행하기

1. 새로운 프로젝트 디렉터리를 생성합니다. 아래 예시는 사용자 홈 디렉터리에서 진행하는 예시이며 원하는 위치에서 생성해도 무방합니다:

```
cd
mkdir kiro-cli-workshop && cd kiro-cli-workshop
kiro-cli
```

2.  Kiro CLI가 실행되면 다음과 같은 “>” 프롬프트가 나타납니다. 이 프롬프트는 현재 대화 상태 또는 도구 신뢰 레벨 등을 시각적으로 알려주는 역할도 합니다.

    예:

    * \> : 기본 상태
    * !> : 모든 도구가 trusted 상태
3. 이제 아래 문장을 입력해 봅니다:

```
들여쓰기할 때 탭과 스페이스 중 어떤 것을 선호하나요?
```

4. 출력 결과를 확인하고, 프롬프트를 다시 관찰합니다.
5. Kiro CLI 종료:
   * /q 입력
   * 또는 Ctrl + C

```
/q
```

6. 이번에는 아래 방식으로 단일 프롬프트 채팅 모드를 실행합니다:

```
kiro-cli chat "들여쓰기할 때 탭과 스페이스 중 어떤 것을 선호하나요?"
```

→ 출력은 다를 수 있으나, 동일한 동작을 수행합니다.

> 다음 실습에서 계속 사용하므로 이 세션을 종료하지 말고 유지하세요.

***

### 1.2 Kiro CLI 내에서 도움말 확인하기

언제든지 /help를 입력하여 Kiro CLI의 모든 명령 및 사용법을 조회할 수 있습니다.

***

### 1.3 Kiro CLI 명령(Command) 구조

Kiro CLI의 명령은 모두 `/` 로 시작합니다.

예시: `/help`, `/reply`, `/editor`, `/model`, `/context show` 등

* `/help` : 모든 명령 목록 보기
* `Ctrl + S` : 명령어 퍼지 검색(Fuzzy Search)
  * 입력하면 명령 목록이 필터링되며
  * 원하는 명령을 선택하거나 ESC로 종료 가능

***

## 02. 멀티라인 프롬프트(Multi-line Prompts)

\
지금까지는 단일 줄(single-line) 프롬프트를 입력해 보았습니다.

하지만 실제 개발 작업에서는 여러 줄로 구성된 요구사항, 코드 템플릿, 기술 지침 등을 전달해야 하는 경우가 많습니다.

Kiro CLI는 이러한 상황을 위해 다양한 방식의 멀티라인(Multi-line) 입력 모드를 지원합니다.

***

멀티라인 입력 방식 1: `Ctrl + J`

Kiro CLI의 Chat 세션에서 Ctrl + J(또는 Ctrl + Enter)를 누르면 프롬프트 내에서 줄바꿈(newline) 이 삽입됩니다.

예:

```
Python 코드를 작성할 때에는 다음의 지침을 따르십시오.
	•	웹 프레임워크(web framework)로 Flask를 사용하십시오.
	•	Flask 애플리케이션 팩토리 패턴(application factory pattern)을 준수하십시오.
	•	구성(configuration)에는 환경 변수(environment variables)를 사용하십시오.
	•	데이터베이스 작업(database operations)을 위해 Flask-SQLAlchemy를 구현하십시오.
```

***

멀티라인 입력 방식 2:  `\` (백슬래시) 사용

명령 줄 끝에 백슬래시 \ 를 입력하면, 다음 줄로 자연스럽게 이어서 작성할 수 있습니다.

예:

```
Python 코드를 작성할 때에는 다음의 지침을 따르십시오. \
	•	웹 프레임워크(web framework)로 Flask를 사용하십시오. \
	•	Flask 애플리케이션 팩토리 패턴(application factory pattern)을 준수하십시오. \
	•	구성(configuration)에는 환경 변수(environment variables)를 사용하십시오. \
	•	데이터베이스 작업(database operations)을 위해 Flask-SQLAlchemy를 구현하십시오.
```

이 방식은 shell 환경에 익숙한 사용자들이 자주 사용하는 패턴입니다.

***

### Task-02 — 두 가지 방식으로 멀티라인 입력해보기

Kiro CLI Chat 세션에서 아래 내용을 두 방식 모두 사용해 입력해 보세요.

입력할 멀티라인 텍스트:

```
Python 코드를 작성할 때에는 다음의 지침을 따르십시오.
	•	웹 프레임워크(web framework)로 Flask를 사용하십시오.
	•	Flask 애플리케이션 팩토리 패턴(application factory pattern)을 준수하십시오.
	•	구성(configuration)에는 환경 변수(environment variables)를 사용하십시오.
	•	데이터베이스 작업(database operations)을 위해 Flask-SQLAlchemy를 구현하십시오.
```

권장 실습:

1. Ctrl + J 방식으로 입력
2. 줄 끝에 \ 추가하는 방식으로 입력

두 방식 모두 동일하게 멀티라인 프롬프트로 처리됩니다.

***

#### 참고: 멀티라인 입력이 필요한 상황

다음과 같은 경우 멀티라인 프롬프트가 특히 유용합니다:

* API 명세서 전체 전달
* SQL 스키마 또는 데이터 모델 정의
* Python/JavaScript 코드 블록 전달
* 긴 요구사항 또는 단계별 지시사항 입력
* 문서 생성 요청 시 구조화된 내용 제공

그러나 멀티라인 프롬프트도 추후 `/editor` 기능을 사용하면 훨씬 편리하게 다룰 수 있습니다.

***

## 03. 선호하는 텍스트 에디터 설정하기

Kiro CLI에서는 복잡한 멀티라인 프롬프트를 더 편리하게 작성하기 위해 외부 텍스트 에디터와 연동할 수 있습니다.

이는 개발자가 이미 익숙한 편집 환경을 그대로 활용할 수 있게 해주며, 긴 지침·코드·설계 문서를 입력해야 할 때 특히 효율적입니다.

***

### 3.1 기본 동작

기본적으로 Kiro CLI는 시스템에서 설정된 기본 에디터(예: vim, nano)를 사용합니다.

그러나 사용자가 원하는 에디터를 직접 지정할 수 있으며, 이를 위해 환경변수 EDITOR 를 설정합니다.

### &#x20;3.2 에디터 지정 방법

아래 명령을 터미널에서 실행하면 해당 에디터가 Kiro CLI의 기본 편집기로 사용됩니다.

예시: vim  사용

```
export EDITOR=vim
```

예시: VS Code 사용

```
export EDITOR="code -w"
```

* `-w` 옵션은 파일을 닫을 때까지 CLI가 기다리도록 하는 설정입니다.

예시: nano  사용

```
export EDITOR=nano
```

환경 변수를 설정한 후 Kiro CLI를 실행하면 /editor 명령을 통해 해당 에디터를 사용할 수 있습니다.

***

### 3.3 /editor 명령을 사용한 프롬프트 편집

Kiro CLI 실행 후 `>` 프롬프트에서 아래를 입력하면 설정된 에디터가 열립니다.

```
/editor
```

에디터에서 원하는 멀티라인 프롬프트를 작성하고 저장 후 종료하면, 해당 내용이 Chat 입력으로 처리되며 즉시 응답이 생성됩니다.

***

### Task-03 — 선호하는 에디터 설정 및 사용

1. 현재 Kiro CLI 세션을 종료합니다.
2. 터미널에서 EDITOR 환경변수를 본인이 선호하는 에디터로 설정합니다.

예시:

```
export EDITOR=vi
export EDITOR="code -w"
export EDITOR="nano"
```

3. 다시 Kiro CLI를 실행하고, `>` 프롬프트에서 아래 명령을 입력합니다:

```
/editor
```

4. 에디터가 열리면 아무 멀티라인 텍스트를 작성해 저장·종료합니다.
5. Kiro CLI가 편집된 입력을 받아 프롬프트를 실행하는 것을 확인합니다.

***

### 3.4  왜 에디터 연동이 중요한가?

긴 프롬프트나 구조화된 입력을 자주 사용하는 개발 워크플로우에서 다음과 같은 장점이 있습니다.

* 로컬 편집기에서 문법 강조(syntax highlighting)를 활용 가능
* 복잡한 코드 블록을 안정적으로 작성
* 장문의 기술 지침을 가독성 좋게 편집
* 자연스러운 버전 관리 및 로컬 파일 활용

앞서 살펴본 멀티라인 기능보다 훨씬 강력하고 실전적입니다.

***

## 05. Reply 기능 사용하기

Kiro CLI에서 `/reply` 명령은 직전 Assistant 응답을 기반으로 후속 메시지를 작성할 때 매우 유용합니다.

특히 긴 답변을 부분 수정하거나, 특정 내용을 인용해 추가 지시를 내릴 때 큰 효율을 제공합니다.

`/reply` 명령을 실행하면 설정된 텍스트 에디터가 열리며, 그 안에 가장 최근 Assistant 메시지가 자동으로 인용 형태로 포함됩니다.

사용자는 해당 내용을 편집하거나 그 아래에 새로운 지시사항을 덧붙인 뒤 저장·종료하면 됩니다.

### &#x20;5.1 Reply 기능 동작 방식

1. Kiro CLI가 직전에 출력한 AI 응답을 감지
2. /reply 실행 시 에디터가 열림
3. 에디터 내부에는 최근 Assistant 메시지가 자동으로 포함됨
4. 사용자는 이를 수정하거나 이어서 작성
5. 저장 후 종료하면 해당 내용이 새로운 사용자 메시지로 전달됨

이는 Slack, GitHub PR 리뷰, 이메일 스레드 등에서 인용(reply) 작성 방식과 유사해 개발자에게 익숙한 경험을 제공합니다.

***

### Task-04 — Reply 기능 실습

#### 1. 먼저 Kiro CLI에서 예시 프롬프트를 입력합니다:

```
JSON 날짜(Date) 데이터를 반환하는 코드를 보여줘.
```

#### 2. Assistant의 응답이 출력되면, 다음 명령을 입력합니다:

```
/reply
```

#### 3. 설정된 에디터가 열리며 아래와 같은 형태를 보게 됩니다(예시):

````
> JSON에서 날짜를 반환하는 간단한 예제입니다:
> 
> **JavaScript/Node.js:**
> ```javascript
> const data = {
>   timestamp: new Date().toISOString(),
>   date: new Date().toISOString().split('T')[0]
> };
> 
> console.log(JSON.stringify(data));
> // {"timestamp":"2025-12-07T05:49:34.328Z","date":"2025-12-07"}
> ```
> 
> **Python:**
> ```python
> import json
> from datetime import datetime
> 
> data = {
>     "timestamp": datetime.now().isoformat(),
>     "date": datetime.now().date().isoformat()
> }
> 
> print(json.dumps(data))
> # {"timestamp": "2025-12-07T05:49:34.328000", "date": "2025-12-07"}
> ```
> 
> **Java:**
> ```java
> import com.fasterxml.jackson.databind.ObjectMapper;
> import java.time.LocalDateTime;
> import java.util.Map;
> 
> ObjectMapper mapper = new ObjectMapper();
> Map<String, String> data = Map.of(
>     "timestamp", LocalDateTime.now().toString(),
>     "date", LocalDateTime.now().toLocalDate().toString()
> );
> 
> String json = mapper.writeValueAsString(data);
> ```
> 
> JSON은 네이티브 Date 타입이 없어서 ISO 8601 형식 문자열(`YYYY-MM-DDTHH:mm:ss.sssZ`)을 사용하는 게 표준입니다.
> [Tool uses: none]
````

4\. 원하는 내용을 편집한 후 저장 및 종료합니다.

5\. CLI가 자동으로 편집된 내용을 새로운 메시지로 처리하고 AI가 후속 응답을 제공합니다.

***

### 5.2 /reply  기능의 활용 사례

| 활용 상황                | 설명                                 |
| -------------------- | ---------------------------------- |
| 이전 답변을 일부 수정하고 싶을 때  | 생성된 코드 중 특정 함수만 변경 요청 등            |
| 긴 답변에 추가 지시를 하고 싶을 때 | “여기에 로그 추가해줘”, “이 부분을 async로 변경해줘” |
| 문서·아키텍처 초안 재작성       | 기존 제안에 수정 댓글 다는 방식으로 편하게 작성        |
| 비교·대조 요청             | “이전 코드와 비교해서 더 최적화된 버전으로 만들어줘”     |

***

### 5.3 Reply 기능의 장점

* 긴 컨텍스트를 복사·붙여넣기 할 필요 없음
* 원본 응답이 자동 포함되어 수정 근거가 명확
* 에디터 기반이므로 멀티라인 편집에 최적화
* 이후 커맨드 히스토리 관리가 용이

***

좋습니다! 이어서 섹션 6 — Using Images as Part of Your Prompt 를 GitBook 스타일의 고급 비즈니스 한국어로 정제하여 제공합니다.

원문 표현과 의미는 최대한 유지했습니다.

***

## 06. 이미지 기반 프롬프트 활용하기

Kiro CLI는 이미지를 프롬프트의 일부로 활용할 수 있도록 지원합니다.

이는 아키텍처 다이어그램, ERD(Entity Relationship Diagram), 디자인 시안, UI 스케치 등 비정형 시각 자료에서 정보를 추출해 코드·설계·문서화를 생성할 때 특히 강력합니다.

이미지는 다음 두 방식으로 CLI에 전달할 수 있습니다.

1. 파일 경로를 통한 이미지 참조
2. 클립보드 이미지 붙여넣기(/paste)

***

### 6.1  이미지 파일을 이용한 프롬프트 작성

Kiro CLI에 이미지 파일을 전달할 때는 프로젝트 디렉터리에 존재하는 이미지 파일을 이름으로 지정하면 됩니다.

예시:

```
data-model 디렉터리의 example-erd.png 다이어그램을 기반으로, Python에서 사용할 샘플 데이터 모델(sample data model)을 생성하세요.
```

Kiro CLI는 다음을 수행합니다:

* 이미지 파일 읽기
* 도형, 테이블, 연결 관계 등을 분석
* Python 기반 데이터 모델(예: SQLAlchemy) 생성 또는 설계 초안 반환

이미지를 기반으로 한 구조적 정보 분석은 데이터 모델링, 백엔드 스키마 설계, CI/CD 아키텍처 구축 등 다양한 영역에 활용 가능합니다.

***

### Task-05 — 이미지 파일 기반 프롬프트 실습

1. example-erd.png 파일을 가져오고, 아래 디렉토리를 생성해서 업로드 합니다.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

2. 로컬 프로젝트에서 다음과 같은 디렉토리를 생성합니다.

```
```

3. mkdir \~/sample\_projectKiro CLI를 실행하고 아래 프롬프트를 입력합니다:

```
~/.kiro example-erd.png 다이어그램을 기반으로, Python에서 사용할 샘플 데이터 모델(sample data model)을 생성하세요.
```

4.  출력 결과를 검토합니다.

    이미지에서 엔티티, 관계, 속성 등을 추출하여 Python 모델을 자동 생성하는 것을 확인할 수 있습니다.

***

### ▶&#x20;

### /paste

### &#x20;명령을 활용한 이미지 붙여넣기

<br>

CLI 세션에서 이미지 파일 없이도

클립보드에 복사된 이미지 자체를 바로 Kiro CLI로 전달할 수 있습니다.

<br>

#### 실습 절차:

1. 로컬 이미지 뷰어에서 원하는 이미지를 열고 “복사(Copy)” 합니다.
2. Kiro CLI 프롬프트에서 다음 명령을 실행합니다:

```
/paste
```

3. CLI는 임시 파일을 생성하고 다음과 같은 메시지를 출력합니다:

```
Reading images: /tmp/.tmpFeCK60.png
(using tool: read)
Allow this action? Use 't' to trust (always allow) this tool for the session. [y/n/t]:
```

4.  이미지 읽기 권한 요청이 나오면 y 또는 t 로 승인합니다.

    이후 Kiro CLI가 이미지의 시각적 요소를 분석하여 작업을 수행합니다.

***

### ▶&#x20;

### /paste

### &#x20;기능의 활용 사례

| 사례                            | 설명                                |
| ----------------------------- | --------------------------------- |
| ERD·DB 스키마 자동 생성              | 관계형 데이터 모델 설계 자동화                 |
| 아키텍처 다이어그램 → IaC 코드           | AWS CDK, Terraform 등 초기 템플릿 생성 가능 |
| UI 스케치 → HTML/CSS/React 코드 초안 | 프로토타입 구현에 도움                      |
| 화이트보드 사진 → 구조적 문서화            | 회의 메모 정리 자동화                      |

***

### ⚠ 이미지 처리 시 주의사항

* 이미지 해상도가 너무 낮으면 분석 정확도가 떨어질 수 있음
* 복잡한 ERD나 흐름도는 단계별로 나누어 전달하는 것이 더 효과적
* CLI 내에서 이미지 처리를 위해 read Tool 권한이 필요

***

## ✔ 섹션 6 완료

<br>

다음은 섹션 7 — Exiting and Resuming Conversations (대화 종료 및 재개) 를 이어서 작성해드릴까요?
