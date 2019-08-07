# React 
用于构建用户界面的JavaScript库   
它是渲染当代Web应用程序用户界面UI的绝佳工具

## JSX
用途：React使用名为JSX的JavaScript语法扩展，允许你直接在JavaScript中编写HTML。

浏览器不能解析JSX，因此必须将JSX代码编译为JavaScript。在这个过程中，转换器Babel是一个很受欢迎的工具。

## 1.简单的JSX
```javascript
const JSX = <h1>Hello JSX!</h1>;
```

## 2.复杂的JSX元素
>关于嵌套的JSX，它必须返回`单个`元素   
并且建议使用()将嵌套的整个HTML元素括起来

```js
const JSX = (
    <div>
        <h1></h1>
        <p></p>
        <ul>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
);
```

## 3.在JSX中添加注释

使用{/* */}添加注释

## 4.渲染HTML元素为DOM树
>在React中，我们可以使用它的渲染API（ReactDOM）将此JSX直接渲染到HTMLDOM。   
ReactDOM提供了一个简单的方法来将React元素呈现给DOM，如下所示：ReactDOM.render(componentToRender, targetNode),其中第一个参数是要渲染的React元素或组件，第二个参数是要将组件渲染到的DOM节点。

```js
const JSX = (
    <div>
        <h1>Hello World</h1>
        <p>Lets render this to the DOM</p>    
    </div>
);
var challenge-node = document.getElementById('challenge-node');
ReactDOM.render(JSX, challenge-node);

```
## 5.在JSX中定义一个HTML Class
>由于class在js中属于关键字，因此不能用class来定义HTML的class名，JSX使用className代替。    
事实上，JSX 中所有 HTML 属性和事件引用的命名约定都变成了驼峰式。例如，JSX 中的单击事件是 onClick，而不是 onclick。同样，onchange变成了onChange。

```js
const JSX = (
    <div className = "container">
        <h1>Add a class to this div</h1>
    </div>
);
```
## 6.了解自动闭合的JSX标记
>JSX 不同于 HTML 的另一个重要方面是自闭合标签。  
在 JSX 中，规则略有不同。任何 JSX 元素都可以使用自闭合标签编写，并且每个元素都必须关闭。   
例如，换行标签必须始终编写为`<br />`。另一方面`<div>`可以写成`<div />`或者`<div></div>`。   
不同之处在于，在第一个语法版本中，无法在`<div />`中包含任何内容。在后面的挑战中你会发现，这种语法在渲染 React 组件时非常有用。
```js
const JSX = (
    <div>
        <br />
        <hr />
        <div />
    </div>
);
```

## 7.创建一个无状态的函数组件
>组件是React的核心，React中的所有内容都是一个组件，在这里学习如何创建一个组件。  

>方法一：使用JavaScript函数。以这种方式定义组件会创建无状态功能组件。应用程序中的状态概念在后介绍。目前，可以将无状态组件视为可以接收数据并对其进行渲染的组件，但他是不管理或跟踪对数据的更改。

>方法详解：要用函数创建组件，只需编写一个返回 JSX 或null的 JavaScript 函数。需要注意的一点是，React 要求你的函数名以`大写字母`开头。下面是一个无状态功能组件的示例，该组件在 JSX 中分配一个 HTML 的 class：
```js
const DemoComponent = function() {
    return (
        <div className='custonClass'/>
    );
};
```
>因为 JSX 组件代表 HTML，所以你可以将几个组件放在一起以创建更复杂的 HTML 页面，这是 React 提供的组件架构的关键优势之一，它允许你用许多独立的组件组成 UI。这使得构建和维护复杂的用户界面变得更加容易。

## 8.使用ES6的class语法创建组件
> 以下示例中，Kitten扩展了React.Component：
```js
class Kitten extends React.Component {
    constructor(props) {
        super(props);
    }
    render() {
        return (
        <h1>HI!</h1>
        )
    };
};
```
>这将创建一个 ES6 类Kitten，它扩展了React.Component类。因此，Kitten类现在可以访问许多有用的 React 功能，例如`本地状态和生命周期`钩子。如果你还不熟悉这些术语，请不要担心，在以后的挑战中我们将更详细地介绍它们。

>另请注意，Kitten类中定义了一个调用super()方法的constructor。它使用`super()`调用父类的构造函数，即本例中的React.Component。构造函数是使用class关键字创建的特殊方法，它用在实例初始化之前。最佳做法是在组件的constructor里调用super，并将props传递给它们，这样可以保证组件能够正确地初始化。现在，你只需要知道这是标准的做法。很快你会看到构造函数的其他用途以及props。

## 9.用组合的方式创建一个React组件
> 现在我们来看看如何组合多个 React 组件。想象一下，你正在构建一个应用程序，并创建了三个组件：Navbar、Dashboard和Footer。

>要将这些组件组合在一起，你可以创建一个App父组件，将这三个组件分别渲染成为子组件。要在 React 组件中渲染一个子组件，你需要在 JSX 中包含作为自定义 HTML 标签编写的组件名称。例如，在render方法中，你可以这样编写：
```js
    class Kitten extends React.component {
        constructor(props) {
            super(props);
        }

        render(){
            return (
                <App>
                    <Navbar />
                    <Dashboard />
                    <Footer />
                </App>
            );
        }
    }
```

## 10.组合React组件
>我们将组合使用更复杂的 React 组件和 JSX，有一点需要注意。在其他组件中渲染 ES6 风格的类组件和渲染你在过去几个挑战中使用的简单组件没有什么不同。你可以在其他组件中渲染 JSX 元素、无状态功能组件和 ES6 类组件。

## 11.渲染class组件为Dom树
>同样是采用ReactDOM.render()方法,不同的是，第一个参数填写的是采用与渲染嵌套组件相同的语法，例如:
```js
ReactDOM.render(<ComponentToRender />, targetNode)
```

## 12.将Props传递给无状态函数组件

>在 React 中，你可以将属性传递给子组件。假设你有一个App组件，该组件渲染了一个名为Welcome的子组件，它是一个无状态函数组件。你可以通过以下方式给Welcome传递一个user属性：

```js
<App>
    <Welcome user='Mark'/>
</App>
```
>使用自定义HTML属性,React支持将属性user传递给组建Welcome。由于Welcome是一个无状态函数组件，它可以像这样访问该值：
```js
const Welcome = (props) => <h1>Hello, {props.user}!</h1>
```
>调用props这个值是常见做法，当处理无状态函数组件时，你基本上可以将其视为返回 JSX 的函数的参数。这样，你就可以在函数体中访问该值。但对于类组件，访问方式会略有不同。

## 13.传递一个数组作为Props
```js
<ParentComponent>
  <ChildComponent colors={["green", "blue", "red"]} />
</ParentComponent>
```
>这样，子组件就可以访问数组属性colors。访问属性时可以使用join()等数组方法。
```js
const ChildComponent = (props) => <p>{props.colors.join(', ')}</p>
```
>这将把所有colors数组项连接成一个逗号分隔的字符串并生成：
```js
<p>green, blue, red</p>
```
## 14.使用默认的Props
>React 还有一个设置默认 props 的选项。你可以将默认 props 作为组件本身的属性分配给组件，React 会在必要时分配默认 prop。如果没有显式的提供任何值，这允许你指定 prop 值应该是什么。例如，如果你声明    `MyComponent.defaultProps = { location: 'San Francisco' }`，即定义一个 location 属性，并且其值在没有另行制定的情况下被设置为字符串`San Francisco`。如果 props 未定义，则 React 会分配默认 props，但如果你将`null`作为 prop 的值，它将保持`null`。

组件.defaultProps = {};

## 15.覆盖默认的Props
>在 React 中，设置默认的 props 是一个很有用的特性，显式设置组件的 prop 值即可覆盖默认 props。

## 16.使用PropTypes来定义你期望的Props
>React 提供了有用的类型检查特性，以验证组件是否接收了正确类型的 props。例如，你的应用程序调用 API 来检索你希望在数组中的数据，然后将数据作为 prop 传递给组件。你可以在组件上设置propTypes，以要求数据的类型为array。当数据是任何其他类型时，都会抛出警告。
>当你提前知道 prop 的类型时，最好的做法是设置propTypes。可以为组件定义propTypes属性，方法与定义defaultProps相同。这样做将检查给定键的 prop 是否是给定类型。这里有一个示例，名为handleClick的 prop 应为function类型：
```js
// 设置其propTypes,注意大小写
MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }
```
>在上面的示例中，PropTypes.func部分检查handleClick是否为函数。添加isRequired是为了告诉 ReacthandleClick是该组件的必需属性。如果未提供该 prop，你将看到警告信息。另请注意，func表示function。在 7 种 JavaScript 基本类型中，function和boolean（写为bool）是仅有的使用异常拼写的两种类型。除了基本类型，还有其他类型可用。例如，你可以检查 prop 是否为 React 组件，请参阅文档以获取所有选项。

>注意：在 React v15.5.0 版本中, PropTypes可以从 React 中单独引入，如下所示：
```js
import React, { PropTypes } from 'react';
```

## 17.使用this.props访问Props
>ES6类组件访问props的方式，利用this关键字，像这样访问props
```js
class Country extends React.Component {
    constructor(props){
        super(props);
    }
    render(){
        return(
            <div/>
        );
    }
}
```

## 18.Props和无状态函数组件回顾
- 无状态函数组件是一个函数，接受props作为输入并返回JSX
- 无状态组件是一个类
，它扩展了React.Component,但是不适用内部状态。
- `状态组件`是指维护其自身内部状态的组件，它简称组件或React组件

> 一种常见的应用模式是尽可能减少状态组件并创建无状态的函数组件。这有助于将状态管理包含到应用程序的特定区域。反过来，通过更容易地跟踪状态变化如何影响其行为，可以改进应用程序的开发和维护

>以下是基本的无状态函数组件
```js
class CampSite extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <Camper/>
      </div>
    );
  }
};
//这是其父组件：CampSite渲染了Camper为它的子组件
// 要求子组件Camper分配默认的props{ name: 'CamperBot' };。并确保其有一个p元素，并包含了作为props传递的name值，并要求name为string类型

const Camper = (props) => (
    <p>{ props.name }</p>
);
//()不要写成{}，若写成{},就要写成下面这样
const Camper = (props) => {
    return(
        <p>{ props.name }</p>
    );
};

Camper.defaultProps = { name: 'CamperBpt' };
Camper.propTypes = { name: PropTypes.string.isRequired };
// 注意大小写

```

## 19.创建一个有状态的组件
>React中一个很重要的概念就是state。state包含了应用程序需要了解的任何数据，这些数据可能随时间变化，你希望应用程序能够响应state的变更，并在必要时显示更新后的UI。React为现代Web应用程序的状态管理提供了一个很好的解决方案。

>具体的做法：
```js
// 需要采用类组件的方法才能创建一个有状态的组件
// 具体需要在构造函数constructor里面声明state，在创建时使用state初始化组件。注意：state属性必须设置为JavaScript对象。

class StatefulComponent extends React.Component(){
    constructor(props) {
        super(props);
        this.state = {
            //describe your state here
            name: 'State'
        }
    }
    render() {
        return (
            <div>{ this.state.name }</div>
        );
    }
};
```
>可以在组件的整个`生命周期`内访问`state`对象,可以更新它,在UI中渲染它,也可以将其作为props传递给子组件。

## 20.在用户界面中渲染状态
>可以在上面的例子中见到，一旦定义了组件的初始state，就可以在要渲染的UI中显示它的任何部分。如果组件是有状态的，它就始终可以访问render()方法中state的数据。就可以使用this.state访问数据。
`{ this.state.name }`

>state是 React 组件中最强大的特性之一，它允许你跟踪应用程序中的重要数据，并根据数据的变化渲染 UI。如果你的数据发生变化，你的 UI 也会随之改变。React 使用所谓的虚拟 DOM 来跟踪幕后的变化。当 state 数据更新时，它会使用该数据触发组件的重新渲染--包括接收 prop 数据的子组件。React 只在必要的时候更新实际的DOM，这意味着你不必担心 DOM 的变更，只需声明 UI 的外观即可。

>注意，如果组件有状态，则没有其他组件知道它的state。它的state是完全封装的，或者是局限于组件本身的，除非你将 state 数据作为props传递给子组件。封装state的概念非常重要，因为它允许你编写特定的逻辑，然后将该逻辑包含并隔离在代码中的某个位置。

## 21.渲染状态的另一种方式
> 还有另一种方法可以访问组件中的state。在render()方法中，在return语句之前，你可以直接编写 JavaScript。例如，你可以声明函数、从state或props访问数据、对此数据执行计算等。然后，你可以将任何数据赋值给你在return语句中可以访问的变量。
```js
class StatefulComponent extends React.Component(){
    constructor(props) {
        super(props);
        this.state = {
            //describe your state here
            name: 'State'
        }
    }
    render() {
        const name = this.state.name ;
        return (
            <div>{ name }</div>
        );
    }
};
```

## 22.用this.setState设置状态
>在前面我们学会了初始化组件的state，那么该如何更改组件的state呢？   
React提供了`setState`方法来更新组件的state。在组件类中调用setState的方法如下：

```js
this.setState({
    username: 'Lewis'
});
```
>React 希望你永远不要直接修改state，而是在 state 发生改变时始终使用this.setState()。此外，你应该注意，React 可以批量处理多个 state 更新以提高性能。这意味着通过setState方法进行的 state 更新可以是异步的。

## 23.将this绑定到Class方法
>除了设置和更新state之外，你还可以为组件类定义方法。类方法通常需要使用this关键字，以便它可以访问方法中类的属性（例如state和props）。有几种方法可以让你的类方法访问this。

>一种常见的方法是在`构造函数`中显式地绑定this，这样当组件初始化时，this就会绑定到类方法。像`this.handleClick = this.handleClick.bind(this)`用于其在构造函数中的`handleClick`方法。然后，当你在类方法中调用像`this.setState()`这样的函数时，this指的是这个类，而不是undefined。

## 24.使用State切换元素
>用比目前所见更复杂的方式在React应用程序中使用state。例如，监视值的状态，然后根据此值有条件地渲染UI。

## 25.创建一个可以控制的输入框
>你的应用程序可能在state和渲染的 UI 之间有更复杂的交互。例如，用于文本输入的表单控件元素（如input和textarea）在用户键入时在 DOM 中维护自己的 state。通过 React，你可以将这种可变 state 转移到 React 组件的state中。用户的输入变成了应用程序state的一部分，因此 React 控制该输入字段的值。通常，如果你的 React 组件具有用户可以键入的输入字段，那么它将是一个受控的输入表单。

## 26.将State作为Props传递给子组件
>一个常见的模式是：有状态组件中包含对应用程序很重要的state，然后用它渲染子组件。你希望这些组件能够访问该state的某些部分，就把这些部分作为 props 传入。

>例如，也许你有一个App组件可以渲染Navbar以及其他组件。在你的App中，你的state中包含大量用户信息，但是Navbar只需要访问用户的用户名就可以显示出来，这时你将该state作为一个 prop 传递给Navbar组件即可。

>这个模式说明了 React 中的一些重要范例。    
- 第一个是单向数据流，state 沿着应用程序组件树的一个方向流动，从有状态父组件到子组件，子组件只接收它们需要的 state 数据。
- 第二，复杂的有状态应用程序可以分解成几个，或者可能是一个单一的有状态组件。其余组件只是从父组件简单的接收 state 作为 props，并从该 state 渲染 UI。
>它开始创建一种分离，在这种分离中，state 管理在代码的一部分中处理，而 UI 渲染在另一部分中处理。将 state 逻辑与 UI 逻辑分离是 React 的关键原则之一。当它被正确使用时，它使得复杂的、有状态的应用程序的设计变得更容易管理。

## 27.传递回调作为Props
>你可以将state作为 props 传递给子组件，但不仅限于传递数据。你也可以将处理函数或在 React 组件中定义的任何方法传递给子组件。这就是允许子组件与父组件交互的方式。你可以把方法像普通 prop 一样传递给子组件，它会被分配一个名字，你可以在子组件中的this.props下访问该方法的名字。

>这里再复习一下props的传递

例码：
```jsx
class MyApp extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      inputValue: ''
    }
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(event) {
    this.setState({
      inputValue: event.target.value
    });
  }
  render() {
    return (
       <div>
        <GetInput input={this.state.inputValue} handleChange={this.handleChange}/> //父组件通过这里传递props
        <RenderInput input={this.state.inputValue}/>
       </div>
    );
  }
};

class GetInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Get Input:</h3>
        <input
          value={this.props.input} //利用传递的props的input
          onChange={this.props.handleChange}/>
      </div>
    );
  }
};

class RenderInput extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h3>Input Render:</h3>
        <p>{this.props.input}</p>
      </div>
    );
  }
};

// 父组件：state、props => 子组件（在属性中引用） => 子组件能通过props利用属性中的数据 
```

## 28.使用生命周期方法
>什么是生命周期？React组件的生命历程    
可分为三个状态：   
Mounting：已插入真实DOM（挂载）    
Updating：正在被重新渲染    
Unmounting：已移出真实DOM（卸载）

>React 组件有几种特殊方法，可以在组件生命周期的`特定点`执行操作。这些称为生命周期方法或生命周期钩子，允许你在`特定时间点捕获组件`。这可以在渲染之前、更新之前、接收 props 之前、卸载之前等等。以下是一些主要生命周期方法的列表：

- componentWillMount()渲染前调用，在客户端也在服务端

- componentDidMount()在第一次渲染后调用，只在客户端。之后组件已经生成了对应的DOM结构，可以通过this.getDOMNode()来进行访问。 如果你想和其他JavaScript框架一起使用，可以在这个方法中调用setTimeout, setInterval或者发送AJAX请求等操作(防止异步操作阻塞UI)。

- componentWillReceiveProps()在组件接收到一个新的 prop (更新后)时被调用。这个方法在初始化render时不会被调用。

- shouldComponentUpdate()返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。 
可以在你确认不需要更新组件时使用。      
可以在你确认不需要更新组件时使用。

- componentWillUpdate()在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。

- componentDidUpdate()在组件完成更新后立即调用。在初始化时不会被调用。

- componentWillUnmount()在组件从 DOM 中移除之前立刻被调用。

## 29.componentWillMount()
>当组件被挂载到 DOM 时，componentWillMount()方法在render()方法之前被调用。
```js
class MyComponent extends React.Component {
    constructor(props) {
        super(props);
    }
    conponenetWillMount() {
        console.log('Hello');  //在componentWillMount()中将一些内容记录到控制台--你需要打开浏览器控制台以查看输出。
    }
    render() {
        return <div />
    }
};
```
## 30.componentDidMount()
>1.API 调用或任何其他调用    
某些时候，大多数 web 开发人员需要调用 API 端点来检索数据。如果你正在使用 React，知道在哪里执行这个动作是很重要的。    
React 的最佳实践是在生命周期方法componentDidMount()中对服务器进行 `API 调用或任何其他调用`。将组件装载到 DOM 后会调用此方法。此处对setState()的任何调用都将触发组件的重新渲染。在此方法中调用 API 并使用 API​​ 返回的数据设置 state 时，一旦收到数据，它将自动触发更新。

>2.添加事件侦听器    
componentDidMount()方法也是添加特定功能所需的任何事件监听器的最佳位置。React 提供了一个合成事件系统，它将本地事件系统封装在浏览器中。这意味着，不管用户的浏览器如何，合成事件系统的行为都完全相同--即使不同浏览器之间的本地事件的行为可能不同。      
你已经使用了一些合成事件处理程序，如onClick()。React 的合成事件系统非常适合用于你在 DOM 元素上管理的大多数交互。但是，如果要将事件处理程序附加到 document 或 window 对象，则必须直接执行此操作。

## 31.componentWillReceiveProps()和compoentDidUpdate()
>另一个生命周期方法是`componentWillReceiveProps()`，只要组件将要接收新的 props 就会调用它。此方法接收新的 props（通常写为nextProps）作为参数。你可以使用此参数并与this.props进行比较，并在组件更新之前执行操作。例如，你可以在处理更新之前在本地调用setState()。

>还有一个方法是`componentDidUpdate()`，它在组件重新渲染后立即调用。请注意，渲染和装载在组件生命周期中是不同的。当页面第一次加载时，所有组件都被装载，这就是调用componentWillMount()和componentDidMount()等方法的地方。此后，随着 state 的变化，组件会重新渲染自己。下一个挑战将更详细地讨论这一点。

## 32.shouldComponentUpdate()
>到目前为止，如果任何组件接收到新的state或新的props，它会重新渲染自己及其所有子组件。这通常是好的。但是 React 提供了一种生命周期方法，当子组件接收到新的state或props时，你可以调用该方法，并特别声明组件是否应该更新。方法是`shouldComponentUpdate()`，它将`nextProps`和`nextState`作为参数。    

>这种方法是优化性能的有效方法。例如，默认行为是，当组件接收到新的props时，即使props没有改变，它也会重新渲染。你可以通过使用shouldComponentUpdate()比较props来防止这种情况。该方法必须返回一个布尔值，该值告诉 React 是否更新组件。你可以比较当前的 props（`this.props`）和下一个 props（`nextProps`），以确定你是否需要更新，并相应地返回true或false。

## 33.内联样式
>还有其他复杂的概念可以为你的 React 代码增加强大的功能。但是，你可能会想知道更简单的问题，比如：如何对在 React 中创建的 JSX 元素进行风格化。你可能知道，由于将 class 应用于 JSX 元素的方式与 HTML 中的使用并不完全相同。

>如果从样式表导入样式，它就没有太大的不同。使用className属性将 class 应用于 JSX 元素，并将样式应用于样式表中的 class。另一种选择是使用`内联样式`，这在 ReactJS 开发中非常常见。

>你将内联样式应用于 JSX 元素，类似于你在 HTML 中的操作方式，但有一些 JSX 差异。以下是 HTML 中内联样式的示例：

```html
 <!-- HTML中的内联样式 -->
<div style="color: yellow; font-size: 16px">Mellow Yellow</div>
```
```js
// 对应的JSX元素
// JSX 元素使用style属性，但是由于 JSX 的传输方式，你不能将值设置为字符串。相反，你应将其设置为 JavaScript对象。这里有一个例子：    
const JSX = (
    <div style={{color: "yellow", fontSize: 16}}>Mellow Yellow</div>
    )

// 第一个{}表示传入js，第二个{}是一个对象，key用驼峰命名法
// 首先，某些 CSS 样式属性的名称使用驼峰式命名
// 除非另有规定，否则所有属性值是长度的（如height、width和fontSize）其单位都假定为px。例如，如果要使用em，可以用引号将值和单位括起来，例如{fontSize: "4em"}。除了默认为px的长度值之外，所有其他属性值都应该用引号括起来。
```

## 34.在React Render方法中使用JavaScript
>如下，在render方法中可直接写js而不用添加{}，因为它还不在JSX里面，当你稍后想在return语句中的 JSX 代码中使用变量时，可以将变量名放在大括号中。
```js
....
render() {
    const a = 1;
    return(
        <div> { a } </div>
    );
}
```

## 35.在render中可以利用各种方式控制UI
- 例如采用`if-else`，决定返回怎样的JSX
- 使用`&&`获得更简洁的条件: `{condition && <p>markup</p>}`    
如果condition为 true，则返回标记。如果 condition 为 false，操作将在判断condition后立即返回false，并且不返回任何内容。你可以将这些语句直接包含在 JSX 中，并通过在每个条件后面写&&来将多个条件串在一起。这允许你在render()方法中处理更复杂的条件逻辑，而无需重复大量代码。
- `三元表达式`     
想在 JSX 中实现条件逻辑，三元表达式是一个很好的选择,可以嵌套使用     
基本语法：`condition ? expressionIfTrue : expressionIfFalse`

## 36.使用Array.map()动态渲染元素
>条件渲染很有用，但是你可能需要组件来渲染未知数量的元素。通常在响应式编程中，程序员在应用程序运行时之前无法知道其 state，因为这在很大程度上取决于用户与该程序的交互。程序员需要提前编写代码来正确处理未知状态。在 React 中使用Array.map()阐明了这个概念。
```js
const items = this.state.toDoList.map(i=> <li>{i}</li>);

<ul>
    {items}       
</ul>
```

## 37.给同级元素一个唯一的键属性
>上一个挑战展示了如何使用map方法根据用户输入动态渲染多个元素。然而，这个例子中缺少一个重要的部分。创建元素数组时，每个元素都需要一个设置为唯一值的key属性。React 使用这些键来跟踪哪些项目被添加、更改或删除。这有助于在以任何方式修改列表时提高重新渲染过程的效率。请注意，键只需要在同级元素之间是唯一的，它们不需要在应用程序中是全局唯一的。

```js
const items = this.state.toDoList.map(i=> <li key = { i }>{ i }</li>);

<ul>
    {items}       
</ul>
```

## 38.使用 Array.Filter() 动态过滤数组
>map数组方法是一个强大的工具，在使用 React 时经常使用。与map相关的另一种方法是filter，它根据条件过滤数组的内容，然后返回一个新数组。例如，如果你有一个 users 数组，每个数组元素都有一个可以设置为true或false的online属性，你可以只过滤那些在线的用户：     
`let onlineUsers = users.filter(user => user.online);`

## 39.用 renderToString 在服务器上渲染 React
>到目前为止，你已经能够在客户端上渲染 React 组件，一般来说我们都是这么做的。然而，在一些用例中，在服务器上渲染一个 React 组件是有意义的。由于 React 是一个 JavaScript 视图库，所以使用 Node 让 JavaScript 运行在服务器上是可行的。事实上，React 提供了一个可用于此目的的renderToString()方法。

>有两个关键原因可以解释为什么服务器上的渲染可能会在真实世界的应用程序中使用。首先，如果不这样做，你的 React 应用程序将包含一个代码量很少的 HTML 文件和一大堆 JavaScript，当它最初加载到浏览器时。这对于搜索引擎来说可能不太理想，因为它们试图为你的网页内容生成索引，以便人们可以找到你。如果在服务器上渲染初始 HTML 标记并将其发送到客户端，则初始页面加载的内容包含搜索引擎可以抓取的所有页面标记。其次，这创造了更快的初始页面加载体验，因为渲染的 HTML 代码量要比整个应用程序的 JavaScript 代码小。React 仍然能够识别你的应用并在初始加载后进行管理。

>ReactDOMServer.renderToString()接受一个React元素作为参数，即需要写成<App/>