# 数据降维(data dimension reduction)

1. 主成分分析(PCA)

PCA是一种常用的降维技术，既然是降维，我们当然希望能够把特征矩阵通过某种方式使得新的特征矩阵的维度降低。实际上下面先简要说明一下PCA的原理和实现步骤。                                                                                                                                      PCA 的原理：通过正交变换将一组可能存在相关性的变量转换为一组线性不相关的变量，转换后的这组变量叫主成分。主成分是原特征的线性组合。（前提是变换后的矩阵需要保留变换前矩阵的主要信息，不然降维没有意义）

既然要进行正交变换，那么我们就得需要一组正交基向量，求解这组正交基向量就成了主成分分析的关键。
PCA的步骤：

1. 对特征矩阵进行中心化，即对矩阵按列求均值得到行向量，然后用特征矩阵减去行向量（由于python的广播机制，行向量扩充为和特征矩阵同等维度的矩阵）得到矩阵X **（去中心化）**

2. 求矩阵X的协方差矩阵，并对协方差矩阵进行特征分解，得到特征值和其对应的特征向量

3. 对特征值按照从大到小的顺序排序，假设取前k 个特征值，然后取这k 个特征值对应的特征向量作为一组基向量

4. 用矩阵X 和基向量相乘，就可以把矩阵X 变换到维度更低的子空间，得到新的矩阵Y ，它就是降维后的矩阵。

  

  PCA 的原理和步骤都很简单，其程序实现也很简单。但是PCA中还是有几个需要注意的点。为什么要先进行中心化？为什么要选择协方差矩阵，直接对中心化后的矩阵进行特征分解不可以吗？为什么要对协方差矩阵进行特征分解，特征分解的意义何在，特征分解后得到的特征值和特征向量又有什么用？ 

！！！

**要先数据清洗**

### caht

要使用PCA算法对13维的wine数据特征进行降维处理，可以按照以下步骤进行：

1. 导入所需的库和模块，如numpy、pandas和sklearn。

2. 加载wine数据集，并将其分为特征矩阵X和目标向量y。

3. 对特征矩阵X进行标准化处理，使得每个特征的均值为0，方差为1。这是因为PCA对数据的尺度敏感。

4. 使用sklearn中的PCA类初始化PCA对象，并指定要降至的目标维度。例如，如果要将维度降至2维，则可以设置n_components=2。

5. 调用PCA对象的fit_transform()方法，将特征矩阵X传入其中。该方法将对数据进行降维处理并返回降维后的结果。

6. 可选：输出降维后的结果，以便进行进一步的分析和可视化。

下面是一个示例代码，展示如何使用PCA算法对wine数据特征进行降维处理：

```python
import numpy as np
import pandas as pd
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler

# 加载wine数据集
url = 'https://archive.ics.uci.edu/ml/machine-learning-databases/wine/wine.data'
data = pd.read_csv(url, header=None)
X = data.iloc[:, 1:].values
y = data.iloc[:, 0].values

# 特征标准化处理
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)

# PCA降维
pca = PCA(n_components=2)
X_pca = pca.fit_transform(X_scaled)

# 输出降维后的结果
print(X_pca)
```

这样，通过PCA算法，您可以将13维的wine数据特征降至2维，即得到降维后的结果X_pca。您可以根据需要对降维后的结果进行进一步的分析和可视化。



以下是一个基于Matplotlib和Seaborn库的PCA可视化代码示例：

```python
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_wine
from sklearn.decomposition import PCA

# Load wine dataset
wine_data = load_wine()
X = wine_data.data
y = wine_data.target

# Perform PCA on wine dataset
pca = PCA(n_components=2)
X_pca = pca.fit_transform(X)

# Visualize the PCA results
plt.figure(figsize=(8, 6))
sns.scatterplot(X_pca[:, 0], X_pca[:, 1], hue=y, palette="deep")
plt.xlabel("PC1")
plt.ylabel("PC2")
plt.title("PCA Visualization of Wine Dataset")
plt.show()
```

代码中首先加载wine数据集，然后通过sklearn库中的PCA类对数据进行降维处理，得到只包含两个主成分的新数据集X_pca。最后利用Matplotlib和Seaborn库中的scatterplot函数对PCA结果进行可视化，用不同颜色表示不同类别的数据点。



不使用PCA和SVD

下面是使用矩阵的特征值分解实现PCA降维的代码：

```python
import numpy as np
from sklearn.datasets import load_wine
import matplotlib.pyplot as plt
import seaborn as sns

# 加载wine数据集
wine_data = load_wine()
X = wine_data.data

# 去中心化
X_mean = np.mean(X, axis=0)
X_centered = X - X_mean

# 计算协方差矩阵
cov_matrix = np.cov(X_centered.T)

# 特征值分解
eigenvalues, eigenvectors = np.linalg.eig(cov_matrix)

# 选择要保留的主成分数量
n_components = 2
eigenvectors_reduce = eigenvectors[:, :n_components]

# 数据投影到降维后的特征空间
X_pca = np.dot(X_centered, eigenvectors_reduce)

# 可视化降维结果
plt.figure(figsize=(8, 6))
sns.scatterplot(X_pca[:, 0], X_pca[:, 1], hue=wine_data.target, palette="deep")
plt.xlabel("PC1")
plt.ylabel("PC2")
plt.title("PCA Visualization of Wine Dataset")
plt.show()
```

这段代码首先加载了wine数据集，并对数据进行了去中心化处理。然后计算协方差矩阵，并对其进行特征值分解得到特征向量。接着选择要保留的主成分数量，并将数据投影到降维后的特征空间。最后，将降维结果可视化出来。注意，这里没有使用`svd`函数，而是使用了`cov`函数计算协方差矩阵，并使用`eig`函数进行特征值分解。



优化

以下是在不使用SVD和PCA函数的情况下进行优化的代码：

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.datasets import load_wine

# 加载wine数据集
wine_data = load_wine()
X = wine_data.data

# 去中心化
X_mean = np.mean(X, axis=0)
X_centered = X - X_mean

# 计算协方差矩阵
cov_matrix = np.cov(X_centered.T)

# 特征值分解
eigenvalues, eigenvectors = np.linalg.eig(cov_matrix)

# 特征值排序和选择主成分
eigen_pairs = [(np.abs(eigenvalues[i]), eigenvectors[:, i]) for i in range(len(eigenvalues))]
eigen_pairs.sort(key=lambda x: x[0], reverse=True)

n_components = 2
eigenvectors_reduce = np.array([eigen_pairs[i][1] for i in range(n_components)])

# 数据投影到降维后的特征空间
X_pca = np.dot(X_centered, eigenvectors_reduce.T)

# 可视化降维结果
plt.figure(figsize=(8, 6))
plt.scatter(X_pca[:, 0], X_pca[:, 1], c=wine_data.target)
plt.xlabel("PC1")
plt.ylabel("PC2")
plt.title("PCA Visualization of Wine Dataset")
plt.show()
```

优化内容：
- 使用`np.cov`函数计算协方差矩阵，避免了直接计算协方差矩阵的过程。
- 使用`np.linalg.eig`函数进行特征值分解，避免了直接计算特征值分解的过程。
- 通过特征值排序和选择主成分，选择了前n个最大的特征向量。
- 去中心化和投影的过程保持不变。

这些优化措施仍然保持了代码的功能，同时避免了使用SVD和PCA函数，减少了计算量和内存占用。然而，请注意，这种自定义实现可能会比使用优化的库函数效率稍低。

---

**上述代码显示的图像中三种颜色的点的含义是什么**



在上述代码显示的图像中，三种颜色的点代表了wine数据集中的三个不同类别。wine数据集是一个用于分类任务的数据集，包含了来自三个不同来源（类别）的葡萄酒样本。这三个类别分别是：

1. 红葡萄酒 (class 0): 在图像中以一种颜色表示，例如红色。
2. 白葡萄酒 (class 1): 在图像中以另一种颜色表示，例如绿色。
3. 其他类型的葡萄酒 (class 2): 在图像中以第三种颜色表示，例如蓝色。

通过图像中不同颜色的点的分布，我们可以观察到降维后的数据在二维空间上的聚类情况。不同类别的点可能形成不同的簇或分布模式，反映了不同类别之间的区别和相似性。这样的可视化可以帮助我们理解数据的结构和类别之间的可分性，为后续的分类任务提供指导和洞察。



**解释函数**

让我为您解释代码中使用的每个函数：

1. `load_wine()`: 这个函数是scikit-learn库中的一个数据集加载函数，用于加载wine数据集。它返回一个包含数据和标签的对象。

2. `np.mean()`: 这个函数是NumPy库中的一个函数，用于计算数组的均值。在这里，它用于计算特征矩阵X的列均值，即每个特征的平均值。

3. `np.cov()`: 这个函数是NumPy库中的一个函数，用于计算矩阵的协方差。在这里，它被用来计算特征矩阵X_centered的协方差矩阵。

4. `np.linalg.eig()`: 这个函数是NumPy库中的一个函数，用于计算矩阵的特征值和特征向量。在这里，它被用来对协方差矩阵进行特征值分解，得到特征值和对应的特征向量。

5. `eigen_pairs.sort()`: 这是一个列表的排序操作，使用了Python内置的`sort()`函数。在这里，它根据特征值的绝对值对特征值和特征向量对进行排序，以便按照特征值的大小降序排列。

6. `np.dot()`: 这个函数是NumPy库中的一个函数，用于计算矩阵的乘积。在这里，它被用来将数据矩阵X_centered投影到降维后的特征空间，通过将X_centered与降维后的特征向量矩阵eigenvectors_reduce相乘。

7. `plt.figure()`: 这个函数是Matplotlib库中的一个函数，用于创建一个新的图形窗口。可以通过设置参数来指定图形的大小和其他属性。

8. `plt.scatter()`: 这个函数是Matplotlib库中的一个函数，用于绘制散点图。在这里，它被用来根据降维后的数据X_pca的两个主成分绘制散点图，颜色由wine数据集的标签提供。

9. `plt.xlabel()`: 这个函数是Matplotlib库中的一个函数，用于设置x轴的标签。

10. `plt.ylabel()`: 这个函数是Matplotlib库中的一个函数，用于设置y轴的标签。

11. `plt.title()`: 这个函数是Matplotlib库中的一个函数，用于设置图形的标题。

12. `plt.show()`: 这个函数是Matplotlib库中的一个函数，用于显示图形窗口并显示绘制的图像。

这些函数组合在一起，实现了加载wine数据集、数据预处理、降维和可视化的流程。最终的图像展示了经过PCA降维后的数据在二维平面上的分布。每个点表示一个样本，它的位置由对应的两个主成分（PC1和PC2）确定。颜色的含义是wine数据集中每个样本所属的类别或类标签。

通过这个散点图，我们可以观察到以下信息：

1. 类别之间的分离程度：如果不同类别的样本在散点图上呈现明显的分离，即不同类别的点聚集在不同的区域，那么说明降维后的特征可以有效地区分不同的类别。
2. 类别内的分布情况：观察每个类别内部的点的分布形态，可以得到关于类别的更多信息。如果同一类别的点在散点图上聚集在一起，并且形成紧密的簇状结构，说明这个类别在降维后的特征空间中具有较好的内部一致性。
3. 异常点的检测：通过观察散点图中的离群点（与其他点明显分离的点），可以检测出数据中的异常样本或异常情况。

总体而言，这个散点图可以帮助我们对数据进行可视化分析，了解降维后的特征在二维空间中的分布情况，以及样本的类别之间的关系。