## 一、语法
* 区分大小写
* 标识符

	所谓标识符，就是指变量、函数、属性的名字，或者函数的参数。标识符可以是按照下列格式规则组合起来的一或多个字符：

	* 第一个字符必须是一个字母、下划线（_）或一个美元符号（$）；
	* 其他字符可以是字母、下划线、美元符号或数字。 
	* 按照惯例，ECMAScript标识符采用驼峰大小写

* 语句

	ECMAScript中的语句以一个分号结尾；如果省略分号，则由解析器确定语句的结尾，

## 二、关键字和保留字

```
	break do instanceof typeof case else new var catch 
	finally return void continue for switch while debugger* 
	function this with default if throw delete in try class 
	enum extends super const export import class enum extends 
	super const export import
```
## 三、变量

ECMAScript的变量是松散类型的，所谓松散类型就是可以用来保存任何类型的数据。

```js
	var message;
	// 这行代码定义了一个名为 message 的变量，该变量可以用来保存任何值，像这样未经过初始化的变量，会保存一个特殊的值— undefined
	var message = "hi"; 
	// 在此，变量message中保存了一个字符串值"hi"。像这样初始化变量并不会把它标记为字符串类型；
	// 初始化的过程就是给变量赋一个值那么简单。因此，可以在修改变量值的同时修改值的类型，如下所示：varmessage = "hi"; message = 100;
	// 有效，但不推荐在这个例子中，变量message一开始保存了一个字符串值"hi"，然后该值又被一个数字值100取代。
	// 有一点必须注意，即使用var操作符定义的变量将成为定义该变量的作用域中的局部变量。
	// 也就是说，如果在函数中使用var定义一个变量，那么这个变量在函数退出后就会被销毁，
```
```js
	var message = "hi", 
		found = false, 
		age = 29;
```
## 四、数据类型

ECMAScript中有5种简单数据类型（也称为基本基本数据类型）：
`Undefined`、 `Null` 、 `Boolean` 、 `Number` 和 `String`。
还有1种复杂数据类型—— `Object` ，`Object` 本质上是由一组无序的名值对组成的。

* `Undefined` 只有一个值，即特殊的 `undefined`。在使用 `var` 声明变量但未对其加以初始化时，这个变量的值就是 `undefined`

```js
	var message; 
	// 这个变量声明之后默认取得了 undefined 值 
	// 下面这个变量并没有声明
	// var age 
	alert( typeof message); 
	// "undefined" 
	alert( typeof age); 
	// "undefined"
```

* `Null` 类型是第二个只有一个值的数据类型，这个特殊的值是 `null`。从逻辑角度来看，`null` 值表示一个空对象指针，而这也正是使用 `typeof` 操作符检测 `null` 值时会返回 "object" 的原因

<p class="tip">如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为 `null` 而不是其他值。这样一来，只要直接检查`null`值就可以知道
</p>

```js
	var car = null; alert( typeof car); // "object"
	if (car != null){ 
		// 对 car 对象执行某些操作 
	}
```
<p class="tip">
	实际上，undefined 值是派生自 null 值的，因此 ECMA- 262 规定对它们的相等性测试要返回 true
</p>

```js
	alert( null == undefined); //true
```
* Boolean 类型 true 和 false。 这两个值与数字值不是一回事，因此 true 不一定等于 1， 而 false 也不也不一定等于 0。

* Number 类型















