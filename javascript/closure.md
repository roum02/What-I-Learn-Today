## 클로저(Closure)

> [스코프](#스코프)를 이해하지 못했다면, 이해하고 오자.

클로저는 자바스크립트에서 중요한 개념 중의 하나이다. <br />
자바스크립트의 고유의 개념이 아니라, 함수를 일급 객체로 취급하는 함수형 프로그래밍 언어에서 사용되는 중요한 특성이다.

> 함수 객체와 스코프를 조합한 것을 클로저라고 한다.


### 1. 클로저 예시

```js
function outerFunc() {
  var x = 10;
  var innerFunc = function () { console.log(x); };
  innerFunc();
}

outerFunc(); // 10
```

innerFunc은 내부함수이므로 자신을 포함하고 있는 outerFunc의 렉시컬 스코프에 참조할 수 있다. <br/>
따라서 변수 x에 접근할 수 있다. 


```js
function outerFunc() {
  var x = 10;
  var innerFunc = function () { console.log(x); };
  return innerFunc;
}

var inner = outerFunc();
inner(); // 10
```

outerFunc의 life-cycle은 종료되었고, 변수 x에 접근할 방법은 없다. <br/>
그럼에도 코드의 실행 결과는 10이다. <br/>

따라서 클로저는 다음과 같이 설명할 수 있겠다.

> 클로저는 반환된 내부함수가 **자신이 선언되었을 때의 환경(Lexical environment)인 스코프**를 기억하여,<br/>
자신이 선언되었을 때의 환경 밖에서 호출되어도<br/>
그 환경에 접근할 수 있는 함수를 말한다.
> (그래서 클로저 closure(닫힘) 이다.)

이때, 내부함수가 외부함수의 변수의 복사본이 아닌 실제 변수에 접근한다는 것에 주의하자.


### 2. 클로저의 활용

자신의 생성될 때의 환경을 기억한다면, 메모리 차원에서 손해를 볼 수 있다. <br />
그럼에도 불구하고 이는 자바스크립트의 강력한 기능으로 사용될 수 있다.

<details>
    <summary>자세히</summary>

#### 2.1 상태 유지
클로저를 이용하여 현재 상태를 기억하고, 변경된 최신 상태를 유지할 수 있다.
```js
 var box = document.querySelector('.box');
    var toggleBtn = document.querySelector('.toggle');

    var toggle = (function () {
      var isShow = false;

      // ① 클로저를 반환
      return function () {
        box.style.display = isShow ? 'block' : 'none';
        // ③ 상태 변경
        isShow = !isShow;
      };
    })();

    // ② 이벤트 프로퍼티에 클로저를 할당
    toggleBtn.onclick = toggle;ß
```

#### 2.2 전역 변수의 사용 억제, 정보의 은닉
전역변수는 언제든지 누구나 변경이 가능하다. 이는 의도치 않게 값이 변경될 수 있다는 것을 의미한다. <br />
클로저는 변수를 private하게 만들어, 의도치 않은 변경을 저지할 수 있다.
```js
var incleaseBtn = document.getElementById('inclease');
    var count = document.getElementById('count');

    var increase = (function () {
      var counter = 0;
      return function () {
        return ++counter;
      };
    }());

    incleaseBtn.onclick = function () {
      count.innerHTML = increase();
    };
```

#### 2.3 자주 발생하는 실수

```js
var arr = [];

for (var i = 0; i < 5; i++) {
  arr[i] = function () {
    return i;
  };
}

for (var j = 0; j < arr.length; j++) {
  console.log(arr[j]()); // 5 5 5 5 5
}
```
i가 전역변수이기 때문에 발생하는 문제이다. 클로저를 사용하면 다음과 같이 고칠 수 있다.
```js
var arr = [];

for (var i = 0; i < 5; i++){
  arr[i] = (function (id) { // ②
    return function () {
      return id; // ③
    };
  }(i)); // ①
}

for (var j = 0; j < arr.length; j++) {
  console.log(arr[j]());
}
```
① 배열 arr에는 즉시실행함수에 의해 함수가 반환된다.

② 이때 즉시실행함수는 i를 인자로 전달받고 매개변수 id에 할당한 후 내부 함수를 반환하고 life-cycle이 종료된다. 매개변수 id는 자유변수가 된다.

③ 배열 arr에 할당된 함수는 id를 반환한다. 이때 id는 상위 스코프의 자유변수이므로 그 값이 유지된다.

(사실 let 키워드를 사용하면 더 쉽게 해결할 수 있다)

</details>



### 마무리

엄밀히 말해 자바스크립트 함수는 모두 클로저이다.<br/>
다만 대부분의 함수가 자신이 정의된 곳과 같은 스코프에서 호출되므로 보통 클로저인지 여부를 따질 필요가 없는데,
함수가 유용할 때는 함수가 정의된 곳과 다른 스코프에서 호출될 때 뿐이다.
