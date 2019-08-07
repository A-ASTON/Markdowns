# 数组
```js
let arr = [];
```
## 数组的方法：
### 插入：
> push(parameter...);      
> 将参数推进数组的末尾     
> eg：`arr.push(1, 2, 'a');`   

> unshift(parameter...);         
> 将参数插入数组的开头    
> eg：`arr.unshift(1, 2, 'aaaa')`

> 这两个函数参数的类型取决于数组能容纳的数据类型
### 移除：
> pop();     
> 从数组末尾弹出一个元素

> shift();      
> 从数组开头移除一个元素

> 两者均不接受输入参数，而且每次只能修改一个元素，并返回移除的元素



### 既能移除也能插入：
> splice(index, amount, newElement);       
> 从数组中的任意位置移除任意数量的连续的元素，注意是连续      
> 第一个参数决定了从哪个索引开始移除，第二个决定了移除的数目，第三个参数代表插入的元素，可以是一个或多个元素，插入位置为起始移除位置


### 拷贝数组项目：
> slice(index_start, index_end);     
> 复制或者说是提取(extract)给定数量的元素到一个新数组里     
> 第一个参数是开始提取元素的索引，第二个参数是结束提取元素的索引     
> 注意：会提取第一个索引对应的值，以及到结束索引前一个索引对应的值


> 使用ES6引入的展开运算符(spread operatpr) : `...`来复制一个数组     
> ```js
> let thisArr = [1, 2, 4, 1];
> let thatArr = [...thisArr];
> ```     
> 利用展开运算符，还能合并数组（如：将某数组的所有元素插入到另一个数组的任意位置）     
> ```js
> let thisArray = ['sage', 'rosemary', 'parsley', 'thyme'];
> let thatArray = ['basil', 'cilantro', ...thisArray, 'coriander'];        
> // thatArray 现在等于 ['basil', 'cilantro', 'sage', 'rosemary', 'parsley', 'thyme', 'coriander']
> ```