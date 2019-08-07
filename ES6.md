# ES6

## 1.let关键字

### 探索var和let关键字之间的差异

1. 使用var关键字声明的变量，重复声明后导致变量被覆盖而不会报错    
使用let关键字声明的变量，重复声明后会报错 

2. var和let作用域不一样     
var：全局变量或函数内的局部变量    
let：全区变量或函数内的局部变量以外，在代码块、语句或表达式中使用关键字let声明变量，这个变量的作用域就被限制在当前的代码块，语句或表达式中。

## 2.const关键字

1. 用const声明的变量
>const关键字拥有let的所有特性，除此以外，用const声明的变量是只读的。意味着通过const声明的变量只能被赋值一次，而不能被再次赋值。    
你应该使用const关键字来对所有不打算再次赋值的变量进行声明。这有助于你避免给一个常量进行额外的再次赋值。一个最佳实践是对所有常量的命名采用全大写字母，并在单词之间使用下划线进行分隔。

2. 用const声明的数组
>对象（包括数组和函数）在使用const声明的时候依然是可变的。使用const来声明只会保证它的标识不会被重新赋值。例如：
```js
"use strict";
const s = [5, 6, 7];
s = [1, 2, 3]; // 试图给 const 变量赋值，报错
s[2] = 45; // 与用 var 或 let 声明的数组一样，这个操作也会成功
console.log(s); // 返回 [5, 6, 45]

// 从以上代码看出，你可以改变[5, 6, 7]自身，所以s变量指向了改变后的数组[5, 6, 45]。和所有数组一样，数组s中的数组元素是可以被改变的，但是因为使用了const关键字，你不能使用赋值操作符将变量标识s指向另外一个数组。
```

## 3.防止对象改变
>通过之前的挑战可以看出,const声明并不会真的保护你的数据不被改变。为了确保数据不被改变，JavaScript 提供了一个函数Object.freeze来防止数据改变。    
当一个对象被冻结的时候，你不能再对它的属性再进行增、删、改的操作。任何试图改变对象的操作都会被阻止，却不会报错。
```js
let obj = {
  name:"FreeCodeCamp",
  review:"Awesome"
};
Object.freeze(obj);
obj.review = "bad"; // obj 对象被冻结了，这个操作会被忽略
obj.newProp = "Test"; // 也会被忽略，不允许数据改变
console.log(obj); 
// { name: "FreeCodeCamp", review:"Awesome"}
```

## 4.箭头函数
- 编写简洁的匿名函数
>匿名函数：不需要复用的函数可采取匿名函数的方式定义，尤其是需要将一个函数作为参数传给另外一个函数的时候，不需要给函数命名

>采用箭头函数能简洁地编写匿名函数，例如:
```js
const myFunc = function() {
  const myVar = "value";
  return myVar;
}
// 可使用箭头函数
const myFunc = () => {
    const myVar = "value";
    return myVar;
}
// 只返回一个值的时候，允许省略return关键字和外面的大括号
const myFunc = () => "value";
```

- 编写带参数的箭头函数
```js
//给传入的数值乘以2并返回结果
const doubler = (item) => item * 2;
```

- 编写高阶箭头函数
>filter函数回顾：把传入的函数依次作用于每个元素，然后根据返回值是true或false决定保留还是丢弃   

>map函数：把传入的数组的每个元素依次作为传入函数的参数，并返回一个传入函数作用后返回值的列表

>reduce函数：接受一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值

>箭头函数在类似map(),filter(),reduce()等需要其他函数作为参数来处理数据的高阶函数里会很好用。例子：
```js
FBPosts.filter(function(post) {
    return post.thumbnail !== null && post.shares > 100 && post.likes > 500;
})
```

上述函数改写为箭头函数：
```js
FBPosts.filter((post) => post.thumbnail !== null && post.shares > 100 && post.likes > 500)
```

## 5.设置函数的默认参数
>ES6中允许给函数传入默认参数，来构建更加灵活的函数。如下：
```js
function greeting(name="Anonymous") {
    return "Hello " + name;
}
console.log(greeting("John"));//Hello John
console.log(greeting());//Hello Anonymous
//可见当不传入参数name时，默认使用值"Anonymous"。还可以给多个参数赋予默认值
```

## 6.将rest操作符与函数参数一起使用,rest即...
>ES6推出了用于函数参数的rest操作符帮助我们创建更加灵活的函数。在rest操作符的帮助下，你可以创建有一个变量来接受多个参数的函数。这些参数被储存在一个可以在函数内部读取的数组中。如下：
```js
function howMany(...args) {
    return "You have passed " + args.length + "arguments. ";
}
console.log(howMany(0, 1, 2));//输出：You have passed 3 arguments.
console.log(howMany("string", null, [1, 2, 3], {}));//输出：You have passed 4 arguments.
```
>rest操作符可以避免查看args数组的需求，并且允许我们在参数数组上使用map(),fiter()，和reduce()。   
注意，rest 参数之后不能再有其他参数(即，只能是最后一个参数)，否则会报错

## 7.使用spread运算符展开数组项
>ES6允许我们使用展开操作符来展开数组，以及需要多个参数或元素的表达式

>展开操作符即： `...args` 只能用于函数参数，或者用于数组中   
其作用可以看成返回一个‘展开’的数组,请看以下例子：
```js
var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr);//返回89

//由于Math.max方法需要传入的是一系列由逗号分隔的参数，而不是一个数组
// apply()方法和call()方法，能够编写用于不同对象的方法（方法重用）
// 这里除了使用apply以外，还可以使用spread运算符

var maximus = Math.max(...arr);

// 还可以这样用
const arr1 = [...arr];
```  

## 8.解构赋值
>注意：解构赋值前的变量声明不是必要的，其声明的是接受赋值的变量的类型
- 使用解构赋值从对象中分配变量
>展开操作符可以展开数组的内容    
对于对象，我们也可以做同样的操作。`解构赋值`就是可以从对象中直接获取对应值的语法。看以下代码：
```js
// ES5：
var voxel = {x: 3.6, y: 7.4, z: 6.54};
var x = voxel.x;//x = 3.6;
var y = voxel.y;//y = 7.4;
var z = voxel.z;//z = 6.54;

// ES6解构语法:
const { x, y, z } = voxel; //x = 3.6, y = 7.4, z = 6.54;
{ 属性名 } = 对象;

//如果想将voxel.x,voxel.y,voxel.z的值分别赋给a,b,c，可以采用这种方法：
const { x : a, y : b, z : c } = voxel; //a = 3.6, b = 7.4 , c = 6.54
{ 属性名:目标变量 } = 对象;
//可以理解为"将x地址中的值拷贝到a当中去"
```

- 使用解构赋值从嵌套对象中分配变量
>我们可以将嵌套的对象解构到变量中
```js
const a = {
    start: { x: 5, y: 6 },
    end: { x: 6, y: -9 }
};
const { start : { x: startX, y: startY }} = a;
console.log(startX, startY);//5, 6

{ 二级对象: { 属性名: 目标变量}} = 一级对象(二级对象的父对象);
```

- 使用解构赋值从数组中分配变量

>在ES6中解构数组可以和对象一样简单   
与数组解构不同，数组的扩展运算会将数组里的所有内容分解成一个由逗号分隔的列表。所以，你不能选择哪个元素来给变量赋值。    
而对数组进行解构却可以让我们做到这一点：
```js
const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b); //1, 2
//变量a以及b分别被数组的第一、第二个元素赋值/
// 我们甚至能在数组解构中使用逗号分隔符，来获取任意一个想要的值：
const [a, b,,, c] = [1, 2, 3, 4, 5, 6];
console.log(a, b, c);//1, 2, 5
```

- 使用解构赋值配合rest操作符来重新分配数组元素
>以下代码结果与使用`Array.prototype.slice()`相同
```js
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b);//1, 2
console.log(arr);//[3, 4, 5, 7]
// 注意rest操作符只能对最后的元素起作用，因此不能截取原数组中间元素的子数组。
```

- 使用解构赋值将对象作为函数的参数传递
>可以在函数的参数里直接解构对象，如下：
```js
const profileUpdate = (profileData) => {
    cosnt { name, age, nationality, location } = profileData;
    // 对这些参数执行某些操作
}

//上面的操作解构了传给函数的对象。可以直接在参数里完成
const profileUpdate = ({ name, age, nationality, location }) => {
    // 对这些参数执行某些操作
}
```
>这样的操作去除了多余的代码，使代码更加整洁。    
这样做还有个额外的好处：函数不需要再去操作整个对象，而仅仅是操作复制到函数作用域内部的参数。

## 9.使用模板字面量创建字符串
>模板字符串是 ES6 的另外一项新的功能。这是一种可以轻松构建复杂字符串的方法。
```js
const person = {
    name: "Zodiac Hasbro",
    age: 56
};

//string interpolation
const greeting = `Hello, my name is ${person.name}! I am ${person.age} years old.`;

console.log(greeting);
//Hello, my name is Zodiac Hasbro! 
// I am 56 years old!
```
>首先，上面使用的${variable}语法是一个占位符。这样一来，你将不再需要使用+运算符来连接字符串。当需要在字符串里增加变量的时候，你只需要在变量的外面括上${和}，并将其放在字符串里就可以了。

>其次，在例子使用了反引号（`），而不是引号（'或者"）将字符串括了起来，并且这个字符串可以换行。

## 10.使用简单字段编写简洁的对象字面量声明
```js
const getMOusePosition = (x ,y) => ({
    x: x,
    y: y
});
// getMousePosition是一个返回了拥有2个属性的对象的简单函数。
//将对象属性作为参数，即可生成包含对应属性的对象

//重写的同样的函数：
const getMousePosition = (x, y) => ({ x, y });
```

## 11.用ES6编写简洁的函数声明
```js
// ES5，当我们需要在对象中定义一个函数的时候，我们必须如下面这般使用function关键字：
const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};

//ES6中可以完全删除function关键字和冒号。请看以下例子：
const person = {
    name: "Taylor",
    sayHello() {
        return `Hello! My name is ${this.name}`;
    }
};
```

## 12.使用class语法定义构造函数
>ES6提供了一个新的创建对象的语法，使用关键字class。    
值得注意的是，class只是一个语法糖，它并不像Java、Python或者Ruby这一类的语言一样，严格履行了面向对象的开发规范。

```js
// 在 ES5 里面，我们通常会定义一个构造函数，然后使用 new 关键字来实例化一个对象：
var SpaceShuttle = function(targetPlanet){
  this.targetPlanet = targetPlanet;
}
var zeus = new SpaceShuttle('Jupiter');

// class的语法只是简单地替换了构造函数的写法：
class SpaceShuttle {
    constructor(targetPlanet) {
        this.targetPlanet = targetPlanet;
    }
}
const zues = new SpaceShuttle('Jupiter');
// 注意class关键字声明了一个新的函数，并在其中添加了一个会在使用new关键字创建新对象时调用的构造函数。
```

## 13.使用getter和setter来控制对象的访问
>你可以从对象中获得一个值，也可以给对象的属性赋值。  
这种行为被称为getters以及setters

>Getter 函数的作用是可以让返回一个对象私有变量的值给用户，而不需要直接去访问私有变量。

>Setter 函数的作用是可以基于传进的参数来修改对象中私有变量的值。这些修改可以是计算，或者是直接替换之前的值。

```js
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer(){
    return this._author;
  }
  // setter
  set writer(updatedAuthor){
    this._author = updatedAuthor;
  }
}
const lol = new Book('anonymous');
console.log(lol.writer);  // anonymous
lol.writer = 'wut';
console.log(lol.writer);  // wut
```
注意我们调用 getter 和 setter 的语法，它们看起来并不像一个函数调用。

Getter 和 Setter 非常重要，因为它们隐藏了内部的实现细节。

## 14.了解import和require之间的差异
>在过去，我们会使用require()函数来从外部文件或模块中引入函数或者代码。这时候会遇到一个问题：有些文件或者模块会特别大，但你却往往只需要引入其中的一些核心代码。

>ES6 给我们提供了import这个便利的工具。通过它，我们能够从外部的文件或者模块中选择我们需要的部分进行引入，从而节约载入的时间和内存空间。

>请看下面的例子：想象math_array_functions拥有大概20个函数，但是我只需要countItems这一个函数在我当前的文件里。使用老的require()方式会强制我引入所有20个函数。而使用新的import语法，我可以只引入需要的那个函数：
```js
import { countItems } from "math_array_functions"

// 下面是对于上面代码的语义描述：
// import { function } from "file_path_goes_here"

//我们还可以用同样的方式来引入变量！
// 对import的使用，有许多的写法，但是上面的例子是最常用的写法。
```

三点注意：
 - 在大括号里的函数名的两侧加上空格是一个最佳实践——这可以帮助我们轻松的阅读import语句。
 - 本节课中进行的是一个非浏览器操作。import以及与其相关的在后面课程中的语句，是无法直接在浏览器上运行的。但是，我们可以通过一些工具来使它可以在浏览器中运行。
 - 在许多的例子中，在文件的路径前会加上./；否则， node.js 会先尝试去node_modules目录中寻找依赖项。

 ## 15.用export来重用代码块
 >在上一个挑战中学习了关于import语句是如何从大文件中引入其中的部分代码的。但是，为了让其正常的工作，我们还必须了解一个与之相关的语句，叫做export。当我们想要一些代码——函数或者变量——在其他文件中使用，我们必须将它们导出来供其他文件导入。和import一样，export也是一个非浏览器的功能。

 >下面的例子阐述了如何进行一个命名导出。通过这样，我们可以使用上节课学习的import语法，将导出的代码导入到其他的文件中去。请看下面的例子：
 ```js
const capitalizeString = (string) => {
  return string.charAt(0).toUpperCase() + string.slice(1);
}
export { capitalizeString } //如何导出函数。
export const foo = "bar"; //如何导出变量。


// 另外，如果你想要将你所有的export语句打包成一行，你可以像下面这个例子一样实现：
const capitalizeString = (string) => {
  return string.charAt(0).toUpperCase() + string.slice(1);
}
const foo = "bar";
export { capitalizeString, foo }
```

## 16.用*从文件中导入所有内容
>与import一起结合*从文件中导入所有的内容：
```js
import * as myMathModule from "math_functions";
myMathModule.add(2,3);
myMathModule.subtract(5,3);

import * as 自定义名称 from path;
```

## 17.用export default创建一个默认导出
>在export的课程中，你学习了命名导出的语法。这让你可以在其他文件中引用一些函数或者变量。

>你还需要知道另外一种被称为默认导出的export的语法。在文件中只有一个值需要导出的时候，你通常会使用这种语法。它也常常用于给文件或者模块创建返回值。
```js
// 这是一个简单的export default例子
export default function add(x,y) {
    return x + y;
}
```
>注意：当使用export default去声明一个文件或者模块的返回值，你在每个文件或者模块中应当只默认导出一个值。特别地，你能将export deafult与var，let与const一起使用。

## 18.导入一个默认的导出
>在上一个挑战里，你学会了export default的用法。还有一个重要的点，你可能需要另外一种import的语法来导入默认导出。

>在下面的例子里有一个add函数, 它在"math_functions"文件里默认被导出。让我们看看来如何导入它：
```js
import add from "math_functions";
add(5,4); //将会返回 9
// 这个语法只有一处不同的地方 —— 被导入的add值，并没有被花括号{}所包围。与导出值的方法不同，导入默认导出的写法仅仅只是简单的讲变量名写在import之后。
```
