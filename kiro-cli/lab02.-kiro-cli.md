---
description: 'Update : 2025.12.06'
---

# LAB02. Kiro CLI 고급 구성

## Advanced Configuration of Kiro CLI

본 섹션은 선택(Optional) 항목으로, Kiro CLI의 내부 구조와 설정 방식을 보다 깊이 이해하고자 하는 사용자에게 제공됩니다. 기본 실습을 빠르게 진행하고자 한다면 본 섹션은 건너뛰어도 무방합니다.

***

## 1. Kiro CLI 구성 심층 탐색

_Exploring Kiro CLI Configuration_

Kiro CLI는 전역 설정(Global Configuration)과 프로젝트 기반 로컬 설정(Project-scoped Configuration)을 모두 지원하며, 이를 통해 사용자는 CLI의 행동과 모델 설정을 세밀하게 조정할 수 있습니다.

***

## 2. 디렉터리 구조 이해하기

Directory Structure Overview

Kiro CLI는 설정 파일을 다음 두 위치에서 관리합니다.

***

### 2.1 전역 설정(Global Settings Directory)

* 위치:

```
~/.kiro
```

* 모든 Kiro CLI 세션에서 공통적으로 사용하는 전역 구성(global configuration) 저장소입니다.
* 예: `settings.json`, MCP 설정, 히스토리 파일 등이 여기에 위치

***

### 2.2 프로젝트별 설정(Project Workspace Settings)

* Kiro CLI를 실행한 현재 디렉터리(Current Working Directory) 가 자동으로 프로젝트 작업 공간(Project Workspace)으로 처리됩니다.
* 해당 디렉터리 아래에 다음 폴더가 생성될 수 있습니다:

```
.kiro/
```

* 이 폴더는 해당 프로젝트에만 적용되는 로컬 설정(Local Configuration) 을 저장합니다.<br>

> ℹ️ 아직 특별히 설정할 필요는 없습니다. 본 배경 지식은 이후 워크숍에서 Kiro CLI의 동작을 사용자 환경에 맞게 최적화할 때 활용됩니다.

***

## 3. 프록시 환경에서 Kiro CLI 사용하기

_Using Kiro CLI Behind a Proxy_

기업망 또는 보안 환경에서 Kiro CLI를 실행하는 경우, 프록시 서버가 필요한 경우가 있습니다.

프록시 설정 방법은 공식 문서에 상세히 설명되어 있으므로 다음 페이지를 참고하십시오:

→ _Kiro CLI Proxy Configuration Documentation_

***

## 4. Kiro CLI 디버깅 옵션

_Debugging Options in Kiro CLI_

Kiro CLI 실행 시 환경 변수(Env Variable) KIRO\_LOG\_LEVEL을 지정하면 로그 상세 수준(Log Verbosity Level)을 변경할 수 있습니다.

#### 예시

```
export KIRO_LOG_LEVEL=trace
k
```

trace 모드는 가장 많은 디버깅 정보를 기록하며,

로그는 아래 위치에 저장됩니다:

```
$TMPDIR/kiro-log/kiro-chat-log
```

#### 지원 로그 레벨

* trace
* debug
* warn
* info
* error

> ⚠️ Trace/debug 모드는 성능을 저하시킬 수 있으니 필요한 경우에만 사용하십시오.

***

## 5. Kiro CLI Settings 구조 및 관리

_Managing Kiro CLI Settings_

전역 설정 파일은 다음 위치에 있습니다:

```
~/.kiro/settings
```

Kiro CLI는 JSON 기반 설정 파일을 사용하며, 다음 중 하나의 방식으로 수정할 수 있습니다:

* CLI 명령을 이용한 수정

```
kiro-cli settings
```

* 설정 파일 직접 편집

***

### 5.1 예시: 기본 모델 변경하기

아래 명령은 기본 대화 모델(default model)을 변경합니다:

```
kiro-cli settings chat.defaultModel claude-sonnet-4.5
```

***

### 5.2 설정 파일 직접 열기

다음 명령은 설정 파일을 기본 편집기에서 엽니다:

```
kiro-cli settings list
```

예시:

```
chat.defaultModel = "claude-sonnet-4.5"
```

***

### 5.3 전체 설정 조회

```
kiro-cli settings all
```

출력 예:

```
chat.defaultModel = "claude-sonnet-4.5"
```

***

***

## 6. Kiro CLI 진단 정보 수집

_Diagnostic Tools for Kiro CLI_

설치 환경과 구성 정보를 요약하여 제공하는 유용한 명령:

```
kiro-cli diagnostic
```

출력 예시(요약):

```
[q-details]
version = "1.21.0"
hash = "dc54efd85f411d6b4347d192733ff40650d38dfb"
date = "2025-11-26T22:30:26.062904Z (10d ago)"
variant = "minimal"

[system-info]
chip = "Intel(R) Xeon(R) Platinum 8375C CPU @ 2.90GHz"
total-cores = 4
memory = "30.81 GB"

[system-info.os.linux]
kernel_version = "6.1.158-178.288.amzn2023.x86_64"
id = "amzn"
name = "Amazon Linux"
pretty_name = "Amazon Linux 2023.9.20251117"
version_id = "2023"
version = "2023"

[environment]
cwd = "/home/USER"
cli-path = "/home/USER"
os = "Linux"
shell-path = "/usr/bin/bash"
shell-version = "5.2.15"
terminal = "VSCode"
install-method = "unknown"

[env-vars]
PATH = "/usr/local/lib/code-server/lib/vscode/bin/remote-cli:/home/USER/.local/bin:/home/USER/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin"
Q_SET_PARENT_CHECK = "1"
SHELL = "/bin/bash"
TERM = "xterm-256color"
```

각 사용자 환경에 따라 출력 내용은 다릅니다.

***

## 7. 실험적 기능(Experimental Features) 사용하기

Working with Experimental Features

Kiro CLI는 출시 초기 단계의 기능(베타 기능)을 /experiment 명령을 통해 활성화하거나 비활성화할 수 있습니다.

#### 실행

```
/experiment
```

예시 화면:

```
> /experiment

 Press (↑↓) to navigate · Enter(⏎) to toggle an experiment 
❯ Knowledge                 [OFF] Enables persistent context storage and retrieval across chat sessions (/knowledge)
  Thinking                  [OFF] Enables complex reasoning with step-by-step thought processes
  Tangent Mode              [OFF] Enables entering into a temporary mode for sending isolated conversations (/tangent)
  Todo Lists                [OFF] Enables Kiro to create todo lists that can be viewed and managed using /todos
  Checkpoint                [OFF] Enables workspace checkpoints to snapshot, list, expand, diff, and restore files (/checkpoint)
                                  Note: Cannot be used in tangent mode (to avoid mixing up conversation history)
  Context Usage Indicator   [OFF] Shows context usage percentage in the prompt (e.g., [rust-agent] 6% >)
  Delegate                  [OFF] Enables launching and managing asynchronous subagent processes
```

* 방향키로 탐색
* Space 로 기능 ON/OFF 전환
* 변경 사항은 자동으로 settings.json에 반영됨

<br>

> 고급 워크샵 단계에서 이러한 기능을 실제로 활용해봅니다.

***

## 8. 작업 완료 알림 설정

<br>

Enabling Task Completion Notifications

<br>

장시간 작업을 Kiro CLI가 수행하는 경우,

작업 완료 시 터미널 알림(Terminal Notification)을 받을 수 있습니다.

<br>

#### 알림 활성화

```
kiro-cli settings chat.enableNotifications true
```

#### 알림 비활성화

```
kiro-cli settings chat.enableNotifications false
```

터미널에 따라 알림 방식은 다를 수 있으며,

이 기능은 장기 실행 작업의 생산성을 크게 향상합니다.

***

## Supporting Resources

<br>

추가 참고 자료

* Kiro CLI Experimental Features Documentation
* 공식 문서: https://kiro.dev/

***

### ✔ 다음 단계도 도와드릴까요?

<br>

원하시면

* Advanced Topics 섹션 전체
* Hooks, Agents, MCP Servers, Steering 등 심화 문서
* GitBook 전체 워크숍 커리큘럼 구조 설계

<br>

까지 동일한 톤과 품질로 제작해드릴 수 있습니다.
