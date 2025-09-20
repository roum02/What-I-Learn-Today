## 몰랐던 개념

### 스토리지

![](https://cdn.imweb.me/upload/S202001291023ba77fb258/e6131cf5b2abd.png)

### 블록 스토리지

: 블록 스토리지는 정보를 고정 크기의 블록으로 나누는 데이터 스토리지 유형을 의미합니다. 각 블록에는 고유한 번호가 할당되어 AWS 블록 스토리지나 Azure 블록 스토리지 같은 클라우드 플랫폼이 데이터를 효율적으로 접근하고 관리할 수 있습니다.

클라우드 환경에서 블록 스토리지 각 블록은 가상 머신 인스턴스에 위치한다.

서버와 스토리지 장비가 물리적으로 분리되어 있을 때, SAN(Storage Area Network)이 두 영역을 연결해 줍니다.

c.f. AWS EBS

### 파일 스토리지

파일과 폴더의 계층구조로 이루어진 방식이다.

데이터가 많아지면 파일과 폴더를 찾기위한 리소스가 많이 소요되어 성능이 저하된다.

파일 스토리지는 NAS에 사용된다.

c.f. AWS EFS

### 객체 스토리지

오브젝트라는 개별 데이터 단위로 데이터를 저장하는 유형이다. 파일 스토리지와는 다르게 계층 구조 없이 평면 구조로 데이터를 저장한다.

c.f. AWS S3

### S3의 스토리지 클래스

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FIHxL8%2FbtsFmmDh9di%2FAAAAAAAAAAAAAAAAAAAAAFbsPCdsExnVks-O3NSm99bp238Ruo7tXaonamAdCkkG%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1759244399%26allow_ip%3D%26allow_referer%3D%26signature%3DotkMHTqD278u58J5CPsdzIXBAL4%253D)

각 스토리지 클래스 간 이동이 가능함.
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FbR05sT%2Fbtr4LGPR1zd%2FAAAAAAAAAAAAAAAAAAAAAAZQCfDAY87bgmXgCE40_BquoUC2KdwJF81CJelSGyEf%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1759244399%26allow_ip%3D%26allow_referer%3D%26signature%3DTH7V0UN6OqwqPyjwXdIc%252Fw4f4r4%253D)

## AWS SNS vs SQS

![](https://cdn.maily.so/ojdy4c893tt760t7eow4b2ic8fv2)

---

## 문제 추가 풀면서 새로 알았던 개념 정리
