---
description: 'Update : 2025.12.0'
---

# LAB 01 . Kiro CLI 초기 구축 및 사용

## Kiro CLI 초기 구축 및 사용

_Establishing and Initiating Kiro CLI Usage_

이 문서는 Kiro CLI를 실무 환경에서 활용하기 위한 초기 구축 절차(Initial Setup) 와 사용 개시 단계(Getting Started) 를 종합적으로 안내합니다.

본 랩(Lab)에서는 다음 과정을 수행합니다:

* Kiro CLI 사용을 위한 Builder ID 등록
* Kiro CLI 다운로드 및 설치
* Kiro CLI 환경 구성(Configuration Options) 이해 및 탐색

Linux·macOS에서는 GitHub/Google 인증을 지원하며, WSL·헤드리스 환경에서는 Builder ID 또는 AWS Identity Center(IdC) 인증이 필요합니다.

***

## 1. Builder ID 생성 절차

_Creating and Registering Your Builder ID_

> 이미 Builder ID를 보유하고 있다면 본 단계를 생략할 수 있습니다.

Kiro CLI의 모든 인증 흐름은 Builder ID를 기반으로 하므로, 유효한 이메일 주소만 있으면 손쉽게 생성할 수 있습니다.

#### 생성 절차 요약

1. Builder ID 페이지 접속
2. Sign in with Builder ID 선택
3. 브라우저에서 이메일 기반 등록 진행

***

## 2. Kiro CLI 설치 절차

_Installation Procedure for Kiro CLI_

Builder ID 준비가 완료되면, Kiro CLI를 다운로드 → 설치 → 초기 구성하는 단계로 이동합니다.

설치 항목을 진행하기 전, Kiro CLI가 동작하는 기반 환경인 터미널(Terminal) 및 셸(Shell) 개념을 간단히 살펴봅니다.

***

### 2.1 터미널 및 셸 개요

_Overview of Terminal and Shell Environments_

명령줄 인터페이스(Command Line Interface)는 시스템과 상호작용하는 텍스트 기반 인터페이스로, 도구 실행·파일 편집·애플리케이션 시작 등 운영체제 기능을 직접 조작할 수 있습니다.

* Kiro CLI는 bash, zsh, fish 셸에서 안정적으로 동작
* iTerm2, Ghostty, tux 등 다양한 터미널 애플리케이션과 호환
* Windows에서는 PowerShell, CMD가 아닌 WSL 기반 Linux Shell 사용 필요

***

## 3. 운영체제별 설치 옵션

_Installation Options by Operating System_

### 3.1 macOS

Kiro.dev 공식 문서의 설치 절차를 따르면 간단히 설치할 수 있습니다.

### 3.3 Linux

Ubuntu 및 기타 Linux 배포판 설치 방법은 모두 Kiro.dev 문서에 정리되어 있습니다.

***

## 4. Kiro CLI 로그인 절차

_Authentication and Login Workflow_

설치가 완료되면 Kiro CLI를 활성화하기 위해 인증 절차를 진행해야 합니다.

본 워크숍에서는 Builder ID를 기준으로 로그인합니다.

***

### 4.1 CLI에서 로그인 시작

```
kiro-cli login --use-device-flow
```

***

### 4.2 GUI 환경(macOS, Linux)

* 브라우저가 자동으로 열리며 인증 공급자 선택
* Builder ID 선택 후 로그인
* 이미 세션이 존재한다면 자동 스킵될 수 있음

***

### 4.3 헤드리스 환경(WSL·CLI Only)

터미널에 다음과 같은 선택지가 표시됩니다:

```
? Select login method ›
 Use for Free with Builder ID
❯Use with Pro license
```

Builder ID를 선택하면 디바이스 코드 인증(Device Code Authentication) 화면이 표시됩니다:

```
Code: PNDN-QVKB
Open this URL:
https://whchoi01.awsapps.com/start/#/device?user_code=PNDN-QVKB
▰▰▱▱▱▱▱ Logging in...
```

브라우저에서 인증 후 터미널에는 다음 메시지가 표시됩니다:

```
Logged in successfully
```

***

### 4.4 고급 인증 옵션

_Advanced Authentication Options_

AWS Identity Center(IdC)를 통한 엔터프라이즈 인증:

```
kiro-cli login --use-device-flow --license pro \
--identity-provider {IdC login URL} \
--region {region}
```

***

## 5. 로그아웃

_Signing Out_

```
kiro-cli logout
```

***

## 6. 설치 검증

_Verifying Installation Integrity_

설치와 설정이 정상 상태인지 확인하려면 다음 명령을 실행합니다:

```
kiro-cli doctor
```

예상되는 정상 출력:

```
✔ zsh ~/.zshrc integration check
✔ Everything looks good!
```

Kiro CLI 버전 확인:

```
kiro-cli -V
```

예시:

```
kiro-cli 1.21.0
```

***

## 7. 기본 MCP 서버 구성

_Default MCP Server Configuration_

Kiro CLI v1.21.0 이상에서는 다음 도구를 포함한 기본 MCP 서버가 자동 설치됩니다.

* web\_fetch
* web\_search

설정 파일:

```
~/.kiro/settings/mcp.json
```

JSON 구성 예시는 기존 설명 유지.

***

## 8. Kiro CLI 업데이트

_Updating to the Latest Version_

```
kiro-cli update
```

업데이트 여부(Yes/No)를 확인한 후 최신 버전을 자동으로 설치합니다.

변경 로그(Changelog):

```
kiro-cli version --changelog
kiro-cli version --changelog 1.20.0
```

***

## 9. 대화 히스토리 확인

_Accessing Kiro CLI Chat History_

Kiro CLI는 사용자의 모든 입력 기록을 다음 파일에 저장합니다:

```
~/.kiro/.cli_bash_history
```

***

## 10. CLI 사용 편의를 위한 Alias 구성

_Configuring Aliases for Improved Productivity_

```
alias k='kiro-cli'
alias kh='cat ~/.kiro/.cli_bash_history'
```

* k → Kiro CLI 실행 단축
* kh → 대화 기록 즉시 조회

***

