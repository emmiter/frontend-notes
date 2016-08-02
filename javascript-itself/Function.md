###[01-Object.assign(target,...sources)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
从 一个或多个 source objects 中拷贝它们自身的可枚举属性值到target对象，返回target对象。

###[02-Function.prototype.call()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)

描述: 

可以使用不同的`this`对象来调用某个已存在的函数。`this`指的是当前的对象，the calling object. **With `call`, you can write a method once and then inherit it in another object, without having to rewrite the method for the new object**.

`call()`方法使用给定的`this`值和一个参数列表来调用函数。

> `call()`函数的语法和`apply()`的语法几乎是相同的，最根本的区别在于前者接收一个**参数列表**，而后者接收一个**单独的参数数组**。

```javascript
func.call(thisArg[,arg1[,arg2[,...]]])
```

返回值:

The result of calling the function with the specified `**this**` value and arguments.

#### using call to chain constructors for an object

```javascript
function Product(name, price) {
  this.name = name;
  this.price = price;

  if (price < 0) {
    throw RangeError('Cannot create product ' +
                      this.name + ' with a negative price');
  }
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

function Toy(name, price) {
  Product.call(this, name, price);
  this.category = 'toy';
}

var cheese = new Food('feta', 5);
var fun = new Toy('robot', 40);
```

#### Using `call` to invoke an anonymous function

```javascript
var animals = [
  { species: 'Lion', name: 'King' },
  { species: 'Whale', name: 'Fail' }
];

for (var i = 0; i < animals.length; i++) {
  (function(i) {
    this.print = function() {
      console.log('#' + i + ' ' + this.species
                  + ': ' + this.name);
    }
    this.print();
  }).call(animals[i], i);
}
//animals[i] => this
//参数列表中只有一个参数 => i
```

#### Using `call` to invoke a function and specifying the context for 'this'

In below example, when we will call greet the value of this will be bind to object i.

```javascript
function greet() {
  var reply = [this.person, 'Is An Awesome', this.role].join(' ');
  console.log(reply);
}

var i = {
  person: 'Douglas Crockford', role: 'Javascript Developer'
};

greet.call(i); // Douglas Crockford Is An Awesome Javascript Developer
```



###[03-Function.prototype.apply()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

使用给定的this值调用该函数，如果要带参数调用的话，那么将所有参数放在数组中，作为第二个参数提供给函数。