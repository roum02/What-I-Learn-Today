### Getter & Setter

> 1) Getter는 객체의 속성(property) 값을 반환하는 메서드 
> 2) Setter는 객체의 속성 값을 설정, 변경하는 메서드
> 

### 예시

```javascript
const user = {
	name: 'name',
    age: 50
}

console.log(user.name); // inpa

user.name = 'userName';
```

user.name의 값을 바로 변경하지 않고,
getName(), setName() 메서드를 통해 경유해서 설정하도록 하는 기법

```javascript
const user = {
	name: 'name',
    age: 50,
    
    // 객체의 메서드(함수)
    getName() {
    	return user.name;
    },
    setName(value) {
    	user.name = value;
    }
}

console.log(user.getName()); // name

user.setName('userName');
```

### 활용하기
1. 객체 내부 속성에 직접 접근하지 않아 객체의 정보 은닉이 가능하다.
2. 코드의 안전성과 유지보수성을 높일 수 있다. 
2. 옳지 않은 값을 넣는 것을 방지할 수 있다.


### ES6
ES6 최신 자바스크립트부터는 Getter와 Setter를 객체 리터럴 안에서 속성 이름 앞에 

get 또는 set 키워드만 붙여 Getter와 Setter를 정의할 수 있다.

```javascript
const user = {
	name: 'name',
    age: 50,
    
    // userName() 메서드 왼쪽에 get, set 키워드만 붙이면 알아서 Getter, Setter 로서 동작된다
    get userName() {
    	return user.name;
    },
    set userName(value) {
    	user.name = value;
    }
}
```

