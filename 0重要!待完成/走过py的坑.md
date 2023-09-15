

### 安装numpy
 - 报错
 - `EnvironmentNotWritableError: The current user does not have write permissions to the target environment.
     environment location: E:\Anaconda\envs\python37`
  > 错误原因：后面列的那个文件姐缺写入权限
  > 解决方法：找到后面列的那个文件夹（我的是D:\Anaconda）——右键——属性——安全——编辑——完全控制（或者只把写入勾上也行，我是懒人，想一劳永逸）——解决


###  使用pip下载包时
- 报错
- `WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ConnectTimeoutError(<pip._vendor.urllib3.connection.HTTPSConnection object at 0x000002789F76D130>, 'Connection to files.pythonhosted.org timed out. (connect timeout=15)')': /packages/eb/b2/c900168d36abd28b1b08a81387835eff8b574bc6c2e9fefb5c4a38135d94/common-0.1.2.tar.gz`

错误原因： [参照CSDN解决](https://blog.csdn.net/qq_40608730/article/details/120988702)


$$
\hat{\beta }=(X^{T}X)^{-1}X^{T}Y
$$
3.13

ModuleNotFoundError: No module named ‘utils‘

https://blog.csdn.net/weixin_62375715/article/details/129326357



4.21

### [pycharm进行画图，显示不出中文](https://blog.csdn.net/weixin_45314061/article/details/130014785)

经查找学习，找出原因是: Matplotlib 默认情况不支持中文

解决方法：

在绘图前，对代码中添加如下代码：

```python
# 在代码中添加如下语句 —— 设置字体为：SimHei（黑体）



plt.rcParams['font.sans-serif']=['SimHei'] 
```



4.24

[python编码报错：UnicodeDecodeError: 'utf-8' codec can't decode byte 0xbc in position 2: invalid start byt](https://blog.csdn.net/sunflower_sara/article/details/103957385)

>解决问题
>UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc0 in position 2: invalid start byte</font>
>
>解决思路
>Unicode解码错误：“UTF-8”编解码器无法解码位置2中的字节0xBC:无效的起始字节
>
> 
>
>解决方法
>三种方法均可以！
>
>T1、将 encoding=’utf-8’ 改为GB2312、gbk、ISO-8859-1，随便尝试一个均可以！
>
>f = open('txt01.txt',encoding='utf-8')
>each_line = f.readline()
>T2、将 encoding=’utf-8’ 改为gbk
>
>df = pd.read_excel('csv01.csv',encoding='gbk')
>T3、也可以将该csv文件转为utf8编码格式即可打开！
>
>



5.28

[ WARN:0@2.947] global loadsave.cpp:244 cv::findDecoder imread_('D:/eyes_images/EX_data\groudtruth\label_9.jpg'): can't open/read file: check file path/integrity->路径格式不统一

>
>
>\# 设置文件夹路径 main_folder = u"D:/eyes_images/EX_data" label_folder = os.path.normpath(os.path.join(main_folder, "groudtruth")) train_folder = os.path.normpath(os.path.join(main_folder, "QGZ", "train")) test_folder = os.path.normpath(os.path.join(main_folder, "QGZ", "test"))
>
>

在上述代码中，`os.path.normpath()`函数会将`main_folder`、`label_folder`、`train_folder`和`test_folder`中的路径分隔符转换为适合当前操作系统的标准分隔符（正斜杠或反斜杠）。

这样，`label_folder`、`train_folder`和`test_folder`中的路径就会统一使用正斜杠（/）格式。



**isibleDeprecationWarning: Creating an ndarray from ragged nested sequences (which is a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes) is deprecated. If you meant to do this, you must specify 'dtype=object' when creating the ndarray.**
  **return asanyarray(a).ravel(order=order)**
Traceback (most recent call last):
  File "D:\py\myMachineLearning\Final_work\pre1.py", line 108, in <module>
    svm.fit(train_features, np.ravel(train_labels))

>https://blog.csdn.net/superdont/article/details/119726779
>
>该问题非常明确地指出，数组的维度不一致，无法使用np.array()将列表转换成数组。例如，
>
>错误出现场景：
>
>我在整理文件夹下的图像，尝试构造一个array。
>
>实际上，文件夹下面的文件大小不一致，出现了该错误。
>
>**解决方案：把源图像文件设置成同样大小，然后再构造数组。**



5.28

**SyntaxError: Non-UTF-8 code starting with '\xd4' in file**

\# -*- coding: utf-8 -*-
