### 스코프 (Scope)

> [실행 컨텍스트]()를 모른다면 이해하고 오자.
>
> [식별자]()를 모른다면 이해하고 오자.

스코프란 자바스크립트 엔진이 참조의 대상이 되는 식별자(Identifier)를 검색할 때 사용하는 규칙의 집합이다.

<details>
    <summary>자세히</summary>

    프로그래밍은 변수를 선언하고, 값을 할당한다. 변수는 전역 또는 코드 블록이나 함수 내에 선언될 수 있다. 식별자는 자신이 어디에서 선언되었는지에 의해 참조될 수 있는 범위를 갖는다.
    전역변수 x는 어디서든 참조할 수 있지만, 함수 내부 변수는 함수에서만 참조가 가능하다.
    이와 같은 규칙을 스코프라고 한다.
</details>
