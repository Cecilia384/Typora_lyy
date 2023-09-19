2023.8.8 23:57

(坑)--为什么直接从网页查询的源码保存在本地然后打开会出现异常？

>1. 缺少相关依赖文件：代码中引用了多个外部样式表和字体文件，如果在本地环境中没有正确配置这些文件的路径或者没有下载这些文件，会导致网页显示不正常。
>2. 编码问题：代码中指定了字符集为utf-8，如果使用的文本编辑器或浏览器默认编码不同，可能会导致中文乱码问题。
>3. 跨域访问问题：代码中引入了外部资源，如果在本地访问时存在跨域限制，浏览器可能会阻止加载这些资源。
>4. JavaScript执行错误：代码末尾的<script>标签可能包含JavaScript代码，如果该代码有语法错误或引用了未定义的变量，可能会导致页面交互功能无法正常工作。
>
>需要注意的是，以上问题只是一些可能出现的情况，并非一定会遇到，具体情况还需要根据实际运行环境来确定。
>
>

2023.8.13

 01:39

睡不着，挑战速成html，做一个简易的页面（其实感觉就是看懂了改一改别人的框架？)

03:22

看完了1h的html速成课，结合菜鸟教程来看确实是大概点了一下（毕竟就1h),感觉和之前java做的那种gui蛮像的，主要还是查表），首先知道一些常用的tag，然后再学学css

（蛮像整一个自己的网站，不过好像也不是那么简单（直接用别人的模板那种）



动画效果

> **视差滚动**

### **Docker**

> Docker 是一种开源的容器化平台，它可以让开发者将应用程序和它们的依赖项打包到一个可移植的容器中，从而实现快速部署、可移植性和可伸缩性。Docker 容器是一种轻量级的、独立的、可执行的软件包，它包含了应用程序和它们的依赖项，可以在任何环境中运行。Docker 可以让你在不同的环境中运行相同的应用程序，从而简化了开发、测试和部署过程。
>
> 例如，你可以使用 Docker 来构建一个 Web 应用程序，并将它打包到一个 Docker 镜像中。然后，你可以将这个镜像上传到 Docker Hub 或其他 Docker 镜像仓库中，并在任何地方使用 Docker 运行这个镜像。这样，你就可以在不同的环境中运行相同的应用程序，而无需担心环境差异或依赖项问题。
>
> 
>
> **Docker和虚拟机有什么区别？**
>
> - Docker 是一种轻量级的容器化技术，它可以在操作系统级别上隔离应用程序和它们的依赖项.
>
> - 虚拟机则是一种完整的虚拟化技术，它可以模拟整个操作系统和硬件环境。
>
> - Docker 容器比虚拟机更轻量级、更快速、更易于部署和管理，因为它们共享操作系统内核和硬件资源。而虚拟机则可以提供更高的隔离性和安全性，因为它们模拟了整个操作系统和硬件环境
>
>   
>
> 关于Docker的信息和**教程**？
>
>  Docker 的官方网站
>
> 可以在 Docker Hub上查找 Docker 镜像和容器。
>
> 



如何使用Docker来构建我的应用程序？

> 你可以使用 Dockerfile 来定义你的应用程序和它们的依赖项，并将它们打包到一个 Docker 镜像中。Dockerfile 是一个文本文件，它包含了一系列指令，用于构建 Docker 镜像。例如，你可以使用以下 Dockerfile 来构建一个 Node.js 应用程序：
>
> ```dockerfile
> FROM node:14
> 
> WORKDIR /app
> 
> COPY package*.json ./
> 
> RUN npm install
> 
> COPY . .
> 
> EXPOSE 3000
> 
> CMD [ "npm", "start" ]
> ```
>
> 
>
> 这个 Dockerfile 定义了一个基于 Node.js 14 的 Docker 镜像，它将应用程序代码复制到容器中，并使用 npm 安装应用程序的依赖项。然后，它将暴露应用程序的端口，并定义了一个启动命令。
>
> 你可以使用以下命令来构建这个 Docker 镜像：
>
> ```dockerfile
> docker build -t my-node-app .
> ```
>
> 这个命令会在当前目录中查找 Dockerfile 文件，并使用它来构建一个名为 my-node-app 的 Docker 镜像。然后，你可以使用以下命令来运行这个镜像：
>
> ```dockerfile
> docker run -p 3000:3000 my-node-app
> ```
>
> 这个命令会在本地主机的 3000 端口上运行这个镜像，并将请求转发到容器内部的 3000 端口。



### 9.1

 Q:请解释

```html
 <meta name="viewport" content="width=device-width,initial-scale=1.0">
<meta http-equiv="X-UA-Compatiable" content="ie=edge">
```

A:


1. `<meta name="viewport" content="width=device-width, initial-scale=1.0">`：这个 meta 用于在移动设备上指定视口的宽度和初始缩放比例。其中的属性含义如下：
   - `name="viewport"`：指定该 meta 元素用于设置视口信息。
   - `content="width=device-width, initial-scale=1.0"`：设定视口的宽度与设备宽度一致，并将初始缩放比例设置为 1。这样能确保移动设备上的网页加载时以设备的实际宽度进行布局，而不会产生缩放。

使用上述 meta 标记可以使访问者在移动设备上进行浏览时，网页内容能够适应视口宽度，并保持正确的缩放比例，提供更好的用户体验。

2. `<meta http-equiv="X-UA-Compatible" content="IE=edge">`：这个 meta 用于在旧版本的 Internet Explorer 浏览器中设置文档的解析和渲染模式。属性含义如下：
   - `http-equiv="X-UA-Compatible"`：指定该 meta 元素用于指示浏览器设置。
   - `content="IE=edge"`：指示浏览器使用最新的渲染模式来解析当前网页，而不是使用 IE 浏览器的兼容模式。

通过设置这个 meta 元素，可能会在旧版本的 IE 浏览器（如 IE8）中强制使用最新的渲染引擎，以确保网页能够正常运行和显示效果。



 9.2

#### JavaScript：验证输入

```js
if(isNaN(x)||x.replace(/(^\s*)|(\s*$)/g,"")==""){
    alert("不是数字");
}
```

#### js basic 

````js
var obj =new Object();//创建一个空对象
var obj2 ={}; 
obj={
    name:"carrot",
    _for:"Max",
    details:{
        color:"orange",
        size:12
    },
    contact:{
        phone:"123-456-7890",
        email:"233@qq.com",
        address:"1234 Main St"
    
    },
}
obj.contact.wechat="123456";
console.log(obj);
console.log(obj.name);
console.log(obj["contact"]["phone"]);
//----array-------
var a =new Array();
var b =[];
a[0]="dog";
a[1]="cat";
a[2]="hen";
b=["dog","monkey","hen"];
console.log(a);
console.log(b);
b.pop();
b.push("fish");

console.log(b);
b.reverse();
b.unshift("lion");//在数组前面添加元素
console.log(b);
var x=5;
console.log(x+5);

 var myString = "Hello World";
 console.log(myString);

 let a=1;
 console.log(a);
 myString = "Hello World 2";
    console.log(myString);
const Pi=3.14;
console.log(Pi);
alert("Hello "+"World");

console.log("hello".length);
console.log("hello".toUpperCase());
console.log("hello".charAt(0));
console.log(Math.random());
console.log("hello".replace("hello","goodbye"));

let age = 25;
console.log(age);   //25

//----闭包-------
function makeAdder(x) { 
    return function(y) { //匿名函数
        return x + y;   //返回一个函数
    };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);
var sum=add5(2); 
console.log(sum);  // 7
console.log(add10(2)); // 12

function sayHello() { //定义一个函数
    console.log("Hello World");
}
sayHello();

````







#### dom

Document Obeject Model

> POM Projecr Obeject Model

### 9.15

````javascript
//How to accept user input in JavaScript
//1.
let username;
document.getElementById("mybutton").onclick = function() {
    username=document.getElementById("mytext").value;
    console.log(username);
    document.getElementById("mylabel").innerHTML ="Hello, " + username;")";
}
//2.
let username1=window.prompt("what's your name?"); console.log(username1);
How to accept user input in JavaScript
 

````



````js
//Math#
let a;
let b;
let c;
a=windows.prompt("Enter side A");
a=Number(a);
b=windows.prompt("Enter side B");
b=Number(b);
c=windows.prompt("Enter side C");
c=Number(c);
c=Math.pow(a,2)+Math.pow(b,2);
c=Math.sqrt(c);
//c=sqrt(Math.pow(a,2)+Math.pow(b,2));

//2.
document.getElementById("submitButton").onclick=function() {
    a=document.getElementById("aText").value;
    a=Number(a);//force transformation to number
    b=document.getElementById("bText").value;
    b=Number(b);
    c=Math.sqrt(Math.pow(a,2)+Math.pow(b,2));
    document.getElementById("cLabel").innerHTML="Side C:"+c;
}
````



```html
 <div class="container">
        <label id = "mylabel">Enter your name:</label><br>
        <input type="text" id="mytext">
        <button type="button" id="mybutton">submit</button><br>
        <script src="main.js"></script><br>
        <label id="aLabel">Side A:</label> 
        <input type="text" id="aText"><br>
        <label id="bLabel">Side B:</label> 
        <input type="text" id="bText"><br>
        <button type="button" id="submitButton">submit</button><br>
        <label id="cLabel">Side C:</label> 

    </div>
```





console.log("side C:",c);



9.19

#### [maven教程](https://www.liaoxuefeng.com/wiki/1252599548343744/1255945359327200)

intro

> Maven是一个Java项目管理和构建工具，它可以定义项目结构、项目依赖，并使用统一的方式进行自动化构建，是Java项目不可缺少的工具。

#### [Log4j](https://logging.apache.org/log4j/2.x/)



intro

> log4j是一个流行的==Java日志记录框架==。它提供了灵活性和可配置性，使开发人员能够进行高效的日志记录和跟踪。
>
> log4j的关键特性包括：
>
> 1. 日志分级：log4j 支持不同级别的日志，如调试（DEBUG）、信息（INFO）、警告（WARN）、错误（ERROR）和致命（FATAL）。通过设置适当的日志级别，可以根据应用程序的需求灵活控制日志输出。
>
> 2. 输出格式：log4j 可以根据配置将日志输出为各种格式，如简单文本、JSON、XML 等。它还支持自定义输出格式，可以根据需求进行定制。
>
> 3. 日志组织和过滤：log4j 可以根据不同的标准来组织和过滤日志。它允许按类、包、时间戳等维度进行过滤。您可以根据自己的需求配置不同类型的过滤器以获取想要的日志信息。
>
> 4. 日志输出位置：log4j 可以将日志输出到各种目标，如控制台、文件、数据库等。您可以选择性地配置一个或多个输出位置。
>
> 5. 异常处理：log4j 可以捕获和记录应用程序中的异常。每当异常发生时，它将会生成一个包含错误信息和堆栈跟踪的日志记录。这有助于调试和查找问题。
>
> 6. 灵活的配置：log4j 提供了配置文件（如 XML 或属性文件）来定义日志记录器、日志输出和其他属性。配置文件可以被动态更改而无需重新编译或重新部署应用程序。
>
> 总之，log4j是一个功能强大且易于使用的日志记录框架，已被广泛应用于Java应用程序的日志记录和跟踪中。通过使用log4j，开发人员可以轻松地获得高质量的日志，并更好地了解和排除应用程序中的问题。



#### [commos logging](https://commons.apache.org/proper/commons-logging/)

intro

> Commons Logging是一个用于在==Java应用程序中实现日志记录的通用日志接口。==它为开发人员提供了一种友好且统一的方式来管理不同日志系统的实现。
>
> Commons Logging的特点如下：
>
> 1. 抽象接口：Commons Logging提供了一个抽象的Logger接口，开发人员可以使用此接口来记录日志。这使得应用程序可以独立于底层的日志具体实现。
>
> 2. 透明的日志实现：Commons Logging可以使用多个日志实现，包括内置的SimpleLog（仅用于开发和调试），以及常见的日志框架如Log4j，JDK Logging等。通过配置适当的类路径和配置文件，开发人员可以轻松切换日志实现，而无需对代码进行更改。
>
> 3. 自动发现和适配：Commons Logging支持自动发现具体的日志实现。它会尝试使用当前环境中存在的所有已知日志实现，并选择适用的实现。这降低了使用和迁移的复杂性。
>
> 4. 日志级别：Commons Logging支持日志级别的定义和控制。您可以使用级别如DEBUG，INFO，WARN和ERROR来控制日志输出的详细程度。这有助于在不同环境中灵活地配置和过滤要输出的信息。
>
> 5. 运行时调整：Commons Logging支持通过更改配置文件动态地调整日志级别。这意味着您可以在不重新编译或重新部署应用程序的情况下更改日志级别，从而有助于故障排除和调试。
>
> 总的来说，Commons Logging赋予了开发人员在Java应用程序中使用日志记录的灵活性和可移植性。它提供了一个简单的接口和对常见日志实现的透明支持，使得日志记录变得高效、可配置和易于管理。



### 9.19

##### （坑）npm报错

1.npm ERR! code E403

> [csdn](https://blog.csdn.net/qq_35664065/article/details/122977681)

2.取消镜像

`npm config set registry https://registry.npmjs.org/`

3.使用镜像

`npm config set registry https://registry.npmmirror.com/`



3.npm publish 出错

> 1.[网络原因](https://www.cnblogs.com/yalong/p/11495661.html)

> npm ERR! code ERR_STRING_TOO_LONG
> npm ERR! Cannot create a string longer than 0x1fffffe8 characters
>
> npm ERR! A complete log of this run can be found in: D:\node_js\node_cache\_logs\2023-09-19T07_31_55_550Z-debug-0.log

(未解决)



[Web.lab crash course](https://weblab.mit.edu/schedule/)



- vs安装插件Prettier Formatter for Visual Studio Code
  - ~~快捷键Ctrl+s(美化格式)~~

double dash : //



##### -css flextbox

https://css-tricks.com/snippets/css/a-guide-to-flexbox/

练习网站

https://flexboxfroggy.com/

http://www.flexboxdefense.com/

> CSS Flexbox是一种用于创建灵活、响应式的布局的CSS模块。Flexbox提供了一套强大的布局工具，使开发者能够轻松地在容器内部对项目进行排序、对齐和分布，以及适应不同尺寸屏幕和设备。
>
> 以下是Flexbox的一些主要特点和概念：
>
> 1. 弹性容器（Flex containers）：使用Flexbox布局的元素称为弹性容器。通过将元素的父级容器设置为`display: flex`，就可以将其转换为弹性容器。
>
> 2. 弹性项目（Flex items）：弹性容器内的每个元素称为弹性项目。弹性项目根据弹性容器的布局规则定位和排列。
>
> 3. 主轴（Main axis）和交叉轴（Cross axis）：弹性容器具有一个主轴和一个交叉轴。默认情况下，主轴是水平轴，交叉轴是垂直轴。弹性项目可以在主轴上排列，也可以在交叉轴上对齐。
>
> 4. 弹性布局属性：通过使用一些简单的CSS属性，开发者可以控制弹性容器和弹性项目的布局样式。这些属性包括`flex-direction`、`justify-content`、`align-items`等，它们控制项目的排序、对齐和分布方式。
>
> 5. 响应式设计：Flexbox能够根据屏幕尺寸和设备特性自动调整布局。它可以很容易地实现响应式设计，并适应各种屏幕大小和设备类型。
>
> Flexbox是一种强大而直观的布局工具，使得构建复杂的网页布局变得更加简单和灵活。它适用于各种场景，包括导航菜单、图片库、网格布局、响应式布局等。学习和掌握Flexbox将使开发人员能够更高效地编写具有吸引力的页面布局。

##### js-function

两种写法

```js
//1.
function sayHello2(name) {
    console.log("Hello " + name);
}
sayHello2("Cecilia");

//2. Syntax: (parameters) => { body };
const celsiusToFahrenheit = (tempC) => { //celcius to fahrenheit
    const tempF = tempC * 1.8 + 32;
    return tempF;
};
console.log(celsiusToFahrenheit(10));   //50
```

-**Callback functions**

```js
const adTwo = x => {
    return x + 2;
};
const modifyArray = (array, callback) => {
    for (let i = 0; i < array.length; i++){
        array[i] = callback(array[i]);
    }
};
let myArray = [5,10,15,20];
modifyArray(myArray, addTwo);	//[7,12,17,22]
```

**Anonymous functions**

Syntax: (parameters) => output;

```js
const modifyArray = (array, callback) => {
    for (let i = 0; i < array.length; i++){
        array[i] = callback(array[i]);
    }
};

let myArray = [5, 10, 15, 20];
modifyArray(myArray, x => {
    return x+2;
});
```

##### - map

