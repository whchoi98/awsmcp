---
description: 'Update : 2025.12.07'
---

# Thinking Tool

Thinking Tool 기능은 복잡한 문제를 해결하는 과정에서 Kiro의 \*\*추론 과정(reasoning process)\*\*을 명시적으로 보여줍니다. 이를 통해 Kiro의 의사 결정 과정을 투명하게 확인하고, 학습·검증·디버깅 시 강력한 통찰을 제공합니다.

***

## 1. Overview

Thinking Tool을 활성화하면 Kiro는 다음을 수행합니다:

* 문제 해결 과정에서 단계별 reasoning을 표시
* 복잡한 맥락을 분석할 때 intermediate reasoning 공개
* 의사결정 기준과 고려 요소를 구조화하여 설명
* 최종 결론에 도달하기까지의 논리적 흐름 전면 공개

이 기능은 특히 아키텍처 설계, 알고리즘 선택, 디버깅, 트레이드오프 분석 등 복잡한 기술 작업에서 유용합니다.

***

## 2. Enabling Thinking Tool

### CLI 설정으로 활성화

```
kiro-cli settings chat.enableThinking true
```

### 실험 기능 UI로 활성화

```
/experiment
# "Thinking" 항목 선택
```

***

## 3. How It Works

Thinking Tool은 Kiro가 “복잡한 문제”라고 판단할 때 자동으로 활성화됩니다.

활성화 조건:

* 여러 단계의 논리가 필요한 문제
* 다양한 기술적 선택지를 분석해야 하는 상황
* 의존성이 많은 멀티스텝 계획(planning)
* 디버깅·성능 분석처럼 체계적 접근이 필요한 문제
* 아키텍처, 설계 패턴 등 trade-off 분석 요구



Thinking Tool 활성화 시 Kiro는 다음을 수행합니다:

1. 문제를 구성 요소로 분해
2. 각 요소에 대한 고려사항을 정리
3. 가능한 해결책/옵션을 비교
4. 기준에 따라 선택지 평가
5. 최종 결론 도출

***

## 4. Example Usage

### 4.1 일반 응답과 Thinking Tool 비교

#### Without Thinking

```
> What's the best way to implement caching for our API?
I recommend using Redis for caching...
```

#### With Thinking Tool

```
🧠 Thinking...

1. First, analyze the nature of cached data
   - Heavy read workload
   - Need TTL and invalidation

2. Evaluate candidate technologies
   - In-memory: fast but limited
   - Redis: distributed, persistent, TTL support
   - Memcached: fast but limited features

3. Based on your use case:
   - API responses → distributed cache needed
   - TTL important → Redis fits well

Conclusion: Redis is the most suitable choice.
```

***

## 5. Benefits

### 5.1 For Learning & Knowledge Transfer

* 복잡한 문제 해결 방식을 관찰하여 논리적 사고 향상
* AI의 분석 단계가 그대로 공개되어 학습 효과 극대화
* 의사결정 이유가 명확해져 기술적 판단력 향상

### 5.2 For Debugging

* Kiro가 판단 과정에서 어떤 가설을 고려하는지 추적 가능
* 잘못된 가정이나 정보 부족 지점 식별
* 문제 원인 분석 과정의 투명성 확보

### 5.3 For Technical Decision-Making

* 옵션별 장단점을 명확히 비교
* 아키텍처·알고리즘·패턴 선택 시 신뢰성 향상
* 복잡한 의사결정을 구조적으로 검증 가능

***

## 6. Use Cases

### 6.1 Architecture Decisions

```
> Should we use microservices or a monolith?
🧠 Thinking...
- Consider team size, scalability, deployment needs
- Trade-offs between complexity vs speed
- Recommend monolith for small teams, uncertain requirements
```

### 6.2 Algorithm Selection

```
> Which sorting algorithm should I use?
🧠 Thinking...
- Evaluate data size, partial-sortedness, memory constraints
- Compare Quick Sort, Merge Sort, Tim Sort, Heap Sort
- Provide recommendation with reasoning
```

### 6.3 Debugging Complex Issues

```
> My application is slow but I don't know why
🧠 Thinking...
- Check DB queries, network latency, memory leaks, CPU-bound tasks
- Suggest diagnostic order and reasoning
```

***

## 7. Configuration

### Enable/Disable

```
# Enable
kiro-cli settings chat.enableThinking true

# Disable
kiro-cli settings chat.enableThinking false

# Check
kiro-cli settings chat.enableThinking
```

***

## 8. Limitations

### 8.1 Performance

Thinking Tool는 reasoning을 생성하므로 다음이 발생할 수 있습니다:

* 응답 지연 증가
* 토큰 사용량 증가
* 출력 결과가 길어짐

### 8.2 Not Needed For

* 단순 질문
* 빠른 반복 작업
* 단순 코드 생성·파일 작성 등 reasoning이 필요 없는 작업

***

## 9. Best Practices

### 9.1 When to Enable

* 새로운 기술을 학습할 때
* 중요한 아키텍처 결정을 검증해야 할 때
* 복잡한 문제를 분석하거나 디버깅할 때
* reasoning 구조를 보고 싶을 때

### 9.2 When to Disable

* 빠른 응답이 필요한 경우
* reasoning 없이 결과만 필요할 때

### 9.3 Workflow Integration

1. 복잡한 문제 시작 전 Thinking Tool 켜기
2. 분석 과정 관찰 & 논리 검증
3. 구현 단계에서는 성능 위해 끄기
4. 리뷰 시 다시 켜서 검증

***

## 10. Troubleshooting

### Thinking이 보이지 않는 경우

1. 활성화 여부 확인

```
kiro-cli settings chat.enableThinking
```

2. 단순 질문은 thinking이 트리거되지 않음
3. 새로운 세션 시작
4. 더 복잡한 질문 입력

### Thinking이 너무 길거나 과도할 때

* 비활성화:

```
kiro-cli settings chat.enableThinking false
```

* “간단히 설명해줘” 또는 “short version” 요청

***

## 11. Related Features

* Tangent Mode — reasoning 보조 질문을 분리된 대화로 진행
* TODO Lists — planning reasoning을 구조화해 action items로 자동 변환
* Experimental Features — Thinking Tool 포함 실험 기능 전체 관리
