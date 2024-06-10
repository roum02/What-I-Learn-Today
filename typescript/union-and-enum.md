we usually use Enum or union type using typescript.

they are defined sets of values in programming, but they serve different purposes.

Today, we are going to find out about these.

![](https://velog.velcdn.com/images/roum02/post/bfaf23b9-8edd-4817-abd7-74672d5aa8df/image.png)



we can make a similar type using those two type.

#### union type
a union type is a type can hold one of several types.
> type DeviceType = "phone" | "pad" | "deskTop"


#### enum
An enumm defines a set of named values.
> enum DeviceType {
phone="phone",
pad="pad",
deskTop="deskTop"
}


### what is the difference between them?

1. Enum is impossible to extend. if we need to combine types, we should use union type.
```
enum Fruit {
APPLE,
BANANA
}

enum AnotherFruit{
PINEAPPLE
}

type Fruit = Fruit | AnotherFruit
```

2. Enum can not allocate the value directly.

```
enum Fruit {
APPLE = 'APPLE',
BANANA = "BANANA"
}

getSomeFruit('APPLE') // X
getSomeFruit(Fruit.APPLE) // O
```

3. Numberic enum in enum is not guarantee type stability.

```
enum Status{
pedding=0,
success=1,
fail=2
}

const newStatus: Status = 100; // none error here..
```

4. The size of an enum is larger than that of a union type.


#### In most cases, an Enum can be replaced by union type.

and an Enum an be replaced by object also.

```
const Device = {
phone="phone",
pad="pad",
deskTop="deskTop"
} as const

type DeviceType = typeof Device[keyof typeof Device]

```

### When can we use an enum?

Reverse mapping
```
enum Color {
    Red = 1,
    Green,
    Blue
}

// Forward mapping
console.log(Color.Red); // Output: 1
console.log(Color.Green); // Output: 2

// Reverse mapping
console.log(Color[1]); // Output: "Red"
console.log(Color[2]); // Output: "Green"

```