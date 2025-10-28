2. 한 회사가 API로 구동되는 클라우드 커뮤니케이션 플랫폼을 설계하고 있습니다. 이 애플리케이션은 Network Load Balancer(NLB) 뒤의 Amazon EC2 인스턴스에서 호스팅됩니다. 
이 회사는 Amazon API Gateway를 사용하여 외부 사용자에게 API를 통해 애플리케이션에 대한 액세스를 제공합니다.
이 회사는 SQL 주입과 같은 웹 익스플로잇으로부터 플랫폼을 보호하고 대규모의 정교한 DDoS 공격을 탐지하고 완화하고자 합니다.
어떤 솔루션 조합이 가장 많은 보호를 제공합니까? 
(두 가지를 선택하세요.)
A. AWS WAF를 사용하여 NLB를 보호하세요.
B. NLB와 함께 AWS Shield Advanced를 사용합니다.
C. AWS WAF를 사용하여 Amazon API Gateway를 보호합니다.
D. AWS Shield Standard와 함께 Amazon GuardDuty 사용
E. Amazon API Gateway와 함께 AWS Shield Standard를 사용합니다.

답: B,C


## 문제에서 요구하는 것
- API 기반 애플리케이션 보안 구조 설계
- 웹 익스플로잇(SQL injection, XSS 등 L7 공격) 방어
- 대규모·정교한 DDoS 공격 탐지 및 완화

```
[사용자] → [API Gateway] → [NLB] → [EC2 애플리케이션]
```

## 키워드

### AWS WAF (Web Application Firewall)
애플리케이션 계층(L7) 방화벽.
HTTP(S) 요청의 패턴을 검사해 SQL Injection, XSS, Command Injection 등을 차단.
“웹 애플리케이션 공격”은 대부분 L7 계층에서 발생하므로,
WAF는 **HTTP 요청 내용(URI, Header, Body)**을 검사할 수 있음

### NLB
- Network Load Balancer (NLB)
- L4 계층 로드밸런서 (TCP/UDP 기반). => OSI 계층상 L4라서 HTTP 헤더/쿼리를 인식하지 않음 → WAF 적용 불가
- 트래픽 분산 담당.

### AWS Shield
AWS 네트워크 계층(L3/L4)에서의 DDoS 공격을 자동 완화하는 서비스.
두 가지 버전이 있음:

- Shield Standard (무료, 기본 포함)
- Shield Advanced (유료, 고급 보호)

Shield는 “네트워크 계층 보호(L3/L4)” 중심이지만,
ALB/CloudFront/API Gateway와 결합하면 L7까지 간접 보호 가능

### Amazon API Gateway

REST/HTTP/WebSocket API를 외부 사용자에게 노출하는 서비스.
트래픽의 첫 진입점(Entry point) 역할.
WAF, Shield와 통합되어 애플리케이션 계층 보안 적용 가능.

=> 두 서비스가 같은 L7 계층에서 동작하기 때문에, API Gateway에 WAF 직접 연결 가능 (SQLi/XSS 등 필터링)


### Amazon GuardDuty
지속적 위협 탐지 서비스.
즉, “탐지”는 하지만 “차단/완화”는 하지 않음.




3. 한 회사가 AWS에 최신 제품을 배포했습니다. 이 제품은 Network Load Balancer 뒤의 Auto Scaling 그룹에서 실행됩니다. 이 회사는 제품의 객체를 Amazon S3 버킷에 저장합니다.
이 회사는 최근 시스템에 대한 악의적인 공격을 경험했습니다. 이 회사는 AWS 계정, 워크로드, S3 버킷에 대한 액세스 패턴에서 악의적인 활동을 지속적으로 모니터링하는 솔루션이 필요합니다. 
이 솔루션은 또한 의심스러운 활동을 보고하고 대시보드에 정보를 표시해야 합니다.
어떤 솔루션이 이러한 요구 사항을 충족할까요?
A. Amazon Macie를 구성하여 모니터링하고 AWS Conbg에 결과를 보고합니다.
B. Amazon Inspector를 구성하여 모니터링 결과를 AWS CloudTrail에 보고합니다.
C. Amazon GuardDuty를 구성하여 모니터링하고 결과를 AWS Security Hub에 보고합니다.
D. AWS Config를 구성하여 모니터링을 수행하고 Amazon EventBridge에 결과를 보고합니다.

답: C

## 요구사항
```
"AWS 계정, 워크로드, S3 버킷의 액세스 패턴을 지속적으로 모니터링하고,
**악의적인 활동(의심스러운 행동)**을 **탐지·보고·시각화(대시보드)**해야 한다.”
```
즉, 보안 이상 탐지 + 중앙 보고 + 시각화 통합 기능을 가진 서비스


## 키워드

### Amazon Macie + AWS Config
Macie: S3 버킷 내 민감 데이터(PII, 개인정보) 탐지용.
→ “데이터 분류(Data Classification)” 목적.

AWS Config: 리소스 구성 변경 감시 및 규정 준수 확인용.
→ 공격/이상행동 탐지 기능 없음.


### Amazon Inspector + AWS CloudTrail
Inspector: EC2, ECR, Lambda에 대한 취약점(Vulnerability) 스캐너.
→ 실행 중 워크로드의 “보안 결함” 점검용.

CloudTrail: AWS API 호출 기록용.
→ Inspector 결과를 CloudTrail로 “보고”하는 구조 자체가 비논리적.

### Amazon GuardDuty + AWS Security Hub
GuardDuty:
CloudTrail, VPC Flow Logs, DNS Logs 분석 →
비정상 로그인, 포트 스캔, 데이터 유출, C2 트래픽 등 탐지.
계정·워크로드·S3 액세스 패턴 이상 행위 탐지 모두 지원.

Security Hub:
GuardDuty, Inspector, Macie 등 여러 서비스의 결과를
중앙 대시보드로 통합·시각화.
경고 통합(Findings Aggregation) + Compliance View 제공.


### AWS Config + EventBridge

Config: 리소스 구성 상태 모니터링.
예: S3 버킷 Public 여부, 보안그룹 포트 오픈 여부.
“행위(behavior)”가 아니라 “상태(state)” 중심.

EventBridge: 이벤트 전달/자동화 서비스.
보안 분석용 아님.





4. 한 회사에 두 개의 Amazon EC2 인스턴스에 호스팅된 동적 웹 애플리케이션이 있습니다. 이 회사는 자체 SSL 인증서를 가지고 있으며, 각 인스턴스에 SSL 종료를 수행합니다.
최근 트래픽이 증가했고 운영 팀은 SSL 암호화 및 복호화로 인해 웹 서버의 컴퓨팅 용량이 최대 한도에 도달하고 있다고 판단했습니다.
솔루션 아키텍트는 애플리케이션의 성능을 높이기 위해 무엇을 해야 할까요?
A. AWS Certificate Manager(ACM)를 사용하여 새 SSL 인증서를 만듭니다. 각 인스턴스에 ACM 인증서를 설치합니다.
B. Amazon S3 버킷 만들기 SSL 인증서를 S3 버킷으로 마이그레이션합니다. EC2 인스턴스가 SSL 종료를 위해 버킷을 참조하도록 구성합니다.
C. 프록시 서버로 다른 EC2 인스턴스를 만듭니다. SSL 인증서를 새 인스턴스로 마이그레이션하고 기존 EC2 인스턴스에 직접 연결하도록 구성합니다.
D. SSL 인증서를 AWS Certificate Manager(ACM)로 가져옵니다. ACM의 SSL 인증서를 사용하는 HTTPS 리스너가 있는 Application Load Balancer를 만듭니다.

답: D


## 요구사항

현재 EC2 인스턴스(2대)에서 직접 SSL 종료(TLS termination) 중 → 암·복호화로 CPU 병목

목표: 애플리케이션 성능 향상(= SSL 처리 부하를 인스턴스에서 떼어내기)



## 키워드


### AWS Certificate Manager(ACM):

SSL/TLS 인증서를 관리하는 AWS 서비스.

AWS에서 무료로 퍼블릭 인증서 발급 / 기존(자체 발급) 인증서도 등록 가능

EC2에는 직접 설치 불가
로드밸런서, CloudFront 등 AWS 관리형 서비스와 함께 사용해야 함

<!--
- ACM이 발급한 퍼블릭 인증서: ALB/CloudFront 등 AWS 통합 서비스에서만 사용 가능, EC2에 직접 설치 불가.
- 가져오기(Import)한 인증서: 기존 자체 인증서를 ACM에 업로드해 ALB 등에서 사용 가능(자동 갱신은 직접).
-->

### SSL Offloading (오프로딩)

SSL 암호화/복호화 연산을 **애플리케이션 서버가 아닌 다른 곳(로드밸런서 등)**에서 대신 수행하는 것.

EC2에는 직접 설치 불가

로드밸런서, CloudFront 등 AWS 관리형 서비스와 함께 사용해야 함

** “EC2를 프록시로 만들어 SSL 종료를 대신 하자”는 접근은 가능하지만 관리 비용↑ / HA 보장 X

c.f. AWS에서의 대표적 구현:

Application Load Balancer(ALB) + HTTPS 리스너

(또는 CloudFront + ACM)


### SSL / TLS Termination (종단)

클라이언트(브라우저) ↔ 서버 간 통신을 암호화하는 HTTPS 연결의 끝부분을 어디에서 처리할지를 의미합니다.
“종단(Termination)”은 SSL 암호 해제(복호화)를 수행하는 지점

- EC2에서 SSL 종단 → 서버 CPU가 암호화 연산 수행 → 부하 증가
- ALB에서 SSL 종단 → 로드밸런서가 암호화 처리 → EC2는 평문 HTTP로만 통신 → 부하 감소

c.f. B. S3는 인증서 저장소나 SSL 종료 지점이 아님.

EC2가 여전히 직접 TLS 처리 → 병목 해소 실패 + 보안/운영 모범 사례 아님





5. 한 회사가 Amazon S3 버킷을 데이터 레이크 스토리지 플랫폼으로 사용합니다. S3 버킷에는 여러 팀과 수백 개의 애플리케이션에서 무작위로 액세스하는 방대한 양의 데이터가 들어 있습니다. 
이 회사는 S3 스토리지 비용을 줄이고 자주 액세스하는 객체에 대한 즉각적인 가용성을 제공하고자 합니다.
이러한 요구 사항을 충족하는 가장 운영 효율적인 솔루션은 무엇입니까?
A. 객체를 S3 Intelligent-Tiering 스토리지 클래스로 전환하기 위한 S3 수명 주기 규칙을 생성합니다.
B. Amazon S3 Glacier에 객체를 저장합니다. S3 Select를 사용하여 애플리케이션에 데이터 액세스를 제공합니다.
C. S3 스토리지 클래스 분석의 데이터를 사용하여 S3 수명 주기 규칙을 생성하여 객체를 S3 Standard-Infrequent Access(S3 Standard-IA) 스토리지 클래스로 자동 전환합니다.
D. 객체를 S3 Standard-Infrequent Access(S3 Standard-IA) 스토리지 클래스로 전환합니다. 애플리케이션에서 객체에 액세스할 때 객체를 S3 Standard 스토리지 클래스로 전환하는 AWS Lambda 함수를 만듭니다.


## 요구사항

- 비용 절감: S3 저장 비용을 낮춰야 함
- 즉각적 가용성: “자주 액세스하는 객체”는 지연 없이 곧바로 읽혀야 함
=> 여러 팀·수백 개 앱이 무작위 패턴으로 접근 → 운영 자동화/자체 최적화가 중요


## 키워드

### 수명 주기로 S3 Intelligent-Tiering 전환

: 접근 패턴 자동 모니터링 후 자주/비자주/아카이브(Instant/Archive) 등으로 자동 이동
자주/비자주 티어는 즉시 조회(복원 불필요) → “즉각적 가용성” 충족

