

## 作业一 ：将**奇异值分解**应用于缺失值填补 

#### *[资料一](https://blog.csdn.net/aohun0743/article/details/101702263?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167860675416800215079173%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=167860675416800215079173&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-101702263-null-null.142^v73^control,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=%E4%BD%BF%E7%94%A8%E7%9F%A9%E9%98%B5%E5%88%86%E8%A7%A3%E5%A1%AB%E8%A1%A5%E7%9F%A9%E9%98%B5%E7%A9%BA%E7%BC%BA%E5%80%BC&spm=1018.2226.3001.4187)*

- 用于矩阵近似问题。
- 假设矩阵可以分解成三个矩阵的乘积。其中第一个矩阵是一个方阵，并且是正交的，中间的矩阵通常不是方阵，它对角线上的元素都是由原矩阵的特征值构成的，第三个矩阵也是一个方阵，并且也是正交矩阵。
- 分解时，中间的矩阵不取全部的特征值，而是只取前面若干个最大的特征值，这样就可以对原矩阵进行近似了，两个矩阵之间的近似度一般用[Frobenius 范数](https://blog.csdn.net/weixin_45251808/article/details/102968002)来衡量，即两个矩阵相应元素的平方差累加再开方。（Frobenius 范数（F-范数）**矩阵中每项数的平方和的开方值**）

- **应用于协同过滤（预测用户对电影的评分）：**

​	一般来讲，某个用户对电影评分时，会考虑多个因素，比如电影时长，情节设置，剧情等等，不同用户对这些因素的打分一般也是不同的，某用户对某部电影的评分可以看作这些因素的加权组合。
​	但电影相关的特征很难获取全面，这些特征所依赖的数据很多，可能来自很多因素和源头，对这些特征进行清洗也需要耗费大量的精力。
​	协同过滤有这样一个假设，即过去某些用户的喜好相似，那么将来这些用户的喜好仍然相似。基于这种思想，奇异值分解可以用于预测用户对电影的评分。
​	用户对电影的评分构成的矩阵中通常会存在缺失值，如果某个用户对某部电影没有评分，那么评分矩阵中该元素即为缺失值。预测该用户对某电影的评分等价于填补缺失值。

- **应用于缺失值填补：**

​	每一行是一个样本，每一列是一个特征，这种情形中，每个样本就相当于协同过滤中的某个用户，	每个特征就相当于协同过滤中的某个商品，如此一来，上述情形就有可能扩展到样本的特征缺失情	形中
​	奇异值分解算法并不能直接用于填补缺失值，但是可以利用某种技巧，比如加权法，将奇异值分解	法用于填补缺失值。这种加权法主要基于将原矩阵中的缺失值和非缺失值分离开来。

#### [*资料二*](https://blog.csdn.net/m0_67097397/article/details/127636440)

 矩阵分解常用的三种方法，分别为：
1  ◯特征值分解
2  ◯奇异值分解
3  ◯Funk-SVD
————————————————

矩阵分解原理



矩阵分解算法将 m × n   维的矩阵 R  分解为 m × k  的用户矩阵 P  和 k × n  维的物品矩阵 Q 相乘的形式。其中 m  为用户的数量， n  为物品的数量， k  为隐向量（Latent Factor）的维度。 k  的大小决定了隐向量表达能力的强弱，实际应用中，其取值要经过多次的实验来确定。在得到了 P  用户矩阵和物品矩阵 Q  后，将两个矩阵相乘，就可以得到一个满秩的矩阵。那么，我们就对未被评价过的物品，有了一个预测评分。接下来，可以将评分进行排序，推荐给用户。这就是矩阵分解对于推荐系统最基本的用途。
  **矩阵分解的目的就是通过分解之后的两矩阵内积，来填补缺失的数据，用来做预测评分**。矩阵分解的**核心**是将矩阵分解为两个低秩的矩阵的乘积，分别以 **k  维的隐因子向量**表示，用户向量和物品向量的内积则是用户对物品的偏好度，即预测评分。值得注意的是 k  的选取是通过实验和经验而来的，因此矩阵分解的可解释性不强。
————————————————

***一、特征值分解*** 

  A 为 n阶矩阵，若数 λ 和 n维非0列向量  $ \vec{v}$ 满足 A $ \vec{v}$ =  λ $ \vec{v}$ 那么数 λ称为 A的特征值， $ \vec{v}$ 称为 A的对应于特征值 λ的特征向量。

  可以这样理解： λ 为矩阵变换的大小，  $ \vec{v}$​ 为矩阵变换的方向。但是特征值只能用于方阵，对推荐系统用户——物品的矩阵还不太适合。

**特征值分解**，就是将矩阵$ A$分解为如下式：$A = Q Σ Q ^{− 1}$

  Q是矩阵 A的特征向量组成的矩阵，Σ则是一个对角阵，对角线上的元素就是特征值。我们来分析一下特征值分解的式子，分解得到的Σ矩阵是一个对角矩阵，里面的特征值是由大到小排列的，这些特征值所对应的特征向量就是描述这个矩阵变换方向（从主要的变化到次要的变化排列）。

  我们通过特征值分解得到的前N个特征向量，就对应了这个矩阵最主要的N个变化方向。我们利用这前N个变化方向，就可以近似这个矩阵变换。也就是说：**提取这个矩阵最重要的特征** 。



***二、奇异值分解***
  假设一个矩阵 M 是一个 m × n 的矩阵，则一定存在一个分解：$M = U Σ V^T $

  其中 U 是 m × m 的正交矩阵， V 是 n × n的正交矩阵， Σ 是 m × n 的对角矩阵。 Σ 对角线上的元素就称为 M的奇异值。




***三、Basic Matrix Factorization(Funk-SVD)***  (factorization  因式分解 )

  Funk-SVD的基本思想就是：既然评价指标是**均方根误差**(Root Mean Squared Error, **RMSE**)，那么可以直接通过训练集中的观察值利用最小化RMSE学习用户特征矩阵P和物品特征矩阵Q。为方便表示，用U表示用户的集合，D表示物品的集合，R表示用户评分矩阵。通过这种方法用户和物品可以被映射到一个K维（K可以自己设置）的潜在特征空间。通过挖 掘用户的潜在特征矩阵P（|U|xK维）和物品潜在特征矩阵Q(|D|xK维)来估计评分。即通过下式来得到评分矩阵. $$R≈P×QT=R$$.

因此利用上述公式，可以计算出用户i对物品j的估计评分   $ \hat{r_{ij}} $​  为：

![img](%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.assets/R517UQD%7DMT6OX66KZ7ID%7B%25A.png)             








####  *[资料三](https://blog.csdn.net/weixin_52835157/article/details/115571639?ops_request_misc=&request_id=&biz_id=102&utm_term=%E5%8D%8F%E5%90%8C%E8%BF%87%E6%BB%A4%20%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-1-115571639.142^v73^control,201^v4^add_ask,239^v2^insert_chatgpt&spm=1018.2226.3001.4187)*

协同过滤算法应用和实现

>常用的协同过滤算法分为两种，
>
>**基于用户的协同过滤算法(user-based collaboratIve filtering)**，以及
>
>**基于物品的协同过滤算法(item-based collaborative filtering)**。特点可以概括为“人以类聚，物以群分”，并据此进行预测和推荐。

（这个似乎不是矩阵分解



#### [*资料四*](https://www.cnblogs.com/wuliytTaotao/p/10814770.html)



[矩阵补全（Matrix Completion）和缺失值预处理](https://www.cnblogs.com/wuliytTaotao/p/10814770.html)



#### *[资料五-数学知识](https://blog.csdn.net/manduner/article/details/80564414?ops_request_misc=&request_id=&biz_id=102&utm_term=%E4%BD%BF%E7%94%A8%E7%9F%A9%E9%98%B5%E5%88%86%E8%A7%A3%E5%A1%AB%E8%A1%A5%E7%9F%A9%E9%98%B5%E7%A9%BA%E7%BC%BA%E5%80%BC&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-8-80564414.nonecase&spm=1018.2226.3001.4187)*



[线代里的svd, numpy 的svd以及sklearn的TruncatedSVD](https://blog.csdn.net/deecheanW/article/details/112756983?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167876388616800211548569%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=167876388616800211548569&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-112756983-null-null.142^v73^control,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=U.dot%28np.diag%28truncated_s%29%29.dot%28V%29&spm=1018.2226.3001.4187)



## 使用的函数

[1.](https://blog.csdn.net/rainpasttime/article/details/79831533?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167875937916800192229615%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167875937916800192229615&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-79831533-null-null.142^v73^control,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=np.linalg.svd&spm=1018.2226.3001.4187)    `np.linalg.svd`

函数：np.linalg.svd(a,full_matrices=1,compute_uv=1)。

参数：

a是一个形如(M,N)矩阵

full_matrices的取值是为0或者1，默认值为1，这时u的大小为(M,M)，v的大小为(N,N) 。否则u的大小为(M,K)，v的大小为(K,N) ，K=min(M,N)。

compute_uv的取值是为0或者1，默认值为1，表示计算u,s,v。为0的时候只计算s。

返回值：

总共有三个返回值u,s,v

u大小为(M,M)，s大小为(M,N)，v大小为(N,N)。

A = u*s*v

其中s是对矩阵a的奇异值分解。s除了对角元素不为0，其他元素都为0，并且对角元素从大到小排列。s中有n个奇异值，一般排在后面的比较接近0，所以仅保留比较大的r个奇异值。

 [2.](https://blog.csdn.net/lilong117194/article/details/78397329?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167876015216782425199203%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=167876015216782425199203&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-78397329-null-null.142^v73^control,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=np.mean&spm=1018.2226.3001.4187)

`numpy.mean(a, axis, dtype, out，keepdims )`

mean() 函数定义：
numpy.mean(a, axis, dtype, out，keepdims )

**mean()函数功能：求取均值**
经常操作的参数为axis，以m * n矩阵举例：

axis 不设置值，对 m*n 个数求均值，返回一个实数
axis = 0：压缩行，对各列求均值，返回 1* n 矩阵
axis =1 ：压缩列，对各行求均值，返回 m *1 矩阵



 [3.Python 的输出矩阵的一些常用设置](https://blog.csdn.net/weixin_42175045/article/details/122447449?ops_request_misc=&request_id=&biz_id=102&utm_term=%20py%E8%BE%93%E5%87%BA%E7%9F%A9%E9%98%B5%E6%97%B6%E6%8E%A7%E5%88%B6%E7%B2%BE%E5%BA%A6&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-122447449.nonecase&spm=1018.2226.3001.4187)

- 矩阵输出

限制矩阵的精度以及宽度

```python
    np.set_printoptions(linewidth=300)
    #输出在屏幕中宽度为 300
     
    np.set_printoptions(suppress=True)
    #抑制数值科学计数法表达
     
    np.set_printoptions(precision=6)
    #设置输出中数值的精度
```

- 矩阵的乘法

  ```python
  np.dot(a,b)
  #适用于矩阵内部之间的点乘
   
  np.multiply()
  #适用于矩阵的直积
  ```

  





## 降维模型

[csdn](https://blog.csdn.net/weixin_40844116/article/details/109219001?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167876388616800211548569%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=167876388616800211548569&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-109219001-null-null.142^v73^control,201^v4^add_ask,239^v2^insert_chatgpt&utm_term=U.dot%28np.diag%28truncated_s%29%29.dot%28V%29&spm=1018.2226.3001.4187)





##### csdn-gpt

Q:为什么使用svd可以填补矩阵的空缺值，给出具体推理证明过程和例子

A:

SVD（奇异值分解）是一种矩阵分解方法，可以将一个矩阵分解为三个矩阵的乘积：A = UΣV^T，其中U和V是正交矩阵，Σ是对角矩阵。SVD的一个重要应用是矩阵的降维和压缩，但它也可以用于填补矩阵的空缺值。

具体来说，假设我们有一个矩阵A，其中有一些元素缺失。我们可以使用SVD将A分解为UΣV^T，然后用这个分解来填补缺失值。具体方法是，我们可以将U和V的前k列和Σ的前k个对角元素相乘得到一个近似的矩阵A_k，其中k是一个比缺失值少的数。然后，我们可以用A_k中的值来填补A中的缺失值。

这个方法的原理是，SVD将矩阵分解为一些基本的模式，这些模式可以用来近似矩阵。因此，如果我们知道一个矩阵的一部分值，我们可以使用SVD来推断出缺失值的近似值。

例如，假设我们有一个3x3的矩阵A，其中有一些元素缺失：

| 1    | 2    |      |
| ---- | ---- | ---- |
| 4    |      | 6    |
|      | 8    | 9    |

我们可以使用SVD将A分解为UΣV^T：

U = |-0.34 | 0.93 | 0.16 | |-0.73 | 0.25 |-0.63 | |-0.60 |-0.26 | 0.75 |

Σ = |11.6 | 0   | 0   | | 0  | 3.0 | 0   | | 0  | 0   | 0.3 |

V^T = |-0.45 |-0.89 | 0   | |-0.89 | 0.45 | 0   | | 0   | 0    | 1.0 |

然后，我们可以用U和V的前两列和Σ的前两个对角元素相乘得到一个近似的矩阵A_2：

A_2 = U[:,:2] @ Σ[:2,:2] @ V[:2,:].T

A_2 = | 1.0 | 2.0 | 1.5 | | 4.0 | 7.5 | 6.0 | | 2.4 | 8.0 | 9.0 |

然后，我们可以用A_2中的值来填补A中的缺失值，得到完整的矩阵：

| 1    | 2    | 1.5  |
| ---- | ---- | ---- |
| 4    | 7.5  | 6    |
| 2.4  | 8    | 9    |

因此，使用SVD可以填补矩阵的空缺值。



```python
import numpy as np
from numpy.linalg import svd

def fill_missing_values(M):
# Perform SVD on the matrix M
U, s, Vt = svd(M)
# Replace the singular values with 0
S = np.zeros((M.shape[0], M.shape[1]))
S[:min(M.shape), :min(M.shape)] = np.diag(s)

# Reconstruct the matrix with the modified singular values
M_prime = np.dot(U, np.dot(S, Vt))

return M_prime

M = np.array([[1, 2, np.nan], [4, np.nan, 6], [7, 8, 9]])
M_prime = fill_missing_values(M)
print(M_prime)

```



Q:用python实现利用奇异值分解来填补矩阵空缺值，举例并代码实现

A:

可以使用Python中的numpy库来实现利用奇异值分解来填补矩阵空缺值。以下是一个简单的示例代码：

```python
import numpy as np

# 创建一个5x5的矩阵，其中有一些空缺值
matrix = np.array([[1, 2, np.nan, 4, 5],
                   [6, np.nan, 8, 9, 10],
                   [11, 12, 13, np.nan, 15],
                   [16, np.nan, 18, 19, 20],
                   [21, 22, 23, 24, np.nan]])

# 使用numpy中的linalg库进行奇异值分解
U, s, V = np.linalg.svd(matrix, full_matrices=False)

# 选择一个合适的截断值，将奇异值矩阵中较小的值设为0
truncated_s = np.zeros_like(s)
truncated_s[:2] = s[:2]

# 重构原始矩阵
reconstructed_matrix = U.dot(np.diag(truncated_s)).dot(V)

# 输出重构后的矩阵
print(reconstructed_matrix)


```

在上面的代码中，我们首先创建了一个5x5的矩阵，其中有一些空缺值。然后，我们使用numpy中的linalg库进行奇异值分解，并选择一个合适的截断值，将奇异值矩阵中较小的值设为0。最后，我们使用重构后的矩阵来填补原始矩阵中的空缺值。
