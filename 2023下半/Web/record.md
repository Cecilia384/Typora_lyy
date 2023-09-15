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



#### 9.1

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

js basic 

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

9.15

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

