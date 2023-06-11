### 객체 생성 방법

> [생성자 함수](constructor.md)를 모른다면, 먼저 이해하고 오자.

자바스크립트는 프로토타입 기반 객체 지향 언어로, 클래스라는 개념이 없고 별도의 객체 생성 방법이 존재한다. <br/>
*es6에서 새롭게 클래스가 도입되었다.*


#### 2.1 객체 리터럴
중괄호를 사용하여 객체를 생성하는 방법이다.

```javascript
var emptyObject = {};
console.log(typeof emptyObject); // object
```

### 2.2 Object 생성자 함수
new 연산자와 Object 생성자 함수를 호출하여 빈 객체를 생성할 수 있다.

사실 객체 리터럴 방식은 Object 생성자 함수의 축약 표현이다.
(보통의 개발자라면 일부러 생성자 함수를 이용하여 객체를 생성해야 할 일은 거의 없다.)
```javascript
// 빈 객체의 생성
var person = new Object();

// 프로퍼티 추가
person.name = 'Lee';
person.gender = 'male';
```

