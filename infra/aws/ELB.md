# ELB란? (Elastic Load Balancer)

: 트래픽(부하)를 적절하게 분배해주는 장치이다.

트래픽을 적절하게 분배해주는 장치를 보고 전문적인 용어로 로드밸런서라고 부른다. 서버를 2대 이상 가용할 때 ELB를 필수적으로 도입하게 된다.

![](https://blog.lael.be/wp-content/uploads/2019/07/aws-elb.jpg)

ELB도 ELB만의 IP주소가 있다. 하나의 컴퓨터임. ELB를 통해서 사용자를 보내야, 트래픽을 조절할 수 있다.

- ELB의 부가기능으로, HTTP를 HTTPS로 적용시키는 것이 있다

# TLS/SSL/HTTPS

## SSL/TLS란?

: HTTP를 HTTPS로 바꿔주는 인증서이다.

HTTP는 암호화를 시키지 않고 통신을 하기 때문에 중간에서 데이터를 가로채서 해킹할 수 있다.
