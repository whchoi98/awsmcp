---
description: 'Update : 2025.12.12'
---

# Code Intelligence

***

## 1. 개요 (Overview)

Code Intelligence는 Language Server Protocol(LSP, 언어 서버 프로토콜)을 Kiro CLI에 통합하여, IDE 확장 기능과 유사한 방식으로 코드베이스에 대한 의미론적 이해(Semantic Understanding)를 Kiro 에이전트에게 제공합니다.

이를 통해 Kiro는 단순한 텍스트 검색을 넘어, 심볼(Symbol), 타입(Type), 참조(Reference), 정의(Definition), 진단 정보(Diagnostics)를 이해하고 활용할 수 있습니다.

Kiro CLI는 기본적으로 다음 7개 언어에 대한 LSP 설정을 사전 구성(pre-configured)하여 제공합니다.

* TypeScript / JavaScript
* Rust
* Python
* Go
* Java
* Ruby
* C / C++

또한, 프로젝트 루트의 lsp.json 파일을 통해 커스텀 LSP 설정(Custom LSP Configuration)을 추가함으로써 사실상 모든 언어로 확장 가능합니다.

`/code init` 명령 실행 이후, 다음과 같은 작업을 자연어 기반(Natural Language)으로 수행할 수 있습니다.

* 심볼 검색 (Search Symbols)
* 참조 찾기 (Find References)
* 정의로 이동 (Go to Definition)
* 파일 간 리네임(Rename across files)
* 진단 정보 조회(Get Diagnostics)

***

## 2. 동작 방식 (How It Works)

Kiro CLI는 백그라운드에서 LSP 서버 프로세스(Language Server Process)를 실행하며, 이들은 stdio 기반 JSON-RPC를 통해 Kiro와 통신합니다.

작업 흐름은 다음과 같습니다.

1. 워크스페이스 초기화 시, 프로젝트 마커(Project Marker)
   * 예: package.json, Cargo.toml
   * 파일 확장자(.ts, .rs, .py 등)
2. 이를 기반으로 사용 언어 자동 감지(Language Detection)
3. 해당 언어에 맞는 LSP 서버 자동 실행
4. LSP 서버는 지속적으로:
   * 심볼(Symbol)
   * 타입(Type)
   * 참조 관계(Reference Graph)
   *   진단 정보(Diagnostics)

       를 분석·인덱싱
5. 사용자가 자연어로 질문하면:
   * Kiro가 이를 \*\*LSP 요청(LSP Request)\*\*으로 변환
   * 관련 서버에 전달
   * 결과를 사람이 읽기 쉬운 형태로 가공하여 출력

***

## 3. Code Intelligence 활성화 절차

### 1. 언어 서버 설치 (Installing Language Servers)

**지원 언어 및 설치 방법**

| 언어                      | 확장자                  | LSP 서버                         | 설치 명령                                                |
| ----------------------- | -------------------- | ------------------------------ | ---------------------------------------------------- |
| TypeScript / JavaScript | .ts, .js, .tsx, .jsx | typescript-language-server     | npm install -g typescript-language-server typescript |
| Rust                    | .rs                  | rust-analyzer                  | rustup component add rust-analyzer                   |
| Python                  | .py                  | jedi-language-server / pyright | npm install -g pyright 또는 pip install pyright        |
| Go                      | .go                  | gopls                          | go install golang.org/x/tools/gopls@latest           |
| Java                    | .java                | jdtls                          | brew install jdtls (macOS)                           |
| Ruby                    | .rb                  | solargraph                     | gem install solargraph                               |
| C / C++                 | .c, .cpp, .h, .hpp   | clangd                         | brew install llvm 또는 apt install clangd              |

***

### 2. Code Intelligence 초기화 (Initialize Code Intelligence)

프로젝트 루트에서 다음 명령을 실행합니다.

```
/code init
```

이 명령은 다음을 수행합니다.

* lsp.json 설정 파일 생성
* 언어 서버 실행
* 코드 인텔리전스 초기화

**실행 결과 예시**

```
✓ Workspace initialization started

Workspace: /path/to/your/project
Detected Languages: ["python", "rust", "typescript"]
Project Markers: ["Cargo.toml", "package.json"]

Available LSPs:
✓ jedi-language-server (python) - initialized (687ms)
✓ rust-analyzer (rust) - initialized (488ms)
✓ typescript-language-server (typescript) - initialized (214ms)
○ gopls (go) - not installed
○ solargraph (ruby) - not installed
```

**상태 표시 설명**

* ✓ : 초기화 완료 및 사용 가능
* ◐ : 초기화 진행 중
* ○ available : 설치되어 있으나 현재 프로젝트에서 필요 없음
* ○ not installed : 시스템에 설치되지 않음<br>

> 💡 언어 서버가 비정상 종료되거나 응답하지 않을 경우  `/code init -f`   명령으로 강제 재시작할 수 있습니다.

### 3. 자동 초기화 및 비활성화

*   최초 /code init 실행 이후

    → lsp.json이 존재하면 Kiro CLI 시작 시 자동 초기화
*   Code Intelligence 비활성화

    → 프로젝트 루트에서 lsp.json 삭제



## 4. Language Server 활용 예시

#### 예제 1: 심볼 찾기 (Find Symbol)

```
> Find the UserRepository class
```

출력 예시:

```
1. Class UserRepository at src/repositories/user.repository.ts:15:1
```

#### 예제 2: 참조 찾기 (Find References)

```
> Find references of Person class
```

#### 예제 3: 정의로 이동 (Go to Definition)

```
> Find the definition of UserService
```

#### 예제 4: 파일 내 심볼 조회 (Get File Symbols)

```
> What symbols are in auth.service.ts?
```

#### 예제 5: 리네임 미리보기 (Rename – Dry Run)

```
> Dry run: rename the method "FetchUser" to "fetchUserData"
```

#### 예제 6: 진단 정보 조회 (Diagnostics)

```
> Get diagnostics for main.ts
```

5\. 커스텀 언어 서버 설정 (Custom Language Servers)<br>
----------------------------------------------

프로젝트 루트의 lsp.json 파일을 수정하여 사용자 정의 LSP 서버를 추가할 수 있습니다.

```
{
  "languages": {
    "mylang": {
      "name": "my-language-server",
      "command": "my-lsp-binary",
      "args": ["--stdio"],
      "file_extensions": ["mylang", "ml"],
      "project_patterns": ["mylang.config"],
      "exclude_patterns": ["**/build/**"],
      "multi_workspace": false,
      "initialization_options": {
        "custom": "options"
      },
      "request_timeout_secs": 60
    }
  }
}
```

## 6. 주요 필드 설명

* name: 언어 서버 표시 이름
* command: 실행 바이너리
* args: 실행 인자 (일반적으로 --stdio)
* file\_extensions: 처리할 파일 확장자
* project\_patterns: 프로젝트 루트 식별 파일
* exclude\_patterns: 분석 제외 경로
* multi\_workspace: 멀티 워크스페이스 지원 여부
* initialization\_options: LSP 초기화 옵션
* request\_timeout\_secs: 요청 타임아웃(초)

> ⚠️ 변경 후 Kiro CLI 재시작 필요

## 7. 트러블슈팅 (Troubleshooting)

| 문제            | 원인              | 해결 방법                  |
| ------------- | --------------- | ---------------------- |
| 워크스페이스 초기화 지연 | LSP 서버 인덱싱 중    | 잠시 대기 또는 /code init -f |
| LSP 초기화 실패    | 서버 오류           | /code logs -l 확인       |
| 심볼 검색 결과 없음   | 인덱싱 미완료 / 문법 오류 | 파일 오류 수정, 검색어 구체화      |
| 정의 탐색 실패      | 잘못된 위치          | 심볼 이름 위치 확인            |

## 8. Best Practices

* 프로젝트당 1회만 /code init 실행
* 리네임 작업 전 dry run 필수
* 진단 오류(Diagnostics)를 먼저 해결
* 검색 시 대소문자 및 정확한 심볼명 사용

## 9 .제한 사항 (Limitations)

* LSP 기능 지원 범위는 언어 서버별로 상이
* 대규모 코드베이스는 초기 인덱싱에 시간 소요
* 일부 언어 서버는 rename, formatting 미지원
