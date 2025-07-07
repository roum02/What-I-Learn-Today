1. 클래스 상속과 생성자 함수 상속의 차이
   : 프로토타입 상속은 프로토타입 체인을 통해 다른 객체의 자산을 상속
   상속에 의한 클래스 확장은 기존 클래스를 상속받아 새로운 클래스를 확장하여 정의하는 것

2. 접근자 프로퍼티란?
   : 자체적으로는 값을 갖지 않고, 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 사용하는 접근자 합수로 구성된 프로퍼티이다.
   getter, setter

```
class Person {
  constructor(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  }

  // getter 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }

  // setter 함수
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ');
  }
}

const me = new Person('Ungmoo', 'Lee');

// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
me.fullName = 'Heegun Lee';
console.log(me); // { firstName: "Heegun", lastName: "Lee" }
```

접근자 프로퍼티는 호출하는 것이 아니라, 프로퍼티처럼 참조하는 형식으로 사용되며, 참조 시에 내부적으로 호출된다.

https://ko.javascript.info/class
