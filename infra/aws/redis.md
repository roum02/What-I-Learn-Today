# Redis 란

![](https://picturesque-staircase-f6e.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fcb949b7b-7dd8-4f60-8762-5f9522635195%2F6ae01967-a3db-4a7d-a786-bce300f7c008%2FUntitled.png?table=block&id=11b89d65-50dd-4574-ac3a-fc1523a42362&spaceId=cb949b7b-7dd8-4f60-8762-5f9522635195&width=670&userId=&cache=v2)

1. 관계형 데이터베이스(RDS)
   ![](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F992ECA335BE148210D)
2. Redis
   : [Key]:value 값으로 데이터를 간결하게 저장함

- 간단한 데이터라면, 굳이 구조화된 관계형 데이터 베이스에 저장할 필요는 없음.
- 그리고 Redis는 >>>고성능(매우중요)<<<임. 많은 요청이 들어오는 요청일 경우에, 레디스는 최적의 성능을 낼 수 있음.
- 주로 캐싱, 인증 관리, DB동시성 제어 등에서 다양한 목적으로 사용

## 레디스의 주요 특징

- key-value로 구성된 단순화된 데이터 구조로 sql 쿼리 사용 불필요
  c.f. sql 쿼리는 RDB에서 사용하는데, 꽤 복잡도가 높다.
- 빠른 성능
  - 인메모리 NoSql 데이터베이스이기 때문에 성능이 빠르다
    c.f. 인메모리? : 컴퓨터는 Storage(Hard disk), Rem, CPU 중 스토리지에 데이터를 저장함. 기본적으로 스토리지는 메모리에 비해 가격이 저렴하고 성능이 떨어짐. 하지만 Rem은 임시기억장치로서 비용이 비싸고 속도가 빠름. 레디스는 이런 메모리 기반의 동작을 한다.
  - rdb는 기본적으로 disk에 저장이고 필요시에 메모리에 캐싱하는 것이므로, rdb보다 훨씬 빠른 성능
    c.f. 관계형데이터베이스의 경우에는 스토리지를 기반으로 저장하기 때문에 필요에 따라 일부 Rem을 활용하기도 함.
    그런데 레디스는 메모리에 데이터를 올려두고, 주기적으로 스냅샷 Disk에 저장한다. 메모리는 사실 컴퓨터를 한 번 껐다가 키면 다 날라가는뎅.., 그럼에도 불구하고 운영 가능한 이유는 주기적으로 스냅샷을 찍기 때문.
- key-value는 구조적으로 해시 테이블을 사용함으로서 매우 빠른 속도로 데이터 검색 가능
- Single Thread 구조로 동시성 이슈 발생X
  - 보통의 DB는 여러 요청을 동시에 처리해주는걸 지원해줌. 이 과정에서 데이터 무결성에 이슈가 생기기도 한다.
    그런데 레디스는 싱글스레드라서 한 번에 한 요청밖에 처리하지 않음.
- 윈도우 서버에서는 지원하지 않고, linux서버 및 macOS등에서 사용 가능
