# Most Commonly Used Lodash Methods
https://lodash.com/docs/4.17.15
Lodash methods are categorized into 13 types(as of Jun 2020):
* Array
* Collection
* Date
* Function
    - curry
    - curryRight
* Lang
    - isEmpty
    - isArray, isObject, isBoolean, isFunction, isInteger...
* Math
    - floor, sum
* Number: clamp, inRange, random
* Object
    - get
    - pick
    - has
* Seq
* String
* Util
    - noop
* Properties: lodash properties
* Methods: lodash method.


### IsEmpty
Checks if value is an empty object, collection, map, or set.
Objects are considered empty if they have no own enumerable string keyed properties.
Array-like values such as arguments objects, arrays, buffers, strings, or jQuery-like collections are considered empty if they have a length of 0. Similarly, maps and sets are considered empty if they have a size of 0.

https://stackoverflow.com/questions/43233102/lodash-isempty-and-has-method-vs-simple-check/43233163#43233163

```
_.isEmpty(null);
// => true
_.isEmpty(true);
// => true
_.isEmpty(1);
// => true
_.isEmpty([1, 2, 3]);
// => false
_.isEmpty({ 'a': 1 });
// => false
_.isEmpty('');
// => true
_.isEmpty(NaN);
// => true
_.isEmpty(undefined);
// => true
```
