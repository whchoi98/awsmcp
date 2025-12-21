---
description: 'Update : 2025.12.0'
---

# LAB 1 . Kiro CLI 초기 구축 및 사용

## Kiro CLI 초기 구축 및 사용

이 문서는 Kiro CLI를 실무 환경에서 활용하기 위한 초기 구축 절차(Initial Setup) 와 사용 개시 단계(Getting Started) 를 종합적으로 안내합니다.

본 랩(Lab)에서는 다음 과정을 수행합니다:

* Kiro CLI 사용을 위한 Builder ID 등록
* Kiro CLI 다운로드 및 설치
* Kiro CLI 환경 구성(Configuration Options) 이해 및 탐색

Linux·macOS에서는 GitHub/Google 인증을 지원하며, WSL·헤드리스 환경에서는 Builder ID 또는 AWS Identity Center(IdC) 인증이 필요합니다.

***

## 1. Builder ID 생성 절차

> 이미 Builder ID를 보유하고 있다면 본 단계를 생략할 수 있습니다.

Kiro CLI의 모든 인증 흐름은 Builder ID를 기반으로 하므로, 유효한 이메일 주소만 있으면 손쉽게 생성할 수 있습니다.

#### 생성 절차 요약

1. Builder ID 페이지 접속
2. Sign in with Builder ID 선택
3. 브라우저에서 이메일 기반 등록 진행

***

## 2. Kiro CLI 설치 절차

Builder ID 준비가 완료되면, Kiro CLI를 다운로드 → 설치 → 초기 구성하는 단계로 이동합니다.

설치 항목을 진행하기 전, Kiro CLI가 동작하는 기반 환경인 터미널(Terminal) 및 셸(Shell) 개념을 간단히 살펴봅니다.

***

### 2.1 터미널 및 셸 개요

명령줄 인터페이스(Command Line Interface)는 시스템과 상호작용하는 텍스트 기반 인터페이스로, 도구 실행·파일 편집·애플리케이션 시작 등 운영체제 기능을 직접 조작할 수 있습니다.

* Kiro CLI는 bash, zsh, fish 셸에서 안정적으로 동작
* iTerm2, Ghostty, tux 등 다양한 터미널 애플리케이션과 호환
* Windows에서는 PowerShell, CMD가 아닌 WSL 기반 Linux Shell 사용 필요

***

## 3. 운영체제별 설치 옵션

### 3.1 macOS

```
curl -fsSL https://cli.kiro.dev/install | bash
```

### 3.3 Linux

설치 파일 다운로드

```
curl --proto '=https' --tlsv1.2 -sSf \
'https://desktop-release.q.us-east-1.amazonaws.com/latest/kirocli-x86_64-linux.zip' \
-o 'kirocli.zip'
```

압축 해제

```
unzip kirocli.zip
```

설치 스크립트 쉘 시작

```
./kirocli/install.sh
```

***

## 4. Kiro CLI 로그인 절차

설치가 완료되면 Kiro CLI를 활성화하기 위해 인증 절차를 진행해야 합니다.

본 워크숍에서는 Builder ID를 기준으로 로그인합니다.

***

### 4.1 CLI에서 로그인 시작

또는 아래 명령어로 로그인을 시작합니다.

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
  Use with Builder ID
  Use with IDC Account
```

Builder ID를 선택하면 디바이스 코드 인증(Device Code Authentication) 화면이 표시됩니다:

IDC Account를 선택하면 Identity Center로 인증을 시도합니다.

```
$ kiro-cli login --use-device-flow
✔ Select login method · Use with IDC Account
✔ Enter Start URL · https://whchoi01.awsapps.com/start/
? Enter Region › us-east-1
```

인증을 위해서 아래와 같은 URL 접속을 요청합니다.

```
Confirm the following code in the browser
Code: XXXX-XXXX

Open this URL: https://whchoi01.awsapps.com/start/#/device?user_code=xxxx-xxxx
▰▰▰▰▱▱▱ Logging in...
```

IDC에 등록된 USER NAME을 입력합니다.

<div align="left"><figure><img src="../.gitbook/assets/image.png" alt="" width="375"><figcaption></figcaption></figure></div>

Password를 입력합니다.

<div align="left"><figure><img src="../.gitbook/assets/image (1).png" alt="" width="375"><figcaption></figcaption></figure></div>

Kiro CLI 서비스를 사용하기 위한 인증권한을 컨펌합니다.

<div align="left"><figure><img src="../.gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure></div>

접근 권한을 최종 수락합니다.

<div align="left"><figure><img src="../.gitbook/assets/image (3).png" alt="" width="375"><figcaption></figcaption></figure></div>

브라우저에서 인증 후 터미널에는 다음 메시지가 표시됩니다:

```
Logged in successfully
```

***

### 4.4 고급 인증 옵션

AWS Identity Center(IdC)를 통한 엔터프라이즈 인증을 아래와 같이 옵션을 통해서, 명령을 수행할 수도 있습니다.

```
kiro-cli login --use-device-flow --license pro \
--identity-provider {IdC login URL} \
--region {region}
```

4.5 인증확인

아래와 같은 명령을 통해서, Kiro CLI 에 접근이 가능한지 확인합니다.

```
kiro-cli
```

정상적으로 로그인이 된다면 아래와 같이 출력됩니다.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

***

## 5. 로그아웃

```
kiro-cli logout
```

***

## 6. 설치 검증

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

Kiro CLI는 사용자의 모든 입력 기록을 다음 파일에 저장합니다:

```
~/.kiro/.cli_bash_history
```

***

## 10. CLI 사용 편의를 위한 Alias 구성

```
k() {
  command kiro-cli "$@"
}

kh() {
  cat ~/.kiro/.cli_bash_history 2>/dev/null
}
```

* k → Kiro CLI 실행 단축
* kh → 대화 기록 즉시 조회

***

