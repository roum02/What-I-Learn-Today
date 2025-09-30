1. 한 회사가 새로운 비즈니스 애플리케이션을 구현하고 있습니다. 이 애플리케이션은 두 개의 Amazon EC2 인스턴스에서 실행되고 문서 저장을 위해 Amazon S3 버킷을 사용합니다. 솔루션 아키텍트는 EC2 인스턴스가 S3 버킷에 액세스할 수 있는지 확인해야 합니다.

솔루션 아키텍트는 이 요구 사항을 충족하기 위해 무엇을 해야 합니까?

A. S3 버킷에 대한 액세스를 허용하는 IAM 역할을 만듭니다. 역할을 EC2 인스턴스에 연결합니다.
B. S3 버킷에 대한 액세스를 허용하는 IAM 정책을 만듭니다. 정책을 EC2 인스턴스에 연결합니다.
C. S3 버킷에 대한 액세스를 허용하는 IAM 그룹을 만듭니다. 그룹을 EC2 인스턴스에 연결합니다.
D. S3 버킷에 대한 액세스를 허용하는 IAM 사용자를 만듭니다. 사용자 계정을 EC2 인스턴스에 연결합니다.

2. 다음 IAM 정책은 IAM 그룹에 첨부되었습니다. 이것은 그룹에 적용되는 유일한 정책입니다.

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "1",
      "Effect": "Allow",
      "Action": "ec2:*",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "ec2:Region": "us-east-1"
        }
      }
    },
    {
      "Sid": "2",
      "Effect": "Deny",
      "Action": [
        "ec2:StopInstances",
        "ec2:TerminateInstances"
      ],
      "Resource": "*",
      "Condition": {
        "BoolIfExists": {
          "aws:MultiFactorAuthPresent": false
        }
      }
    }
  ]
}


그룹 구성원에 대한 이 정책의 효과적인 IAM 권한은 무엇입니까? D

A. 그룹 구성원은 us-east-1 지역 내에서 모든 Amazon EC2 작업을 허용받습니다. 허용 권한 이후의 명령문은 적용되지 않습니다.
B. 그룹 구성원은 다중 인증(MFA)을 사용하여 로그인하지 않는 한 us-east-1 지역에서 Amazon EC2 권한이 거부됩니다.
C. 그룹 멤버는 다중 요소 인증(MFA)으로 로그인한 경우 모든 리전에 대해 ec2:StopInstances 및 ec2:TerminateInstances 권한이 허용됩니다. 그럴 때만 다른 모든 Amazon EC2 작업이 허용됩니다.
D. 그룹 멤버는 멀티팩터 인증(MFA)으로 로그인한 경우에만 us-east-1 지역에 대한 ec2:StopInstances 및 ec2:TerminateInstances 권한이 허용됩니다. 그룹 멤버는 us-east-1 지역 내에서 다른 모든 Amazon EC2 작업이 허용됩니다.


3. 한 회사가 Amazon S3 버킷으로 데이터를 마이그레이션하려고 계획하고 있습니다.
요구 사항:
- 데이터는 S3 버킷 내에서 휴면 상태로 암호화되어야 함
- 암호화 키는 매년 자동으로 순환되어야 함

어떤 솔루션이 가장 적은 운영 오버헤드로 이러한 요구 사항을 충족할까요?

A. S3 버킷으로 데이터를 마이그레이션합니다. Amazon S3 관리 키(SSE-S3)로 서버 측 암호화를 사용합니다.

B. AWS Key Management Service(AWS KMS) 고객 관리 키를 만듭니다. 자동 키 로테이션을 활성화합니다. S3 버킷의 기본 암호화 동작을 고객 관리 KMS 키를 사용하도록 설정합니다. 데이터를 S3 버킷으로 마이그레이션합니다.

C. AWS Key Management Service(AWS KMS) 고객 관리 키를 만듭니다. S3 버킷의 기본 암호화 동작을 고객 관리 KMS 키를 사용하도록 설정합니다. 데이터를 S3 버킷으로 마이그레이션합니다. 매년 KMS 키를 수동으로 순환합니다.

D. 고객 키 자료를 사용하여 데이터를 암호화합니다. 데이터를 S3 버킷으로 마이그레이션합니다. 키 자료 없이 AWS Key Management Service(AWS KMS) 키를 만듭니다. 고객 키 자료를 KMS 키로 가져옵니다. 자동 키 로테이션을 활성화합니다.

4. 한 회사에는 Amazon RDS for MySQL DB 클러스터의 데이터베이스에서 정보를 검색하는 임베디드 자격 증명이 있는 사용자 지정 애플리케이션이 있습니다. 이 회사는 최소한의 프로그래밍 노력으로 애플리케이션을 더 안전하게 만들어야 합니다. 이 회사는 애플리케이션 사용자를 위해 RDS for MySQL 데이터베이스에 자격 증명을 만들었습니다.

어떤 솔루션이 이러한 요구 사항을 충족할까요?

A. AWS Key Management Service(AWS KMS)에 자격 증명을 저장합니다. AWS KMS에 키를 만듭니다. AWS KMS에서 데이터베이스 자격 증명을 로드하도록 애플리케이션을 구성합니다. 자동 키 로테이션을 활성화합니다.

B. 암호화된 로컬 저장소에 자격 증명을 저장합니다. 로컬 저장소에서 데이터베이스 자격 증명을 로드하도록 애플리케이션을 구성합니다. Cron 작업을 생성하여 자격 증명 로테이션 일정을 설정합니다.

C. AWS Secrets Manager에 자격 증명을 저장합니다. Secrets Manager에서 데이터베이스 자격 증명을 로드하도록 애플리케이션을 구성합니다. Secrets Manager에 대한 AWS Lambda 함수를 생성하여 자격 증명 로테이션 일정을 설정합니다.

D. AWS Systems Manager Parameter Store에 자격 증명을 저장합니다. Parameter Store에서 데이터베이스 자격 증명을 로드하도록 애플리케이션을 구성합니다. Parameter Store를 사용하여 RDS for MySQL 데이터베이스에 자격 증명 로테이션 일정을 설정합니다.

5. 한 회사가 Amazon Aurora MySQL DB 클러스터를 스토리지로 사용하는 다중 계층 웹 애플리케이션을 호스팅합니다.
애플리케이션 계층은 Amazon EC2 인스턴스에서 호스팅됩니다.

회사의 IT 보안 지침:

- 데이터베이스 자격 증명은 암호화되어야 함
- 14일마다 순환되어야 함

솔루션 아키텍트는 최소한의 운영 노력으로 이 요구 사항을 충족하기 위해 무엇을 해야 합니까?

A. 새로운 AWS Key Management Service(AWS KMS) 암호화 키를 만듭니다. AWS Secrets Manager를 사용하여 적절한 자격 증명과 함께 KMS 키를 사용하는 새로운 비밀을 만듭니다. 비밀을 Aurora DB 클러스터와 연결합니다. 14일의 사용자 지정 로테이션 기간을 구성합니다.

B. AWS Systems Manager Parameter Store에 두 개의 매개변수를 만듭니다. 하나는 문자열 매개변수로 사용자 이름을 위한 매개변수이고 다른 하나는 암호에 SecureString 유형을 사용합니다. 암호 매개변수에 AWS Key Management Service(AWS KMS) 암호화를 선택하고 애플리케이션 계층에 이러한 매개변수를 로드합니다. 14일마다 암호를 순환하는 AWS Lambda 함수를 구현합니다.

C. 자격 증명이 포함된 파일을 AWS Key Management Service(AWS KMS) 암호화된 Amazon Elastic File System(Amazon EFS) 파일 시스템에 저장합니다. 애플리케이션 계층의 모든 EC2 인스턴스에 EFS 파일 시스템을 마운트합니다. 파일 시스템에서 파일에 대한 액세스를 제한하여 애플리케이션이 파일을 읽을 수 있고 슈퍼 사용자만 파일을 수정할 수 있도록 합니다. 14일마다 Aurora에서 키를 순환하고 새 자격 증명을 파일에 쓰는 AWS Lambda 함수를 구현합니다.

D. 애플리케이션이 자격 증명을 로드하는 데 사용하는 AWS Key Management Service(AWS KMS) 암호화된 Amazon S3 버킷에 자격 증명이 포함된 파일을 저장합니다. 올바른 자격 증명이 사용되도록 정기적으로 애플리케이션에 파일을 다운로드합니다. 14일마다 Aurora 자격 증명을 순환하고 이러한 자격 증명을 S3 버킷의 파일에 업로드하는 AWS Lambda 함수를 구현합니다.
