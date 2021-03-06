# 06 Arrays

Thee I’ll chase hence, thou wolf in sheep’s array.

—William Shakespeare, The First Part of Henry the Sixth 

An array is a linear allocation of memory in which elements are accessed by integers that are used to compute offsets. Arrays can be very fast data structures. Unfortunately, JavaScript does not have anything like this kind of array. 

Instead, JavaScript provides an object that has some array-like characteristics. It converts array subscripts into strings that are used to make properties. It is significantly slower than a real array, but it can be more convenient to use. Retrieval and updating of properties work the same as with objects, except that there is a special trick with integer property names. Arrays have their own literal format. Arrays also have a much more useful set of built-in methods, described in Chapter 8.

数知是一段线性分配的内存，它通过整数计算偏移并访问其中的元素。数组是一种性能出色的数据结构。不幸的是，Javascript 没有像此类数组一样的数据结构。作为替代，Javascript 提供了一种拥有一些类数组（aray-like）特性的对象。它把数组的下标转变成字符串，用其作为属性。它明显地比一个真正的数组慢，但它使用起来更方便。它的属性的检索和更新的方式与对象一模一样，只不过多一个可以用整数作为属性名的特性。数组有自己的字面量格式。数组也有一套非常有用的内置方法。

## 01. Array Literals

Array literals provide a very convenient notation for creating new array values. An array literal is a pair of square brackets surrounding zero or more values separated by commas. An array literal can appear anywhere an expression can appear. The first value will get the property name '0', the second value will get the property name '1', and so on:

```js
var empty = [];
var numbers = [
    'zero', 'one', 'two', 'three', 'four',
    'five', 'six', 'seven', 'eight', 'nine'
];

empty[1] // undefined
numbers[1] // 'one'
empty.length // 0
numbers.length // 10
```

The object literal:

```js
var numbers_object = {
    '0': 'zero', '1': 'one', '2': 'two',
    '3': 'three', '4': 'four', '5': 'five',
    '6': 'six', '7': 'seven', '8': 'eight',
    '9': 'nine'
};
```

produces a similar result. Both numbers and number\_object are objects containing 10 properties, and those properties have exactly the same names and values. But there are also significant differences. numbers inherits from Array.prototype, whereas number\_object inherits from Object.prototype, so numbers inherits a larger set of useful methods. Also, numbers gets the mysterious length property, while number\_object does not.

In most languages, the elements of an array are all required to be of the same type. JavaScript allows an array to contain any mixture of values: 

```js
var misc = [
    'string', 98.6, true, false, null, undefined,
    ['nested', 'array'], {object: true}, NaN,
    Infinity
];

misc.length // 10
```

1『 JS 里数组的各个元素可以是不同的类型，这个是「对象模拟数组」的一个体现。』

## 02. Length

Every array has a length property. Unlike most other languages, JavaScript’s array length is not an upper bound. If you store an element with a subscript that is greater than or equal to the current length, the length will increase to contain the new element. There is no array bounds error. The length property is the largest integer property name in the array plus one. This is not necessarily the number of properties in the array: 

1『 JS 的数组长度没上限，可以自动增加长度。注意：数组的长度跟其元素里的整数属性名挂钩，印象中 php 的数组也是，待验证。』

```js
var myArray = [];
myArray.length // 0
myArray[1000000] = true;
myArray.length // 1000001
// myArray contains one property.
```

The [] postfix subscript operator converts its expression to a string using the expression’s toString method if it has one. That string will be used as the property name. If the string looks like a positive integer that is greater than or equal to the array’s current length and is less than 4,294,967,295, then the length of the array is set to the new subscript plus one.

The length can be set explicitly. Making the length larger does not allocate more space for the array. Making the length smaller will cause all properties with a subscript that is greater than or equal to the new length to be deleted: 

 [] 后置下标运算符把它所含的表达式转换成一个字符串，如果该表达式有 tostring 方法就使用该方法的值。这个字符串将被用做属性名。如果这个字符串看起来像一个大于等于这个数组当前的  length 且小于 4294967295 的正整数，那么这个数组的 length 就会被重新设置为新的下标加 1。

```js
numbers.length = 3;
// numbers is ['zero', 'one', 'two']
```

A new element can be appended to the end of an array by assigning to the array’s current length:

```
numbers[numbers.length] = 'shi';
// numbers is ['zero', 'one', 'two', 'shi']
```

It is sometimes more convenient to use the push method to accomplish the same thing:

```
numbers.push('go');
// numbers is ['zero', 'one', 'two', 'shi', 'go']
```

## 03. Delete

Since JavaScript’s arrays are really objects, the delete operator can be used to remove elements from an array:

```
delete numbers[2];
// numbers is ['zero', 'one', undefined, 'shi', 'go']
```

Unfortunately, that leaves a hole in the array. This is because the elements to the right of the deleted element retain their original names. What you usually want is to decrement the names of each of the elements to the right.

1『超级不建议用这种方式直接删数组里的元素。』

Fortunately, JavaScript arrays have a splice method. It can do surgery on an array, deleting some number of elements and replacing them with other elements. The first argument is an ordinal in the array. The second argument is the number of elements to delete. Any additional arguments get inserted into the array at that point: 

这是因为排在被删除元素之后的元素保留着它们最初的属性。而你通常想要的是递减后面每个元素的属性。幸运的是，Javascript 数组有一个 splice 方法。它可以对数组做个手术，删除一些元素并将它们替换为其他的元素。第 1 个参数是数组中的一个序号，第 2 个参数是要刑除的元素个数。任何额外的参数会在序号那个点的位置被插入到数组中。

```js
numbers.splice(2, 1);
// numbers is ['zero', 'one', 'shi', 'go']
```

The property whose value is 'shi' has its key changed from '4' to '3'. Because every property after the deleted property must be removed and reinserted with a new key, this might not go quickly for large arrays.

## 04. Enumeration

Since JavaScript’s arrays are really objects, the for in statement can be used to iterate over all of the properties of an array. Unfortunately, for in makes no guarantee about the order of the properties, and most array applications expect the elements to be produced in numerical order. Also, there is still the problem with unexpected properties being dredged up from the prototype chain.

遗憾的是，for in 无法保证属性的顺序，而大多数要遍历数组的场合都期望按照阿拉伯数字顺序来产生元素。此外，可能从原型链中得到意外属性的问题依旧存在。

Fortunately, the conventional for statement avoids these problems. JavaScript’s for statement is similar to that in most C-like languages. It is controlled by three clauses—the first initializes the loop, the second is the while condition, and the third does the increment:

```js
var i;
for (i = 0; i < myArray.length; i += 1) {
    document.writeln(myArray[i]);
}
```

## 05. Confusion

A common error in JavaScript programs is to use an object when an array is required or an array when an object is required. The rule is simple: when the property names are small sequential integers, you should use an array. Otherwise, use an object. JavaScript itself is confused about the difference between arrays and objects. The typeof operator reports that the type of an array is 'object', which isn’t very helpful. JavaScript does not have a good mechanism for distinguishing between arrays and objects. We can work around that deficiency by defining our own is\_array function: 

```js
var is_array = function (value) {
    return value &&
        typeof value === 'object' &&
        value.constructor === Array;
};
```

Unfortunately, it fails to identify arrays that were constructed in a different window or frame. If we want to accurately detect those foreign arrays, we have to work a little harder:

```
var is_array = function (value) {
    return value &&
    typeof value === 'object' &&
    typeof value.length === 'number' &&
    typeof value.splice === 'function' &&
    !(value.propertyIsEnumerable('length'));
};
```

First, we ask if the value is truthy. We do this to reject null and other falsy values. Second, we ask if the typeof value is 'object'. This will be true for objects, arrays, and (weirdly) null. Third, we ask if the value has a length property that is a number. This will always be true for arrays, but usually not for objects. Fourth, we ask if the value contains a splice method. This again will be true for all arrays. Finally, we ask if the length property is enumerable (will length be produced by a for in loop?). That will be false for all arrays. This is the most reliable test for arrayness that I have found. It is unfortunate that it is so complicated.

Having such a test, it is possible to write functions that do one thing when passed a single value and lots of things when passed an array of values.

1『

中文版里给的判断方法不同：

```js
var is_array = function() {
    return Object,prototype.toString.apply(value) === '[object Arrary]';
};
```

』

## 06. Methods

JavaScript provides a set of methods for acting on arrays. The methods are functions stored in Array.prototype. In Chapter 3, we saw that Object.prototype can be augmented. Array.prototype can be augmented as well. For example, suppose we want to add an array method that will allow us to do computation on an array:

```js
Array.method('reduce', function (f, value) {
    var i;
    for (i = 0; i < this.length; i += 1) {
        value = f(this[i], value);
    }
    return value;
});
```

By adding a function to Array.prototype, every array inherits the method. In this case, we defined a reduce method that takes a function and a starting value. For each element of the array, it calls the function with an element and the value, and computes a new value. When it is finished, it returns the value. If we pass in a function that adds two numbers, it computes the sum. If we pass in a function that multiplies two numbers, it computes the product:

```js
// Create an array of numbers.
var data = [4, 8, 15, 16, 23, 42];

// Define two simple functions. One will add two
// numbers. The other will multiply two numbers.
var add = function (a, b) {
    return a + b;
};

var mult = function (a, b) {
    return a * b;
};

// Invoke the data's reduce method, passing in the add function.
var sum = data.reduce(add, 0); // sum is 108

// Invoke the reduce method again, this time passing in the multiply function.
var product = data.reduce(mult, 1); // product is 7418880
```

Because an array is really an object, we can add methods directly to an individual array:

```js
// Give the data array a total function.

data.total = function ( ) {
    return this.reduce(add, 0);
};
total = data.total( ); // total is 108
```

Since the string 'total' is not an integer, adding a total property to an array does not change its length. Arrays are most useful when the property names are integers, but they are still objects, and objects can accept any string as a property name. It is not useful to use the Object.create method from Chapter 3 on arrays because it produces an object, not an array. The object produced will inherit the array’s values and methods, but it will not have the special length property.

## 07. Dimensions

JavaScript arrays usually are not initialized. If you ask for a new array with [], it will be empty. If you access a missing element, you will get the undefined value. If you are aware of that, or if you will naturally set every element before you attempt to retrieve it, then all is well. But if you are implementing algorithms that assume that every element starts with a known value (such as 0), then you must prep the array yourself. JavaScript should have provided some form of an Array.dim method to do this, but we can easily correct this oversight:

```js
Array.dim = function (dimension, initial) {
    var a = [], i;
    for (i = 0; i < dimension; i += 1) {
        a[i] = initial;
    }
    return a;
};

// Make an array containing 10 zeros.
var myArray = Array.dim(10, 0);
```

JavaScript does not have arrays of more than one dimension, but like most C languages, it can have arrays of arrays:

```js
var matrix = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8]
];

matrix[2][1] // 7
```

To make a two-dimensional array or an array of arrays, you must build the arrays yourself:

```js
for (i = 0; i < n; i += 1) {
    my_array[i] = [];
}
// Note: Array.dim(n, []) will not work here.
// Each element would get a reference to the same
// array, which would be very bad.
```

The cells of an empty matrix will initially have the value undefined. If youwant them to have a different initial value, you must explicitly set them. Again, JavaScript should have provided better support for matrixes. We can correct that, too: 

```js
Array.matrix = function (m, n, initial) {
    var a, i, j, mat = [];
    for (i = 0; i < m; i += 1) {
        a = [];
    for (j = 0; j < n; j += 1) {
        a[j] = initial;
    }
    mat[i] = a;
    }
    return mat;
};

// Make a 4 * 4 matrix filled with zeros.
var myMatrix = Array.matrix(4, 4, 0);
document.writeln(myMatrix[3][3]); // 0

// Method to make an identity matrix.
Array.identity = function (n) {
    var i, mat = Array.matrix(n, n, 0);
    for (i = 0; i < n; i += 1) {
        mat[i][i] = 1;
    }
    return mat;
};
myMatrix = Array.identity(4);
document.writeln(myMatrix[3][3]); // 1
```