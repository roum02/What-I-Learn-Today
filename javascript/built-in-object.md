# 자바스크립트 원시값 vs 객체 (래퍼 객체)

## 🎯 핵심 개념: 래퍼 객체 (Wrapper Object)

**래퍼 객체란?**

- 원시 값을 객체처럼 사용할 때 자동으로 생성되는 임시 객체
- 메서드 호출이나 속성 접근 시 자바스크립트 엔진이 자동 변환
- 사용 후 즉시 가비지 컬렉션으로 제거 (재사용 ❌)

---

## 📊 래퍼 객체 종류

| 원시 타입 | 래퍼 객체 |
| --------- | --------- |
| `string`  | `String`  |
| `number`  | `Number`  |
| `boolean` | `Boolean` |
| `bigint`  | `BigInt`  |
| `symbol`  | `Symbol`  |

---

## 🔍 1. 타입 확인

```javascript
// 원시값 vs 객체
typeof "hello"; // "string"
typeof new String("hello"); // "object"
```

---

## ⚖️ 2. 비교 연산

```javascript
const str1 = "hello"; // 원시값
const str2 = new String("hello"); // 객체

// 느슨한 비교 (값만 비교)
str1 == str2; // true ✅
// 자동 형변환으로 값만 비교

// 엄격한 비교 (타입 + 값)
str1 === str2; // false ❌
// string vs object 타입이 다름
```

---

## 🔧 3. 메서드 호출 (Auto-boxing)

```javascript
const primitive = "hello"; // 원시값
const object = new String("hello"); // 객체

// 둘 다 동일하게 작동
console.log(primitive.toUpperCase()); // "HELLO"
console.log(object.toUpperCase()); // "HELLO"
```

**동작 원리:**

- `primitive`: 임시로 String 객체로 감싸서(auto-boxing) 메서드 사용
- `object`: 이미 객체이므로 바로 메서드 사용

---

## 💡 권장사항

### ✅ 권장: 원시값 사용

```javascript
const name = "JavaScript"; // 좋음
const age = 25; // 좋음
```

### ❌ 비권장: 객체 생성자 사용

```javascript
const name = new String("JavaScript"); // 피하기
const age = new Number(25); // 피하기
```

**이유:**

- 메모리 효율성 ⬆️
- 성능 최적화 ⬆️
- 예측 가능한 동작
- 타입 안전성 보장

---

## 🚨 주의사항

1. **의도치 않은 객체 생성 방지**
2. **타입 체크 시 혼동 방지**
3. **성능 최적화를 위한 원시값 사용**
4. **레거시 코드나 특수한 경우에만 래퍼 객체 사용**
