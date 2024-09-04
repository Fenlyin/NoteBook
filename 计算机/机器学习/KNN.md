KNN(K Nearest Neighbor) 算法用来解决分类与回归问题。

KNN是惰性学习方法，即在训练后不会建立模型，而是将所有的训练集储存起来，通过比较测试样本与训练样本的相似性做分类和回归。

# 优缺点

**优点**：
- 原理简单，易于实现。
- 对于非线性问题有很好的处理能力。
- **无需事先构建全局模型**，灵活性高。

**缺点**：

- **计算量大**，特别是对于大数据集，每次预测都需要遍历整个训练集。
- **对噪声数据敏感**，因为预测结果完全依赖于最近的K个邻居。
- 预测结果的可解释性相对较差。


>### What is the difference between KNN, and K means?
>- KNN is a supervised machine learning model used for classification problems whereas K-means is an unsupervised machine learning model used for clustering.
>- The “K” in KNN is the number of nearest neighbors whereas the “K” in K means is the number of clusters.


# python实现
```python
import math

def classifyAPoint(points,p,k=3):
    '''
     This function finds the classification of p using
     k nearest neighbor algorithm. It assumes only two
     groups and returns 0 if p belongs to group 0, else
      1 (belongs to group 1).

      Parameters - 
          points: Dictionary of training points having two keys - 0 and 1
                   Each key have a list of training data points belong to that 

          p : A tuple, test data point of the form (x,y)

          k : number of nearest neighbour to consider, default is 3 
    '''

    distance=[]
    for group in points:
        for feature in points[group]:

            #calculate the euclidean distance of p from training points 
            euclidean_distance = math.sqrt((feature[0]-p[0])**2 +(feature[1]-p[1])**2)

            # Add a tuple of form (distance,group) in the distance list
            distance.append((euclidean_distance,group))

    # sort the distance list in ascending order
    # and select first k distances
    distance = sorted(distance)[:k]

    freq1 = 0 #frequency of group 0
    freq2 = 0 #frequency og group 1

    for d in distance:
        if d[1] == 0:
            freq1 += 1
        elif d[1] == 1:
            freq2 += 1

    return 0 if freq1>freq2 else 1

# driver function
def main():

    # Dictionary of training points having two keys - 0 and 1
    # key 0 have points belong to class 0
    # key 1 have points belong to class 1

    points = {0:[(1,12),(2,5),(3,6),(3,10),(3.5,8),(2,11),(2,9),(1,7)],
              1:[(5,3),(3,2),(1.5,9),(7,2),(6,1),(3.8,1),(5.6,4),(4,2),(2,5)]}

    # testing point p(x,y)
    p = (2.5,7)

    # Number of neighbours 
    k = 3

    print("The value classified to unknown point is: {}".\
          format(classifyAPoint(points,p,k)))

if __name__ == '__main__':
    main()

```

## 数据标准化
特征标准化（Feature Standardization）是数据预处理的一个重要步骤，它通过将特征值缩放到一个给定的最小值和最大值之间（通常是0和1），或者通过计算特征值的均值（mean）和标准差（standard deviation），然后将每个特征值减去均值后除以标准差来实现。后者是最常用的标准化方法，也被称为Z-score标准化。

### Z-score标准化的好处：
1. 使得每个特征的平均值为0。
2. 使得每个特征的标准差为1。
3. 提高了梯度下降等优化算法的收敛速度和稳定性。
4. 使得不同量纲或范围的特征能够在同一尺度上进行比较和加权。

### Example
假设我们有一个简单的数据集，包含两个特征，我们想要对这个数据集进行Z-score标准化。

```python
import numpy as np

# 示例数据集
data = np.array([
    [1, 2],
    [3, 4],
    [5, 6],
    [7, 8]
])

# 计算每个特征的均值和标准差
mean = np.mean(data, axis=0)
std = np.std(data, axis=0)

# Z-score标准化
normalized_data = (data - mean) / std

print("原始数据:")
print(data)
print("标准化后的数据:")
print(normalized_data)
```

 **Output:**
```
原始数据:
[[1 2]
 [3 4]
 [5 6]
 [7 8]]
标准化后的数据:
[[-1.34164079 -1.34164079]
 [-0.4472136  -0.4472136 ]
 [ 0.4472136   0.4472136 ]
 [ 1.34164079  1.34164079]]
```

>[!note] 
>- 在进行Z-score标准化时，我们假设数据是服从正态分布的。如果数据不是正态分布，那么这种方法可能不是最佳选择。
>- 标准化后的数据可能会包含负数，这在实际应用中可能需要注意。
>- 在使用标准化后的数据进行训练后，对新数据进行预测时，也需要使用相同的均值和标准差进行标准化，以保证数据的一致性。


### 使用`sklearn`进行特征标准化：
在实际应用中，我们通常会使用`sklearn`库中的`StandardScaler`类来进行特征标准化。

```python
from sklearn.preprocessing import StandardScaler

# 示例数据集
data = np.array([
    [1, 2],
    [3, 4],
    [5, 6],
    [7, 8]
])

# 实例化StandardScaler
scaler = StandardScaler()

# 拟合和转换数据
scaled_data = scaler.fit_transform(data)

print("标准化后的数据:")
print(scaled_data)

# 保存均值和标准差
mean_values = scaler.mean_
std_values = scaler.scale_

# 对新数据进行标准化
new_data = np.array([[9, 10]])
new_scaled_data = scaler.transform(new_data)
print("新数据的标准化:")
print(new_scaled_data)
```

这种方法更加便捷，特别是当处理大型数据集或需要频繁进行标准化时。