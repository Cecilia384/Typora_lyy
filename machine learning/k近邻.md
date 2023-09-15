探究k值对k近邻算法性能的影响

# [K-近邻算法（KNN)](https://blog.csdn.net/weixin_45884316/article/details/115221211?ops_request_misc=&request_id=&biz_id=102&utm_term=k%E8%BF%91%E9%82%BB%E7%AE%97%E6%B3%95&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-115221211.nonecase&spm=1018.2226.3001.4187)

1.K-近邻算法

 K近邻（K-Nearest Neighbor, KNN）是一种最经典和最简单的有监督学习方法之一。K-近邻算法是最简单的分类器，没有显式的学习过程或训练过程，是懒惰学习（Lazy Learning）。当对数据的分布只有很少或者没有任何先验知识时，K 近邻算法是一个不错的选择。

 K近邻算法既能够用来解决分类问题，也能够用来解决回归问题。该方法有着非常简单的原理：当对测试样本进行分类时，首先通过扫描训练样本集，找到与该测试样本最相似的个训练样本，根据这个样本的类别进行投票确定测试样本的类别。也可以通过个样本与测试样本的相似程度进行加权投票。如果需要以测试样本对应每类的概率的形式输出，可以通过个样本中不同类别的样本数量分布来进行估计。



三个基本要素

 k 值的选择、距离度量和分类决策规则

 

### 2.K-近邻模型

KNN中，当训练集、距离度量、k值及分类决策规则确定后，对于任何一个新的输入实例，它所属的类唯一地确定。这相当于根据上述要素将特征空间划分为一些子空间,确定子空间里的每个点所属的类。

单元(cell)：特征空间中对每个训练实例点x，距离该点比其他点更近的所有点组成的一个区域叫做单元。

类标记( classlabel)：每个训练实例点拥有一个单元，所有训练实例点的单元构成对特征空间的一个划分。❎最近邻法将实例 $\large x_i$的类$\large y_i$作为其单元中所有点的类标记( classlabel)。这样,每个单元的实例点的类别是确定的。图3.1是二维特征空间划分的一个例子。

 



#### 2.1 距离度量

 特征空间中两个实例点之间的距离是二者相似程度的反应，所以K近邻算法中一个重要的问题是计算样本之间的距离，以确定训练样本中哪些样本与测试样本更加接近。
 在实际应用中，我们往往需要根据应用的场景和数据本身的特点来选择距离计算方法。当已有的距离方法不能满足实际应用需求时，还需要针对性地提出适合具体问题的距离度量方法。



#### 2.2 $\large {k} $值的选择

不同k值的影响

一般而言，从 $\large {k} $=1开始，随着的逐渐增大，K近邻算法的分类效果会逐渐提升；在增大到某个值后，随着的进一步增大，K近邻算法的分类效果会逐渐下降。

k值较小，相当于用较小的邻域中的训练实例进行预测，只有距离近的（相似的）起作用

- 单个样本影响大

- “学习”的近似误差(approximation error)会减小，但估计误差(estimation error)会增大

- 噪声敏感

- 整体模型变得复杂，容易发生过拟合

  

k值较大，这时距离远的（不相似的）也会起作用

- 近似误差会增大，但估计误差会减小

- 整体的模型变得简单

  

特例： $\large {k} $= 1  （最近邻算法）

此时，KNN的泛化错误率上界为贝叶斯最优分类器错误率的两倍（证明见最后）



特例：$\large {k} $ = $\large {N} $

K近邻算法对每一个测试样本的预测结果将会变成一样（属于训练样例中最多的类）。

**k值选择**

- 一般k值较小。

- k通常取奇数，避免产生相等占比的情况。
- 往往需要通过**交叉验证(Cross Validation)**等方法评估模型在不同取值下的性能，进而确定具体问题的K值。

————————————————

#### 2.3 分类决策规则

 一般都是多数表决规则(majority voting rule)，即把k个邻近的多数类别作为测试样本的类别



#### [KNN算法优化——kd树](https://blog.csdn.net/m0_61787307/article/details/129504138?spm=1001.2101.3001.6650.3&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EYuanLiJiHua%7EPosition-3-129504138-blog-115221211.235%5Ev31%5Epc_relevant_increate_t0_download_v2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EYuanLiJiHua%7EPosition-3-129504138-blog-115221211.235%5Ev31%5Epc_relevant_increate_t0_download_v2&utm_relevant_index=6)

 前面说到，KNN算法需要测量待分类点(小黑点)和每一个已分类点（各种颜色的圆）的距离，并进行排序，选出其中k个距离最近的圆，再进行投票。这个算法在理解上十分简单，但是，如果当数据集十分大的时候，比如有100万个数据点，此时每个数据点还有几十个特征，那么计算起来将会十分复杂。那么有没有一种方式可以减少这样的计算量呢？

答案是肯定的。

这时候，人们结合数据结构中的二叉树，提出了一种算法——kd树（k-dimensional tree）

kd树可以帮助我们很快地找到与测试点最相邻的k个训练点，而不需要计算每个待分类点与已知分类点的距离。为了方便理解，我们还是举一个例子来说明。
————————————————



#### chat

探究k值对k近邻算法性能的影响，给出具体例子的代码和解释



A:

K近邻算法是一种基于实例的学习方法，是一种简单而有效的分类算法。在该算法中，K代表了最近邻居的数量。这个算法的主要思想是，如果一个样本的K个邻居大多数属于某一类别，那么该样本就属于这一类别。

对于K近邻算法来说，K值的选择是非常重要的。如果K值太小，则样本距离较近的点很容易发生过拟合；而如果K值太大，则可能导致错误的分类和低效率。

下面给出一个简单的Python代码，用于探究K值对K近邻算法性能的影响：

```python
import numpy as np
from sklearn import neighbors, datasets
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

# 加载Iris数据集
iris = datasets.load_iris()
iris_X = iris.data
iris_y = iris.target

# 将数据集划分为训练集和测试集
train_X, test_X, train_y, test_y = train_test_split(iris_X, iris_y, test_size=0.3)

# 创建不同的KNN模型，从K=1到K=25
Ks = range(1, 26)
scores = []
for k in Ks:
    # 创建分类器
    clf = neighbors.KNeighborsClassifier(n_neighbors=k)
    # 训练分类器
    clf.fit(train_X, train_y)
    # 使用测试集进行预测，并计算准确率
    pred_y = clf.predict(test_X)
    score = accuracy_score(test_y, pred_y)
    scores.append(score)

# 显示结果
for k, score in zip(Ks, scores):
    print(f"K值为{k}时的准确率为{score:.2f}。")

# 绘制K值和准确率之间的关系图
import matplotlib.pyplot as plt
plt.plot(Ks, scores)
plt.xlabel('K值')
plt.ylabel('准确率')
plt.show()
```

这个代码将Iris数据集加载到内存中，并且将其划分为训练集（70%）和测试集（30%）。然后，代码创建了K值为1到25的一系列KNN模型，并计算它们在测试集上的准确率。最后，代码将K值和准确率之间的关系可视化展示出来。

使用该代码你可以发现，在K值比较小的时候，模型的准确率比较高；但是，随着K值的增大，准确率开始下降，直到达到一个最低点。因此，选择K值的最佳范围需要根据具体的数据集进行调参。
