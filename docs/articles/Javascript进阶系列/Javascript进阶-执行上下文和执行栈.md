## 可执行代码

可执行代码（Executable code）共有三种类型：

**全局代码**：是指全局的 ECMAScript 源代码文本，任何不在函数内部的代码文本都属于全局代码。

**函数代码**：是指提供给 eval 内置函数的源代码文本。

**Eval 代码**：是指作为函数体被解析的源代码文本。

## 上下文执行栈

上下文执行栈（Execution context stack）是 Javascript 引擎创建用于管理存储执行上下文的栈结构。

当 Javascrip 引擎开始执行脚本代码时，就会创建一个全局的执行上下文并且压入当前执行栈。任何时候，当从当前可执行代码转入新的可执行代码时，就会创建一个新的执行上下文压入执行栈中，成为当前运行的执行上下文。

Javascript 引擎首先执行上下文位于栈顶的函数。当函数执行结束时，该执行上下文从执行栈中弹出，执行流程流转到下一个执行上下文。

## 词法环境

**词法环境**是一种规范类型，基于 ECMAScript 代码的词法嵌套结构来定义**标识符**和具体变量和函数声明的关联。一个词法环境由环境记录器和一个可能的引用**外部**词法环境的空值组成。

简单来说**词法环境**是一种持有**标识符—变量映射**的结构。（这里的**标识符**指的是变量/函数的名字，而**变量**是对实际对象[包含函数类型对象]或原始数据的引用）。

词法环境包含两部分：

* **环境记录器**：用于定义变量和函数等声明与作用域内标识符的绑定关系。

* **外部词法环境引用**：用于绑定当前词法环境的父级词法环境，通过外部词法环境引用可构成作**用域链**。

环境记录器有两种类型：

* **声明式环境记录器**：用于定义存储变量声明、函数声明以及参数等绑定关系。
* **对象式环境记录器**：用于定义具体对象（即全局对象）的属性声明与作用域内标识符的绑定关系。

词法环境有两种类型：

* **全局环境**是一个唯一的词法环境，它在任何 js 代码执行前创建。全局环境的环境数据是一个对象式环境记录器，全局环境的外部环境引用为`null`。
* **函数环境**是对应函数代码的词法环境，函数环境的环境数据是一个声明式记录器，内部存储函数内部定义变量，函数环境的外部环境引用取决于函数的定义范围，指向当前词法环境的父级词法环境。

## 执行上下文

执行上下文（Execution context）是解析和执行 Javascript 代码所在环境的抽象概念，每当准备执行全局代码或函数时，就会创建一个执行上下文，执行上下文决定了变量或函数能够访问到哪些数据。

每个执行上下文包含以下部分：**this 绑定**、**词法环境组件**和**变量环境组件**。

执行上下文

在 Javascript 引擎中，执行上下文的创建分为两个阶段：(1)创建阶段 和 (2)执行阶段。

### 创建阶段

####  this 绑定

在全局执行上下文中，this 的值指向全局对象（浏览器环境中，this 指向 window 对象）。

在函数执行上下文中，this 的值取决于函数的调用方式。如果被引用对象调用则 this 指向该对象，否则 this 指向全局对象（严格模式下为 `undefined`）。

#### 词法环境组件

词法环境组件是指一个词法环境对象，用于存储该执行上下文内 let 和 const 变量声明绑定。

#### 变量环境组件

变量环境组件是指一个词法环境对象，和词法环境组件不同的是，其是用于存储该执行上下文内的 var 变量声明绑定和函数声明绑定。

### 执行阶段

![执行上下文栈](images/执行上下文栈.png)