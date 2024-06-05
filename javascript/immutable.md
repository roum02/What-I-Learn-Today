### immutable

the primitive type and object type differ for following three reasons.
1. primitive type is immutable type but object type is mutable type.
2. if a primitive value is assigned, the variable stores the actual value. However, if an object value is assigned, the variable stores a reference to the value.
3. "Pass by value" means that the primitive value is copied when it is assigned to another variable.
"Pass by reference" means that the reference value is copied when it is assigned to another variable.


Summary for Iteration Protocol!

the iterable protocol : An object is considered iterable if it implements a method whose key is Symbol.iterator.
Objects that conform to the iterable protocol can be used in for...of loops, spread syntax.
ex) Array, String, Map, Set. not Object!
the iterator protocol : An iterator is an object that provides a next() method.