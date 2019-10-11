# webpack
## Webpack is used to compile JavaScript modules.

## webpack自行总结 

资源放在src文件夹下，通过配置webpack.config.js文件，以及在index.js（模块）中import所需资源（显式依赖），运行webpack打包，可将资源输出到dist文件夹下

目前为止，总结一下：       
命令行使用过的命令：
```js
npm install --save-dev <package>  //用于开发环境
npm install --save <package>     //用于生产环境

npx webpack (--config <configuration>)//启动打包，采用默认的配置文件（webpack.config.js），也可以自行选择

npm run build //自定义NPM Scripts，详见下方
```
## NPM Scripts
在package.json文件中自定义npm scripts能够便捷地使用npm、webpack等命令行    
```json
{
    ...,
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "watch": "webpack --watch",
        "build": "webpack",
        ...
    },
    ...
}
```

## webpack.config.js的编写
```js
const path = require('path');  //引入path库
//定义模块输出
module.exports = {
    entry: './src/index.js',    //定义入口，即需要被打包的文件

    //定义输出文件
    output: {
        filename: 'bundle.js',   //打包后的名字
        path: path.resolve(__dirname, 'dist') //路径
    },
    module: {
        rules: [
            {
                test: /\.css$/,
                use: [
                    'style-loader',
                    'css-loader'
                ]
            }
        ]
    }
};
```

## 管理资源
通过上述定义模块module和rules进行配置不同文件采用不同的loader，然后在index.js文件中import
```js
npm install --save-dev style-loader css-loader   //引入CSS
file-loader  //引入文字，图片等文件资源
csv-loader xml-loader  //引入数据
```


## 管理输出文件
通过这个方法能更加清晰方便地管理输出文件，具体做法是设置配置文件webpack.config.js

目录结构:
```
  webpack-demo
  |- package.json
  |- webpack.config.js
  |- /dist
  |- /src
    |- index.js
+   |- print.js
  |- /node_modules
```
```js
const path = require('path');  //引入path库
//定义模块输出
module.exports = {
    entry: {
        app: './src/index.js',       //通过键值对的模式传递入口文件
        print: './src/print.js'
    },    

    //定义输出文件
    output: {
        filename: '[name].bundle.js',   //打包后的名字，在index.html中引入的文件
        path: path.resolve(__dirname, 'dist') //路径
    }
};
```

## 插件的使用
```js
npm install --save-dev html-webpack-plugin //启用后每次打包将会自动生成目标index.html文件，并自动添加bundle
npm instsall --save-dev clean-webpack-plugin //启用后每次打包前将会清空/dist目录

//要使用这些插件，也需要调整配置文件
const ...
const HtmlWebpackPlugin = require('html-webpack-plugin');
const { CleanWebpackPlugin } = require('clean-webpack-plugin');

module.exports = {
    ...,
    plugins: [
        new CleanWebpackPlugin(),
        new HtmlWebpackPlugin({
            title: 'Putput Management'
        })
    ],
    ...
};
```

## 开发环境(使用一些开发工具,不适用于生产环境)
- 采用source maps便于找到errors    
- source maps有很多[选项](https://webpack.js.org/configuration/devtool/)，这里采用inline-source-map,修改webpack.config.js文件
- ```js
  module.exports = {
      + devtool: 'inline-source-map'
  }
  ```
### 接下来讲解使用了三个开发工具(webpack's Watch Mode,webpacl-dev-server,webpack-dev-middleware)
- #### webpack's Watch Mode         
    开启后，可以监察文件修改，自动打包。webpack内置的一个模式，通过`webpack --watch`可开启，或者编写npm scripts自定义开启指令        

- #### webpack-dev-server 
    启用后，会提供一个简单的web服务器，它不会生成index.html文件，会监察文件的修改，实时地在浏览器（端口号8080）`localhost:8080`中展现出效果.
    ```js
    npm install --save-dev webpack-dev-server  

    //修改webpack.config.js文件
    module.exports = {
        ...,
        devServer: {
            contentBase: './dist'     //这告诉webpack-dev-server基于dist目录下文件生成预览页面
        },
        ...
    }
    ```

- #### webpack-dev-middleware
    目录结构：    
    ```
      webpack-demo
    |- package.json
    |- webpack.config.js
    + |- server.js
    |- /dist
    |- /src
    |- index.js
    |- print.js
  |- /node_modules
    ```
    这是一个会通过webpack将处理后的文件传送到服务器的一个容器，这个工具在webpack-dev-server内部同样也有使用，但是也能独立使用这个包来实现更多的需求
    ```js
    npm install --save-dev express webpack-dev-middleware

    //修改webpack.config.js文件
    module.exports = {
        ...,
        output: {
            ...,
            publicPath: '/'
        }
    }
    ```
    为保证资源会在
    http://localhost:3000下正确访问，接下来将需要在server.js文件中设置自定义的express服务
    ```js
    //server.js

    const express = require('express');
    const webpack = require('webpack');
    const webpackDevMiddleware = require('webpack-dev-middleware');

    const app = express();
    const config = require('webpack.config.js');
    const compiler = webpack(config);

    //告诉express服务使用webpack-dev-middleware和webpack.config.js配置文件作为基底
    app.use(webpackDevMiddleware(compiler, {
        publicPath: config.output.publicPath
    }));

    //在端口3000访问资源
    app.listen(3000, function () {
        console.log('Example app listening on port 3000!\n');
    });
    ```


### 模块热替换HMR(Hot Module Replacement)
能监听模块的变化，并实时地更新模块，而不用重新更新整个页面？         
此功能能提高生产力，我们需要做的是更新我们的webpack-dev-server配置文件和使用webpack内建的HMR插件

注意：如果你使用了 webpack-dev-middleware 而没有使用 webpack-dev-server，请使用 webpack-hot-middleware package 包，以在你的自定义服务或应用程序上启用 HMR。

设置HMR后，启用webpack-dev-server，即可以使用这个功能
```js
//修改webpack.config.js文件
module.exports = {
    ...,
    devServer: {
        contentBase: './dist',
        hot: true   //use the built-in HMR plugin
        //or just use the CLI to modify the webpack-dev-server configuration with the following command:webpack-dev-server --hotOnly   
    },
    ...
}



//设置index.js文件使其能接受其下模块的变化
//index.js
import _ from 'lodash';
...;

function component() {
    ...
}
document.body.appendCHild(component());

if (module.hot) {
    module.hot.accept('./print.js', function() {
        console.log('Accepting the updated printMe module!');
        printMe();
    })
}
```
若想将HMR应用于CSS，只需要配置css-loader和style-loader即可

## 代码分离
>代码分离的好处：此特性能够把代码分离到不同的 bundle 中，然后可以按需加载或并行加载这些文件。代码分离可以用于获取更小的 bundle，以及控制资源加载优先级，如果使用合理，会极大影响加载时间。
目前三种常用的代码分离方法：
- 入口起点(entry points):使用`entry`配置手动地分离代码。
- 防止重复(prevent duplication):使用`SplitChunksPlulgin`去重和分离chunks。
- 动态导入(dynamic imports):通过痛快的内联函数调用来分离代码。
- 