==**！！学习过程写博客自己整理记录EVERDAY！！**==



## 关于写博客

1.自己建博客网站（要成本，要维护，现在先排除这个方式

2.CSDN，**博客园**，**知乎**，微信公众号等（优选，有账号的平台（github先不发，整理好了一起上传吧）都发哈哈哈

3.画流程图mermaid（**学一下**）[link](https://github.com/mermaid-js/mermaid)



6.19

Linux



6.29

c++/c ，visual studio开发



 `getline()`函数从外部读取一行；

 `ignore() `函数会忽略掉之前读语句留下的多余字符。



#### 7.2

[（坑）vscode：四个乱码问题及解决方法](https://blog.csdn.net/weixin_50697073/article/details/122789632?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-122789632-blog-104277310.235^v38^pc_relevant_sort_base2&spm=1001.2101.3001.4242.1&utm_relevant_index=3)



#### 7.3

- **命名空间**:本质上，命名空间就是定义了一个范围。



- [（坑）没有与这些操作数匹配的 "<<" 运算符 操作数类型为: std::ostream << std::string](https://www.cnblogs.com/swjtumao/p/10548790.html)

  

##### C++ 预处理器



>预处理器是一些指令，指示编译器在实际编译之前所需完成的预处理。
>
>所有的预处理器指令都是以井号（#）开头，只有空格字符可以出现在预处理指令之前。预处理指令不是 C++ 语句，所以它们不会以分号（;）结尾。
>
>我们已经看到，之前所有的实例中都有 **#include** 指令。这个宏用于把头文件包含到源文件中。
>
>C++ 还支持很多预处理指令，比如 #include、#define、#if、#else、#line 等，让我们一起看看这些重要指令。
>
>## #define 预处理
>
>\#define 预处理指令用于创建符号常量。该符号常量通常称为**宏**，指令的一般形式是：
>
>```
>#define macro-name replacement-text 
>```
>
>当这一行代码出现在一个文件中时，在该文件中后续出现的所有宏都将会在程序编译之前被替换为 replacement-text。例如：
>
>```cpp
>#include <iostream> 
>using namespace std;  
>#define PI 3.14159  
>int main () {     
>    cout << "Value of PI :" << PI << endl;      
>    return 0; 
>}
>```
>
>
>
>##  参数宏
>
>您可以使用 #define 来定义一个带有参数的宏，如下所示：
>
>```cpp
>#include <iostream>
>using namespace std;
> 
>#define MIN(a,b) (a<b ? a : b)
> 
>int main ()
>{
>   int i, j;
>   i = 100;
>   j = 30;
>   cout <<"较小的值为：" << MIN(i, j) << endl;
> 
>    return 0;
>}
>```
>
>
>
>##  条件编译
>
>有几个指令可以用来有选择地对部分程序源代码进行编译。这个过程被称为条件编译。
>
>条件预处理器的结构与 if 选择结构很像。请看下面这段预处理器的代码：
>
>```cpp
>#ifdef NULL
>   #define NULL 0
>#endif
>```
>
>您可以只在调试时进行编译，调试开关可以使用一个宏来实现，如下所示：
>
>```cpp
>#ifdef DEBUG
>   cerr <<"Variable x = " << x << endl;
>#endif
>```
>
>如果在指令 #ifdef DEBUG 之前已经定义了符号常量 DEBUG，则会对程序中的 **cerr** 语句进行编译。您可以使用 `#if 0 `语句**注释掉**程序的一部分，如下所示：
>
>```cpp
>#if 0
>   不进行编译的代码
>#endif
>```
>
> 



##### # 和 ## 运算符



\# 和 ## 预处理运算符在 C++ 和 ANSI/ISO C 中都是可用的。

'#'  运算符会==把 replacement-text 令牌转换为用引号引起来的字符串。==

'##' 运算符用于连接两个令牌。下面是一个实例：

```cpp
#define CONCAT( x, y )  x## y
```

==**#** 和 **##** 运算符==

==**#**== 字符串化的意思，出现在宏定义中的#是把跟在后面的参数转换成一个字符串。

当用作字符串化操作时，# 的主要作用是将宏参数不经扩展地转换成字符串常量。

-  宏定义参数的左右两边的空格会被忽略，参数的各个 Token 之间的多个空格会被转换成一个空格。
-  宏定义参数中含有需要特殊含义字符如"或\时，它们前面会自动被加上转义字符 \。

==**##**== 连接符号，把参数连在一起。

将多个 Token 连接成一个 Token。要点：

-  它不能是宏定义中的第一个或最后一个 Token。

-  前后的空格可有可无。

  ---

  

  

C++ 提供了下表所示的一些预定义宏：

| 宏       | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| __LINE__ | 这会在程序编译时包含当前行号。                               |
| __FILE__ | 这会在程序编译时包含当前文件名。                             |
| __DATE__ | 这会包含一个形式为 month/day/year 的字符串，它表示把源文件转换为目标代码的日期。 |
| __TIME__ | 这会包含一个形式为 hour:minute:second 的字符串，它表示程序被编译的时间。 |

 example

```cpp
#include <iostream>
using namespace std;
 
int main ()
{
    cout << "Value of __LINE__ : " << __LINE__ << endl;
    cout << "Value of __FILE__ : " << __FILE__ << endl;
    cout << "Value of __DATE__ : " << __DATE__ << endl;
    cout << "Value of __TIME__ : " << __TIME__ << endl;
 
    return 0;
}
```

##### **unistd.h**

`#include <unistd.h>`提供了一些与系统调用（system calls）和常见的POSIX函数相关的声明。该头文件主要在Unix-like系统上使用。

`<unistd.h>` 头文件中包含了一些常见函数的声明，如：

- `read()`：从文件描述符中读取数据
- `write()`：向文件描述符写入数据
- `sleep()`：让程序暂停执行一段时间
- `fork()`：创建一个新的进程
- `exec()` 系列函数：用于在当前进程中执行一个新程序
- 等等...

这些函数通常用于处理与操作系统相关的任务，例如文件I/O、进程控制和系统调用等。

请注意，`<unistd.h>` 是一个标准的C/C++库头文件，但并不是所有的编译器都提供该头文件。因此，在使用该头文件之前，请确保您的编译器支持该头文件，并且您在正确的编译环境中使用它。





- [（坑）windows下VS 无法打开源文件 unistd.h](https://blog.csdn.net/Dashi_Lu/article/details/90054696)

 

#### 8.22

(真是隔了一个月没学习了……愧疚感促使行动力了hhh)

- 下载visual studio和unity（不知道为什么unity学生认证一直不行呜呜）
- 在.NET上使用c#， 看着例子学了基本的操作（和JAVA GUI好像
- unity入门（未完成
- 决定选题（未



#### .pak 

一种文件扩展名，通常用于表示文件存档或打包文件。它是一种常见的文件格式，用于将多个文件或目录打包成单个文件，以便进行方便的传输、存储或共享。

.pak 文件可以包含各种不同类型的数据，例如游戏资源文件、应用程序资源文件、图像、音频、视频、文本等。这些文件被打包为一个二进制文件，可以通过特定的软件或工具进行解包和提取其中的内容。

.pak 文件的具体格式和结构可以因使用的软件或应用而有所不同，因此需要使用相应的解包工具来打开或提取其中的文件。

请注意，尽管 .pak 文件是一种常见的文件类型，但不同的软件或应用程序可能使用相同的文件扩展名，并且其文件格式可能会有所不同。因此，要正确处理和解释 .pak 文件，最好查阅相关软件或应用的文档或支持资料，了解其具体的文件格式和使用方式。



#### 8.22

[ 适用于PHP初学者的学习线路和建议](https://www.runoob.com/w3cnote/php-learning-recommend.html)

（坑）Visual Studio如何在一个Project下运运行不同的main函数代码

> [csdn](https://blog.csdn.net/qq_24123029/article/details/103910061)  在不期望生成的源文件，右击属性->从生成中排除



8.23

像素风绘画软件

Pixly

#### 8.28

vc code 配置文件保存

launch.json

```cpp
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        
        {
            "name": "(gdb) 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "输入程序名称，例如 ${workspaceFolder}/a.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "/path/to/gdb",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ]
        },
        {
            "name": "(gdb) 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "D:\\mingw64\\bin\\g++.exe",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description":  "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ]
        },
        {
            "name": "(gdb) Windows 上的 Bash 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "输入程序名称，例如 ${workspaceFolder}/a.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "pipeTransport": {
                "debuggerPath": "/usr/bin/gdb",
                "pipeProgram": "${env:windir}\\system32\\bash.exe",
                "pipeArgs": ["-c"],
                "pipeCwd": ""
            },
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description":  "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ]
        },
        {
            "name": "g++.exe build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "D:\\mingw64\\bin\\gdb.exe",	
            /*"D:\mingw64\bin\gdb.exe"	
            /*修改成自己bin目录下的gdb.exe，这里的路径和电脑里复制的文件目录有一点不一样，这里是两个反斜杠\\*/
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "task g++"
        }
    ]
}




```

8.29







8.30



菜单嵌套功能







AVL例子











二叉排序例



##### 指向指针的 指针

Q:请详细解释一下Student** 类型的指针的用法`Student**` 类型的指针是一个指向 `Student*` 类型指针的指针。该类型的指针用来操作 `Student*` 类型的指针，提供对指针的间接控制能力。

在 C 语言中，函数的形参采用值传递的方式，即在函数调用时，实参的值会被拷贝一份传递给函数形参。所以，当我们需要在函数内部修改一个指针的值时，直接传递指针本身是不够的。这时，我们可以采用传递指向指针的地址 ，即使用 `Student**` 类型的指针。

在函数中，通过 `Student**` 类型的指针，我们可以获得指向指针的指针，即得到指针本身的地址，在函数内部通过修改该地址所存储的值，可以改变指针指向的内容。

示例 1：使用 `Student*` 类型的指针：

```c
void modifyPointer(Student* ptr) {
    ptr = NULL;
}

int main() {
    Student* student = (Student*)malloc(sizeof(Student));
    modifyPointer(student);
    // 在 modifyPointer 函数中将指针指向 NULL，并不会影响 main 函数中的指针值

    // do something with the student pointer...

    return 0;
}
```

在上述示例中，我们在 `modifyPointer` 函数内部将指针 `ptr` 修改为 `NULL`，但该修改不会反映到 `main` 函数中的指针 `student`。

示例 2：使用 `Student**` 类型的指针：

```c
void modifyPointer(Student** ptr) {
    *ptr = NULL;
}

int main() {
    Student* student = (Student*)malloc(sizeof(Student));
    modifyPointer(&student);
    // 在 modifyPointer 函数中修改了指针指向的值为 NULL

    // do something with the student pointer...

    return 0;
}
```

在上述示例中，我们通过将 `&student` 传递给 `modifyPointer` 函数来获得指向指针 `student` 的指针的地址（`Student**` 类型的指针），然后通过 `*ptr` 访问该指针并将其值修改为 `NULL`。这样，影响将会在 `main` 函数中体现出来， `student` 指针指向的内容将被设置为 `NULL`。

在学生信息管理系统的例子中，我们将 `Student*` 类型的指针传递给 表示学生信息链表的 `Student**` 类型的指针，通过修改指针的值来添加/删除学生节点。

总结来说，`Student**` 类型的指针可以更改指向 `Student*` 类型的指针本身的值，从而实现间接控制指针的目的。



 



#### 9.1

(坑)C语言：使用`system("cls");`有时候会出现之前的输出还没有来得及显示就被清除了，如果想要看到之前的输出，可以在printf语句下面加一句`system("pause");`



(坑）关于时不时出现的段错误--可能的原因

1.指针型变量未初始化，指空了

2.分配内存时出错（感觉很玄学，不知道怎么出现的）



9.11

#### web学习顺序

> 你好，这是Bing。你的问题很好，我会尽力回答。首先，我建议你按照以下顺序学习：
>
> 1. **HTML**：HTML是网页的基础，它定义了网页的结构和内容。因此，学习HTML是学习Web开发的第一步。你可以从MDN Web Docs或W3Schools开始学习。
> 2. **CSS**：CSS用于控制网页的样式和布局。学习CSS可以让你更好地控制网页的外观和感觉。你可以从MDN Web Docs或W3Schools开始学习。
> 3. **JavaScript**：JavaScript是一种编程语言，用于为网页添加交互性和动态效果。学习JavaScript可以让你更好地掌握Web开发。你可以从MDN Web Docs或W3Schools开始学习。
> 4. **PHP**：PHP是一种服务器端脚本语言，用于创建动态Web页面。学习PHP可以让你更好地掌握服务器端编程。你可以从PHP官方文档或W3Schools开始学习。
> 5. **MySQL**：MySQL是一种关系型数据库管理系统，用于存储和管理数据。学习MySQL可以让你更好地掌握数据管理和查询技能。你可以从MySQL官方文档或W3Schools开始学习。
> 6. **SQL**：SQL是一种结构化查询语言，用于与关系型数据库进行交互。学习SQL可以让你更好地掌握数据管理和查询技能。你可以从W3Schools或SQLZoo开始学习。
>
> 以上是一个合理的学习顺序，但也取决于你的兴趣和目标。如果你想成为一个全栈Web开发人员，那么还需要了解其他技术，如服务器端框架（如Node.js、Ruby on Rails等）和前端框架（如React、Angular等）。
>
> 关于网站搭建的完整流程，这里提供一个大致的流程：
>
> 1. **规划**：确定网站的目标、受众、内容和功能，并创建一个网站地图。
> 2. **设计**：设计网站的外观和感觉，并创建原型。
> 3. **开发**：使用HTML、CSS、JavaScript等技术来实现网站，并将其部署到Web服务器上。
> 4. **测试**：测试网站以确保其在各种设备和浏览器上都能正常工作，并修复任何错误。
> 5. **发布**：将网站发布到生产环境中，并确保其可用性和安全性。
> 6. **维护**：定期更新网站内容、修复错误并添加新功能。
> 7. [1. freecodecamp.org](https://www.freecodecamp.org/news/beginners-roadmap-web-development/)
> [2. developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Learn)
> [3. geeksforgeeks.org](https://www.geeksforgeeks.org/can-start-learn-web-development/)
> [4. turing.com](https://www.turing.com/resources/web-development-process)
> [5. marceldigital.com](https://www.marceldigital.com/blog/website-development-process-a-step-by-step-guide)
> [6. techuz.com](https://www.techuz.com/blog/web-development-process-a-guide-to-complete-web-development-life-cycle/)
> [7. velvetech.com](https://www.velvetech.com/blog/web-development-process/)
>
>  

部署到服务器上具体该怎么一步一步实现呢

> 将网站部署到服务器上需要以下步骤：
>
> 1. **选择Web服务器**：选择一个Web服务器，例如Apache或Nginx。这些服务器可以在Linux、Windows或macOS上运行。
> 2. **选择操作系统**：选择一个操作系统，例如Linux或Windows。大多数Web服务器都支持Linux，因为它是免费的，并且具有出色的性能和安全性。
> 3. **安装Web服务器**：安装所选的Web服务器。这通常涉及到下载和安装软件包，然后配置服务器以便它可以运行您的网站。
> 4. **编写网站代码**：使用HTML、CSS、JavaScript、PHP等技术编写您的网站代码。您可以使用文本编辑器（例如Notepad++或Sublime Text）或集成开发环境（例如Visual Studio Code）来编写代码。
> 5. **上传代码**：将您的网站代码上传到Web服务器。您可以使用FTP客户端（例如FileZilla）或版本控制系统（例如Git）来上传代码。
> 6. **配置域名**：如果您有自己的域名，则需要将其指向您的Web服务器。这通常涉及到在域名注册商处进行设置。
> 7. **测试网站**：测试您的网站以确保它在各种设备和浏览器上都能正常工作，并修复任何错误。
>
>  [1. codecademy.com](https://www.codecademy.com/learn/deploy-a-website)
>
> [2. shopify.com](https://www.shopify.com/partners/blog/deploy-website)
>
> [3. developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/Publishing_your_website)



#### 9.14

(坑)本地分支上传到github上出错

> 1.fatal: unable to access 'https://github.com/Cecilia384/gamemaker_1.git/': ==OpenSSL SSL_read: Connection was reset, errno 10054==

可能原因
1. DNS 解析出现问题

    在 cmd 窗口输入 ipconfig/flushdns ，清除缓存后再重新进行 git 操作即可

2. 防火墙或代理设置

    取消代理

        git config --global --unset http.proxy
        
        git config --global --unset https.proxy




[csdn](https://blog.csdn.net/Skybububu/article/details/132379910)

> 2.fatal: unable to access 'https://github.com/Cecilia384/gamemaker_1.git/': 
>
> ==Failed to connect to github.com port 443 after 21143 ms: Timed out==



[csdn](https://blog.csdn.net/ReCclay/article/details/121254869)

http上传超时了，改为ssh重新推送

```assembly
git remote rm origin
git remote add origin git@github.com:xxx/yyy.git
git push origin master

```



> 3.Permission denied (publickey). fatal: Could not read from remote repository. Please make sure you have the correct access rights and the repository exists.

[csdn](https://blog.csdn.net/helloasimo/article/details/123778112)

修改git里的全局用户名和邮箱（和github保持一致）

> 进入git bash界面然后：
> 第1步，git config --global --list 验证邮箱与GitHub注册时输入的是否一致
>
>  可以通过git config --global user.name “yourname”，git config --global user.email “email@email.com ”（这里得名字和邮箱都是注册github时用的）设置全局用户名和邮箱。
>
> 第2步，ssh-keygen -t rsa -C “这里换上你的邮箱”，一路回车(注意：不需要输入其他内容），直到生成密钥。
>
> 根据上面地址和文件名可知， 会在/Users/***/路径下生成一个.ssh\id_rsa.pub文件，密钥就存储在其中:
>
> **第3步**，使用浏览器到git仓库，添加秘钥
>
> 右上角--> settings --> SSH and GPG keys ....
>
> **第4步**，ssh -T git@github.com 测试一下通不通，通了显示如下



#### 9.15

需要了解

- [ ] Redies

- [ ] maven

- [ ] Gradle

- [ ] [Tomcat服务器](https://blog.csdn.net/qq_38490457/article/details/108440922?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522169473694316800186533185%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=169473694316800186533185&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-108440922-null-null.142^v94^chatsearchT3_1&utm_term=tomcat&spm=1018.2226.3001.4187)

- [ ] MVC

- [ ] servlet

   
  
  ？如何设计一个网站，可以在线浏览电子书
  
  > 界面：一个书架的样式，有分类索引
  >
  > admin: 管理图书数据（pdf） ==？怎么存储这些pdf到网上，NAS ?==
  >
  > 用户浏览：要让其他人可以通过网址访问，==如何注册域名,如何连接服务器==

?注册域名和有自己的云服务器有什么关联和作用



daily

[js_course](https://www.bilibili.com/video/BV145411D7QL?p=10&spm_id_from=pageDriver&vd_source=8539000814a4ae2faefd4a32086c5afc)

(10p /day --> 10day fin)
