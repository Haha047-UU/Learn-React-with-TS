# Introducting
这本书会学习React和TypeScript,分别了解这两种技术的基础知识。之后将开始学习这两种技术结合使用，使我们能够创建强大的类型安全组件。我们还将详细了解 React 的常用钩子和在应用程序中的使用情况。
# Chapter 1 Introducing React
React用于构建基于组件的前端。TypeScript 它允许用户在 JavaScript 代码中添加丰富的类型系统。
本书涵盖了构建 Web 前端所需的关键主题，如样式、表单和数据获取。
在本章中，我们将介绍以下主题：
## 了解 React 的优势
React广受欢迎的原因是为构建用户界面，组件很好地提供了强大的机制，React 的流行形成了一个庞大的生态系统，其中包括优秀的工具、流行的库和许多经验丰富的开发人员。
组件是UI 的片段，它们可以组合在一起创建前端。此外，组件还可以重复使用。可以被集成到现有的应用程序中，即便使用的是不同框架。这是因为它不需要接管整个应用程序的运行；它乐于作为应用程序前端的一部分运行。
React 组件使用虚拟 DOM（文档对象模型）进行高性能显示。对于真正的DOM，它提供了网页的结构，但对真实的DOM进行更改的代价很高，所以React通过使用真实DOM的内存表示来解决这个问题。
工作原理是在 React 更改实际 DOM 之前，它会生成一个新的虚拟 DOM，并将其与当前的虚拟 DOM 进行比较，以计算出最小值。当前的虚拟 DOM 进行比较，以计算实际 DOM 所需的最小更改量。然后，真实 DOM 将根据这些最小更改进行更新。

## 了解 JSX
JSX是 JavaScript XML 的缩写，JSX 是 React 组件中用于定义组件显示内容的语法。下面的代码片段是一个React组件，其中显示了JSX:
```
function App() {
return (
<div className="App">
<Alert type="information" heading="Success">
Everything is really good!
</Alert>
</div>
);
}
```
看起来想html实际上不是，因为html的div元素没有className属性，也没有Alert元素名称，JSX可以嵌入JS的函数中，JSX 是 JavaScript 语法扩展。
接下来试试在JSX中嵌入一些JS，代码如下：
```
const title = "Oh no!";
<div className="title">
<span>{title}</span>
</div>
```
任何一段 JavaScript 片段都可以用大括号将其嵌入 JSX 中。
总之，JSX 可以看作是 HTML 和 JavaScript 的混合体，用于指定 React 组件的输出。

## 创建组件
### 了解React入口点
React 应用程序的入口点位于 index.js 文件中。
```
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import App from './App';
const rootElement = document.getElementById('root');//将 rootElement 变量分配给 id 为 “root ”的 DOM 元素。
const root = createRoot(rootElement);//React 的 createRoot 函数接收 DOM 元素并返回一个变量，该变量可用于显示 React 组件树，React 的 createRoot 函数允许在一个DOM 元素中呈现。
root.render(
<StrictMode>
<App />
</StrictMode>
);
```
组件和嵌套在其中的 App 组件的 JSX。呈现函数会在页面上显示 React 组件。这一过程通常被称为渲染。
### 了解React组件树
React 应用程序是由组件和 DOM 元素组成的树状结构。根组件是位于组件树顶端的组件。React 组件可以嵌套在另一个 React 组件内部，这是一种功能强大的组件组合方式。
React 组件可以在其 JSX 中引用一个或多个其他组件，甚至 DOM 元素。
## 创建基本警报组件
我们将创建一个显示警报的组件，并将其简单地称为 Alert。它将由一个图标、一个标题和一条消息组成。
重要提示：React 组件名称必须以大写字母开头。如果组件名称以小写字母开头，它将被视为 DOM 元素，无法正常渲染。
创建Alert.js文件，并加入以下代码：
```
function Alert() {
return (
<div>
<div>
<span role="img" aria-label="Warning">⚠</span>
<span>Oh no!</span>
</div>
<div>Something isn't quite right ...</div>
</div>
);
}
```
该组件渲染了：1.警告图标，2.标题"Oh no!",3.消息"Something is not quite right..."
注意：在包含警告图标的 span 元素中添加了 role 和 aria-label 属性，以帮助屏幕阅读器理解这是一张带有警告标题的图片。在React函数组件中，普通函数和箭头函数无明显差别。

## 了解导入和导出
### 了解模块的重要性
默认情况下，JS代码在所谓的全局范围内执行，意味着一个文件的代码可以自动在另一个文件中使用。要注意的是，如果名称相同的函数可能会覆盖其他文件中的函数。
可想而知，这种结构很快就会变得具有挑战性和维护风险。好在JS有模块功能模块的函数和变量是隔离的，因此不同模块中的同名函数不会发生冲突。这是一种更安全的代码结构方式，也是构建 React 应用程序时的常见做法。
### 使用导出语句
模块是一个至少包含一条导出语句的文件。导出语句引用的成员可供其他模块使用。可以理解为在一个文件中导出的文件为公共成员，可以是函数，类或变量。而没有被导出的成员为私有，不能在模块外使用。
默认导出语句有两种变体，以下代码可以展示：
```
export default function myFunc1() {//第一种在成员前面添加 export default 关键字
...
}

export default myFunc1;//第二种在模块底部导出语句
```
### 导入语句
```
import myFunc1 from './myModule';//默认导入语句只能用于引用默认导出语句。

import { myFunc1, myFunc3 } from './myModule';//命名导入语句
```
所以我们将上文提到的Alert组件导出：
```
export function Alert() {
...
}
```
通常的做法是将每个 React 组件放在一个单独的文件中，因此也是一个单独的模块。
在别的文件导入Alert组件的语句是：
```
import { Alert } from './Alert';
```

## Use Props
### 了解 Props
props 是一个传入 React 组件的可选参数。该参数是一个包含我们所选属性的对象。示例如下：
```
function ContactDetails(props) {
console.log(props.name);
console.log(props.email);
...
}
```
在 JSX 中，道具是作为属性传入组件的。道具名称必须与组件中定义的名称一致。
## 使用状态
## 使用事件