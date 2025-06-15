### 생성자 함수

생성자 함수란 **new 키워드와 함께** 객체를 생성하고 초기화하는 함수를 말한다.<br/>
생성자 함수를 통해 생성된 객체를 인스턴스(instance)라고 한다.

```
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.sayHello = function () {
    console.log(`Hi, I'm ${this.name} and I'm ${this.age} years old.`);
  };
}

const p1 = new Person("Alice", 25);
p1.sayHello(); // Hi, I'm Alice and I'm 25 years old.

console.log(typeof p1);     // "object"
console.log(p1 instanceof Person); // true

```

c.f. 빌트인 생성자 함수
: ECMAScript 사양에 정의된 표준 빌트인 객체 중에서,
new 키워드를 사용하여 새로운 인스턴스 객체를 생성할 수 있도록 설계된 함수 객체를 말합니다.

자바스크립트에서는 Object, String, Array 등 약 40여 개의 표준 빌트인 객체를 제공합니다.
이 중 Math, Reflect, JSON, Atomics, Intl, WebAssembly 등 일부는 생성자 함수가 아니며 인스턴스를 만들 수 없습니다.
나머지 대부분의 표준 빌트인 객체는 생성자 함수 형태로 정의되어 있으며, new 키워드를 사용해 인스턴스를 생성할 수 있습니다.

- 자바스크립트의 평범한 함수는 생성자 함수가 될 수 있을까?
  : 자바스크립트에서 함수 선언문이나 함수 표현식으로 정의한 일반 함수는new와 함께 호출되면 생성자 함수로 작동합니다.
  즉, 함수 자체가 특별한 “생성자용 문법”을 따로 가져야 하는 게 아니라,new 키워드가 붙었느냐에 따라 동작 방식이 달라집니다.

```
function greet(name) {
this.name = name;
this.sayHello = function () {
console.log(`Hello, ${this.name}`);
};
}

// 일반 함수로 호출
greet("Alice"); // this는 전역객체(window/global) 또는 undefined (strict mode)

// 생성자 함수로 호출
const g = new greet("Bob");
g.sayHello(); // Hello, Bob
```

## 생성자 함수의 인스턴스 생성 과정

new 연산자와 함께 생성자 함수를 호출하면 자바스크립트 엔진은 다음과 같은 과정을 거쳐 암묵적으로 인스턴스를 생성하고 인스턴스를 초기화한 후 암묵적으로 인스턴스를 반환한다.

이러한 암묵적인 과정이 있기 때문에, 생성자 함수에서는 return을 생략해야 한다.

### 1. 인스턴스 생성과 this 바인딩

c.f. 바인딩 : 바인딩이란 식별자와 값을 연결하는 과정을 의미한다. 예를 들어, 변수 선언은 이름(식별자)와 확보된 메모리 공간의 주소를 바인딩하는 것이다.

### 2. 인스턴스 초기화

### 3. 인스턴스 반환
