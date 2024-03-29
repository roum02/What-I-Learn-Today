## map

> A map object is a collection consisting of key-value pairs. 

Map object is similar to an object, but there are some differences as outlined below.
![img.png](images/map.png)

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