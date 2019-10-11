# redux - 状态管理器
原文请在此查看：[完全理解redux](https://github.com/brickspert/blog/issues/22)


### 它和react没有关系，可以用在任何框架

## 状态管理的最简实现
```js
let state = {  //计数器
    count: 1
}       
console.log(state.count);  //使用状态
state.count = 2;     //修改状态
```

这样修改count后，使用count的地方不能接收到通知。可以使用发布-订阅模式来解决这个问题：发布-订阅模式？--使用该属性的先订阅成为订阅者，每次修改发布则需要通知所有订阅者    
订阅函数：以订阅者（可以是函数）为参数，推入订阅列表   
     
这是一个js作用域的问题，使得订阅函数在修改属性的函数里面调用这个属性
```js
// 尝试看懂并学习这种代码方式
const createStore = function (initState) {
    let state  initState;
    let listeners = [];

    // 订阅
    function subscribe(listener) {
        listeners.push(listener);
    }

    function changeState(newState) {
        state = newState;
        // 通知
        for (let i = 0; i < listeners.length; i++) {
            const listener = listeners[i];
            listener();

        }
    }

    function getState() {
        return state;
    }

    return {
        subcribe,
        changeState,
        getState
    }
}


// 我们来使用这个状态管理器管理多个状态 counter 和 info 试试

let initState = {
  counter: {
    count: 0
  },
  info: {
    name: '',
    description: ''
  }
}

let store = createStore(initState);

store.subscribe(() => {
  let state = store.getState();
  console.log(`${state.info.name}：${state.info.description}`);
});
store.subscribe(() => {
  let state = store.getState();
  console.log(state.counter.count);
});

store.changeState({
  ...store.getState(),
  info: {
    name: '前端九部',
    description: '我们都是前端爱好者！'
  }
});

store.changeState({
  ...store.getState(),
  counter: {
    count: 1
  }
});

```