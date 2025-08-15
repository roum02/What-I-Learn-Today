# AWS SAP 스터디 전 2주 통합 학습 로드맵

## 🎯 목표

- AWS Solutions Architect Professional(SAP) 스터디 참여 전 필수 기초 습득
- SAA 수준의 핵심 서비스 이해 + 실습 경험 확보
- AWS 공식문서와 실습 자료를 통한 실무 감각 강화

---

## 📅 2주 학습 플랜

### Day 1 — AWS 개요 & EC2

- 책: 1장 **AWS란**, 2.1~2.2 **EC2 소개**
- 문서: [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/), [Amazon EC2 개요](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/concepts.html)
- 실습: EC2 생성 + SSH 접속
- 추가: EC2 구매 옵션 (온디맨드, 예약, 스팟)

---

### Day 2 — EC2 심화 & EBS

- 책: 2.3 **EC2 실습**, 5.3 **EBS**
- 문서: [Amazon EBS 개요](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/AmazonEBS.html)
- 실습: EBS 볼륨 생성·연결

---

### Day 3 — 네트워킹 (VPC)

- 책: 3.1~3.3 **VPC 개요**
- 문서: [VPC 개요](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/what-is-amazon-vpc.html)
- 실습: 퍼블릭+프라이빗 서브넷 구성
- 추가: Security Group vs NACL 차이

---

### Day 4 — 로드 밸런서

- 책: 4장 **ELB**
- 문서: [Elastic Load Balancing 개요](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)
- 실습: ALB 생성 + EC2 연결
- 추가: ALB vs NLB 차이

---

### Day 5 — S3

- 책: 5.4 **S3**
- 문서: [Amazon S3 개요](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- 실습: S3 버킷 생성 + 정적 웹 호스팅
- 추가: 스토리지 클래스 (Standard, IA, Glacier)

---

### Day 6 — 데이터베이스

- 책: 6장 **RDS**
- 문서: [Amazon RDS 개요](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- 실습: RDS 생성 + EC2 웹서버 연결
- 추가: [DynamoDB 개요](https://docs.aws.amazon.com/ko_kr/amazondynamodb/latest/developerguide/Introduction.html)

---

### Day 7 — 복습 + 기초 문제

- 책: 1~6장 복습
- 문제: Tutorial Dojo SAA 무료 문제
- 부족 서비스: 공식문서 보충

---

### Day 8 — DNS & CDN

- 책: 7.1~7.5 **Route 53, CloudFront**
- 문서: [Route 53 개요](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html), [CloudFront 개요](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
- 실습: S3 + CloudFront 배포

---

### Day 9 — IAM

- 책: 8장 **IAM**
- 문서: [IAM 개요](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html)
- 실습: 사용자 생성 + 정책 연결
- 추가: 역할(Role)과 정책(Policy) 차이

---

### Day 10 — Auto Scaling

- 책: 9장 **Auto Scaling**
- 문서: [Auto Scaling 개요](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)
- 실습: Auto Scaling 그룹 생성

---

### Day 11 — 서버리스 1 (추가)

- 문서: [AWS Lambda 개요](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- 실습: S3 → Lambda 트리거
- 추가: [API Gateway 개요](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)

---

### Day 12 — 보안 & 로깅

- 문서: [AWS CloudTrail](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-user-guide.html), [Amazon CloudWatch](https://docs.aws.amazon.com/cloudwatch/)
- 추가: [AWS KMS 개요](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)
- 실습: CloudWatch 알람 생성

---

### Day 13 — Well-Architected & DR

- 문서: [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
- 추가: [DR 전략 4단계](https://aws.amazon.com/ko/whitepapers/disaster-recovery-workloads-on-aws/)

---

### Day 14 — SAP 예시 문제

- 문제: Tutorial Dojo SAP 샘플 문제
- 복습: 문제에서 언급된 서비스 공식문서 재확인

---

## 📌 참고 자료

- [AWS 공식 문서](https://docs.aws.amazon.com/)
- [AWS Skill Builder](https://explore.skillbuilder.aws/)
- [Tutorial Dojo](https://tutorialsdojo.com/)
