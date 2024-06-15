## map

> A map object is a collection consisting of key-value pairs. 

Map object is similar to an object, but there are some differences as outlined below.
![](https://velog.velcdn.com/images/roum02/post/abc947b1-cd7f-4fe9-8873-b42f10929b83/image.png)

### generating a map object

Map object can create a generator function of Map.

```javascript
const map = new Map();
console.log(map) // Map(0)
```

the generator function of a Map creates the Map object using an iterable,
Which in this case is composed of key-value pairs.

> What is iterable?
> 
> In JavaScript, an iterable must implement the iterable protocol, which means it needs to provide a function that returns an iterator. Common examples of iterables include arrays, strings, and Map objects.

[if you want to see more information, click here](https://inpa.tistory.com/entry/JS-%F0%9F%93%9A-%EC%9D%B4%ED%84%B0%EB%9F%AC%EB%B8%94-%EC%9D%B4%ED%84%B0%EB%A0%88%EC%9D%B4%ED%84%B0-%F0%9F%92%AF%EC%99%84%EB%B2%BD-%EC%9D%B4%ED%95%B4)


```javascript
const map1 = new Map([['key1', 'value1'],['key2', 'value2']]);
console.log(map1) // Map(2) {"key1" => "value1", "key2" => "value2" }
```

if there are duplicate keys in the iterable, they will be overwritten. 
That is why a Map object doesn't have duplicate keys.


### properties for a Map

- size

it can check the amounts of elements in a Map.
it has only a getter function without setter function, 
so that is can not be replaced the value.

- set

it uses adding an element in a Map.

```javascript
let max = new Map();

// map
max.set('id', 0);
max.set('이름', '마이클');
max.set('전공', '영문학');
max.set('나이', 25);

// get
max.get('이름'); // "마이클"

// delete
max.delete('나이'); // true

// clear
max.clear();

```

