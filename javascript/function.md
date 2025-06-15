# 자바스크립트 함수의 이해

## 1. 함수는 객체의 특별한 형태

- 자바스크립트 함수는 일반 객체의 하위 타입으로, 호출 가능한(callable) 특별한 객체입니다.
- 함수 객체는 일반 객체가 가진 프로퍼티 외에도 함수 실행을 위한 내부 데이터와 메서드를 갖고 있습니다.

### 함수 객체가 내부에 저장하는 주요 데이터

| 내부 데이터         | 설명                                                  |
| ------------------- | ----------------------------------------------------- |
| [[Environment]]     | 함수가 선언된 렉시컬 환경 (클로저 생성의 근간)        |
| [[ECMAScriptCode]]  | 함수 내부의 실행 코드                                 |
| [[FunctionKind]]    | 함수 종류 (일반, 클래스 생성자, 제너레이터, async 등) |
| [[ConstructorKind]] | 생성자 종류 (기본, 파생)                              |
| [[ThisMode]]        | this 참조 방식                                        |
| [[Strict]]          | 엄격 모드 여부                                        |
| [[HomeObject]]      | super 참조 객체                                       |

---

## 2. 함수의 핵심 내부 메서드: [[Call]]과 [[Construct]]

- 함수 객체는 다음 두 가지 특별한 내부 메서드를 가집니다.

| 내부 메서드   | 설명                                                  |
| ------------- | ----------------------------------------------------- |
| [[Call]]      | 일반 함수 호출 시 실행 (ex: `func()`)                 |
| [[Construct]] | `new` 키워드로 생성자 호출 시 실행 (ex: `new Func()`) |

- [[Call]]이 구현된 객체는 **callable(호출 가능)** 객체라고 합니다.
- [[Construct]]가 구현된 객체는 **constructor(생성자)** 역할을 하는 함수입니다. [[Construct]]를 가진 객체는 constructor이라고 하고, 가지지 않았다면, non-constructor 이라고 합니다.

일반 함수로서 호출되면 함수 객체의 내부 메서드 [[Call]]이 호출되고, new 연산자와 함께 생성자 함수로 호출되면 [[Construct]] 가 호출된다.

---

## 3. callable과 constructor 차이

- 모든 함수는 callable하지만, 모든 함수가 constructor는 아닙니다.
- 예를 들어, **화살표 함수는 호출 가능(callable)하지만 생성자(new 호출)로는 사용할 수 없습니다.**

![](https://blog.kakaocdn.net/dn/ciaDIb/btrtjP38UzH/EfIcijWUwZ03p8gLEcCW7k/img.png)

- constructor: 함수 선언문, 함수 표현식, 클래스
- non-constructor: 메서드, 화살표함수

```javascript
function normalFunc() {
  console.log("일반 함수 호출");
}

const arrowFunc = () => {
  console.log("화살표 함수 호출");
};

normalFunc();   // 정상 호출
arrowFunc();    // 정상 호출

new normalFunc(); // 가능 (constructor)
new arrowFunc();  // TypeError: arrowFunc is not a constructor

## new 연산자

일반 함수와 생성자 함수에 특별한 형식적 차이는 없다. new 연산자와 함께 함수를 호출하면 해당 함수는 생성자 함수로 동작한다.


```

// 생성자 함수로 정의하지 않은 일반 함수
function add(x, y) {
return x + y;
}

// 일반 함수에 new 연산자를 붙여 호출
let inst = new add(); // 반환값이 없으므로 빈 객체가 반환됨
console.log(inst); // {}

```

```

// 생성자 함수
function Circle(radius) {
this.radius = radius;
this.getDiameter = function () {
return 2 \* this.radius;
};
}

// new 연산자 없이 생성자 함수 호출 → 일반 함수처럼 실행됨
const circle = Circle(5);

// 암묵적으로 다음과 같이 실행됨
window.radius = 5;
window.getDiameter = function () {
return 2 \* this.radius;
};

```

## 함수 선언문은 표현식이 아닌 문(statement)이다

### 표현식과 문(statement)의 차이

- **문(statement)**: 실행 가능한 최소 단위 코드로, 보통 독립적인 실행 단위입니다.
- **표현식(expression)**: 값으로 평가될 수 있는 코드 조각입니다.

### 함수 선언문이 문인 이유와 생성 시점 차이

| 구분         | 함수 선언문                            | 함수 표현식                              |
|------------|---------------------------------|-------------------------------------|
| 종류         | 문(statement)                       | 표현식(expression)                    |
| 생성 시점      | 런타임 이전에 자바스크립트 엔진이 함수 전체를 메모리에 미리 올려놓음 | 런타임에 코드 실행 흐름이 해당 위치에 도달해야 함수 객체 생성 |
| 변수 할당      | 함수 이름과 동일한 식별자에 자동 할당         | 변수에 함수 객체가 할당됨                |
| 호출 가능 시점   | 선언 이전에도 호출 가능 (호이스팅)             | 할당 이전 호출 시 undefined 또는 에러 발생  |
| 문법적 특성     | 독립적인 선언 구조                      | 값 생성 및 할당의 일부                   |

### 이유

1. 함수 선언문은 문법적으로 독립적이고, 스코프 시작 시 엔진이 미리 메모리에 올려 함수 이름과 코드를 같이 준비합니다.
2. 함수 표현식은 변수에 값을 할당하는 문장의 일부로, 실행 흐름에 따라 함수 객체가 만들어지고 할당됩니다.

---

## Function 생성자 함수가 클로저를 생성하지 않는 이유

- `Function` 생성자는 **문자열로 전달된 코드를 런타임에 새로운 함수 객체로 생성**합니다.
- 생성된 함수는 **함수가 정의된 시점의 렉시컬 환경을 참조하지 않고 항상 전역 객체(global scope)를 참조**합니다.
- 즉, `Function` 생성자는 내부적으로 `eval`과 비슷하게 동작하며, 현재 실행 중인 함수의 렉시컬 환경과는 분리된 전역 환경에서 코드를 실행합니다.
- 따라서, `Function` 생성자는 **클로저를 생성하지 않습니다**.

### 참고

- `Function` 생성자 함수는 매개변수 수가 0개일 때 이상적입니다.
- 매개변수를 문자열로 여러 개 전달할 수도 있지만, 가독성 및 유지보수 측면에서 권장하지 않습니다.

---

```
