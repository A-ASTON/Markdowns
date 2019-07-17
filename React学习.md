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
MyComponent.propTypes = { handleClick: PropTypes.func.isRequired }
```
>在上面的示例中，PropTypes.func部分检查handleClick是否为函数。添加isRequired是为了告诉 ReacthandleClick是该组件的必需属性。如果未提供该 prop，你将看到警告信息。另请注意，func表示function。在 7 种 JavaScript 基本类型中，function和boolean（写为bool）是仅有的使用异常拼写的两种类型。除了基本类型，还有其他类型可用。例如，你可以检查 prop 是否为 React 组件，请参阅文档以获取所有选项。

>注意：在 React v15.5.0 版本中, PropTypes可以从 React 中单独引入，如下所示：
```js
import React, { PropTypes } from 'react';
```