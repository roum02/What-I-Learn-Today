### 스코프 (Scope)

> [실행 컨텍스트]()를 모른다면 이해하고 오자.
>
> [식별자](variable.md)를 모른다면 이해하고 오자.

스코프란 자바스크립트 엔진이 참조의 대상이 되는 식별자(Identifier)를 검색할 때 사용하는 규칙의 집합이다.
식별자가 유효한 범위를 말한다.

<details>
    <summary>자세히</summary>

    프로그래밍은 변수를 선언하고, 값을 할당한다. 변수는 전역 또는 코드 블록이나 함수 내에 선언될 수 있다. 식별자는 자신이 어디에서 선언되었는지에 의해 참조될 수 있는 범위를 갖는다.
    전역변수 x는 어디서든 참조할 수 있지만, 함수 내부 변수는 함수에서만 참조가 가능하다.
    이와 같은 규칙을 스코프라고 한다.
</details>

### 스코프 체인

함수가 중첩되기 때문에, 스코프는 계층구조를 지닌다. 스코프가 계층으로 연결된 것을 스코프 체인이라고 한다.

변수 참조 시 자바스크립트 엔진은 상위 스코프 방향으로 이동하며 변수를 검색한다.

상위 스코프에서 유효한 변수는 하위 스코프에서 자유롭게 참조 가능하나, 하위 스코프에서 유효한 변수를 상위 스코프에서 참조 불가능하다.


### 동적 스코프 / 렉시컬 스코프(정적 스코프)

- 동적 스코프: 함수를 어디서 호출했는지가 함수의 상위 스코프 결정

- 정적 스코프: 함수를 어디서 정의했는지가 함수의 상위 스코프 결정 -> 자바스크립트 해당

### 클로저와 useState

- useState hook은 함수형 컴포넌트의 상태 관리 문제를 클로저로 해결한다.

```javascript
const useState = (initialValue) => {
  let value = initialValue;
  
  const state = () => value; //  이 함수는 호출될 때 현재 상태(value)를 반환

  const setState = (newValue) => {
    value = newValue;
  };
  
  return [state, setState];
};


const [counter, setCounter] = useState(0);

console.log(counter()); // 0
setCounter(1);
console.log(counter()); // 1
```

해당 코드에서는 state가 함수이기 때문에, 최신의 value값을 반환받을 수 있다.
다만, useState hook의 state는 getter함수이기 때문에, 변수로 바꿔보자면 다음과 같다.

```javascript
const useState = (initialValue) => {
  let state = initialValue; // 초기 상태값을 저장하는 변수

  const setState = (newValue) => {
    state = newValue; // 상태값을 업데이트하는 함수
  };
  
  return [state, setState];
};


const [counter, setCounter] = useState(0);

console.log(counter); // 0
setCounter(1);
console.log(counter); // 0 → Error!
```
해당 코드에서 state는 setState를 통해서 값이 업데이트 되지만,
업데이트 된 변수의 값이 counter에 반영이 되지는 않는다.


```javascript
const MyReact = (function () {
  let state;

  return {
    render(Component) {
      const Comp = Component();
      Comp.render();
      return Comp;
    },

    useState(initialValue) {
      state ||= initialValue;

      const setState = (newValue) => {
        state = newValue;
      };

      return [state, setState];
    },
  };
})();

const Counter = () => {
  const [count, setCount] = MyReact.useState(0);

  return {
    click: () => setCount(count + 1),
    render: () => console.log('render:', { count }),
  };
};

let App;
App = MyReact.render(Counter); // render: { count: 0 }
App.click();
App = MyReact.render(Counter); // render: { count: 1 }

```

state가 useState의 외부 스코프에 선언되어,
외부 스코프의 state를 변경하게 된다.
클로저의 원리에 따라 state 값은 사라지지 않는다.