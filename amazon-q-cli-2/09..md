# 09.비용최적화 분석하기

## 💸 AWS 리소스 사용 분석 및 비용 최적화 실습

이 실습에서는 Amazon Q CLI를 활용하여 AWS 리소스 사용 현황을 분석하고, 비용 최적화 권장 사항을 도출하며, 실제 최적화 조치를 수행하는 과정을 단계별로 따라갑니다.

***

### 🎯 실습 목표 

이 실습을 통해 다음 내용을 학습할 수 있습니다:

* Amazon Q CLI를 사용한 AWS 리소스 사용량 조회
* 리소스 활용도 및 비용 데이터 분석
* 맞춤형 비용 최적화 권장 사항 도출
* 권장 조치 적용을 통한 비용 절감 실행
* 최적화 이후 효과 분석

***

### 🔧 사전 준비 사항

* AWS CLI 설치 및 구성 완료
* Amazon Q CLI 설치 완료
* AWS Cost Explorer 및 리소스 조회 권한이 포함된 IAM 권한
* 최소 1개월 이상 AWS 리소스 사용 이력

***

### 🧪 실습 단계

\


#### ✅ Step 1: 리소스 사용량 조회

\


Amazon Q CLI를 실행하여 리소스 사용량을 질의합니다.

```
q chat
```

아래와 같은 질문을 자유롭게 할 수 있습니다:

* “지난달 EC2 인스턴스 사용량을 보여줘”
* “S3 스토리지 사용 트렌드를 분석해줘”
* “내 계정에서 가장 비용이 많이 든 서비스를 보여줘”
* “RDS 인스턴스 활용도를 보여줘”

***

#### ✅ Step 2: 비용 최적화 권장 사항 받기

\


동일한 Q CLI 대화 세션에서, 다음과 같은 질문을 통해 비용 최적화 권장 사항을 요청할 수 있습니다:

* “비용을 절감할 수 있는 EC2 인스턴스를 추천해줘”
* “유휴 또는 저활용 리소스를 식별해줘”
* “Savings Plan 또는 예약 인스턴스를 적용할 수 있는 리소스를 알려줘”
* “EBS 볼륨 사용량을 분석하고 최적화 방법을 추천해줘”

***

#### ✅ Step 3: 최적화 조치 실행

\


Amazon Q에서 제공한 권장 사항을 바탕으로 직접 리소스를 최적화합니다.

\


**EC2 인스턴스 유형 조정 예시**

```
aws ec2 stop-instances --instance-ids i-1234567890abcdef0
aws ec2 modify-instance-attribute --instance-id i-1234567890abcdef0 --instance-type t3.micro
aws ec2 start-instances --instance-ids i-1234567890abcdef0
```

**미사용 리소스 삭제**

```
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0
```

**S3 라이프사이클 정책 설정**

```
aws s3api put-bucket-lifecycle-configuration \
  --bucket my-bucket \
  --lifecycle-configuration file://lifecycle-config.json
```

***

#### ✅ Step 4: 최적화 효과 평가

\


조치를 실행한 후, 다시 Q CLI를 통해 비용 절감 효과를 평가합니다.

```
q chat
```

아래와 같은 질문으로 확인해보세요:

* “최적화 전후 비용을 비교해줘”
* “다음 달 예상 AWS 요금은 얼마야?”
* “적용한 최적화 조치의 영향력을 분석해줘”

***

### 🧩 실습 확장

* 리소스 최적화 자동화 스크립트 작성
* 예산 및 비용 경고 설정 (AWS Budgets)
* AWS Organizations + SCP를 활용한 비용 통제 정책 적용

***

### 🧠 정리

\


이번 실습에서는 Amazon Q CLI를 활용해 다음 내용을 실습했습니다:

* AWS 리소스 사용 분석
* 비용 최적화 권장 사항 도출
* 실제 최적화 조치 수행
* 절감 효과 확인 및 분석

\


이러한 역량은 지속적인 비용 절감 및 리소스 효율성 향상에 매우 유용하며, 실환경에서도 반복적으로 적용할 수 있습니다.

***

> 💡 팁:

> Amazon Q에 “How can I lower my AWS bill?”과 같은 질문을 하면, 자동 분석 기반의 맞춤형 절감 전략을 빠르게 확인할 수 있습니다.

***

필요하시면 목차 추가, GitBook 내부 링크, 실습용 .json 샘플 파일 추가 등도 도와드릴 수 있습니다.
