# MachineLearningNotes
## 机器学习是什么

+ 机器学习致力于研究如何通过计算的手段，利用经验来改善自身的性能。在计算机系统中，“经验”通常以“数据“形式存在。因此，机器学习所研究的主要内容，是关于在计算机上从数据产生”模型“的算法，即”学习算法“。有了学习算法，我们把经验数据提供给它，它就能基于这些数据产生模型；在面对新的情况时，模型会给我们提供相应的判例。

## 机器学习的基本概念

+ 数据集
+ 属性（特征）/属性空间（样本空间）
+ 真相：数据潜在的自身规律
+ 假设：学得模型对应了关于数据的某种潜在的规律
+ 训练集：训练集通常只是样本空间的一个很小的采样（但仍希望它能很好地反映出样本空间的特性）
+ 测试集
+ 有监督学习
  -分类任务： 预测离散值
  -回归任务： 预测连续值
+ 无监督学习：
  -聚类任务 
+ 泛化（能力）：学得模型适用与新样本的能力，具有强泛化能力的模型能很好的适用于整个样本空间。

## 机器学习的基本过程

1. 学习到底是在做什么？

我们可以把学习过程看作一个在所有假设组成的空间中进行搜索的过程，搜索目标是找到与训练集”匹配“的假设。

2. 怎么去搜索假设？

可以有许多策略对这个假设空间进行搜索（学习的方法），最终获得与训练集一致的假设（学习的结果）

3. 搜索到的与训练集一致的假设会有多个吗？

现实中，通常面临很大的假设空间，学习过程是基于有限样本训练集进行的，因此，可能有多个假设与训练集一致，也就是存在一个”假设集合“

4. 如果存在”假设集合“怎么办，挑选哪个？

如果存在多个与训练集一致的假设，但它们对应的模型，当面临新样本时，会产生不同的输出，那么应该选哪个模型（假设）呢？
对于一个具体的学习算法而言，它必须要产生一个模型，这时，学习算法本身的”偏好“就会起到关键作用。例如，算法喜欢”尽可能特殊“还是”尽可能通用“
一般性的原则，来引导算法确立”正确的“偏好，*奥卡姆剃刀(Occam's razor)*是一种常用的的原则，即”若有多个假设与观察一致，则选最简单的那个“

5. 奥卡姆剃刀原则就一定是对的吗？它有没有什么问题？

有的时候，判断哪个更”简单“，这个事情并不简单，需要借助其他机制才能解决

6. 根据偏好挑出的算法，是否能在所有的实际问题中都表现比其他的好？

很遗憾，对于一个学习算法A，若它在某些问题上比学习算法B好，那么必然存在另一些问题，在那里B比A好。
甚至，当假设所有问题出现的机会相同、或所有问题同等重要的条件下，所有的学习算法的期望性能都跟随机猜测差不多。

7. 既然跟随机猜差不多，那还有必要进行机器学习吗？

实际上，生活中面临的问题，并不一定是均匀分布（即上述的假设），因此，脱离具体的问题，空谈”什么学习算法更好“毫无意义

## 机器学习的基本方法

#### 我们想要怎么样的学习器/学习算法？


+ 错误率： 通常是把分类错误的样本数占样本总数的比例
+ 误差： 学习器的预测输出 与 真实样本输出之间的差异
  - 训练误差： 学习器在训练集上的误差（经验误差）
  - 泛化误差： 学习器在新样本上的误差

我们希望得到**泛化误差**最小的学习器。

问题是，我们事先并不知道新样本是什么样，实际能做的是努力使训练误差最小。
  我们可以学得一个经验误差很小的学习器，但这并不是我们想要的，而且通常这样的学习器在多数情况下都不好，因为我们希望得到在新样本表现很好的学习器
  

+ 过拟合：通常学习器把训练样本学得”太好“了的时候，可能已经把训练样本自身的一些特点当作了潜在样本都具有的一般性质，也就是导致泛化能力的下降，这种现象称为过拟合
+ 欠拟合：学习得不够、学习能力低下的现象称为欠拟合


#### 现实生活中，多种学习器/学习算法，该如何选择？

理想的解决方案当然是对候选模型的*泛化误差*进行评估，然后选择误差最小的那个


但我们无法直接获取泛化误差，而训练误差又由于过拟合现象的存在，不适合作为标准，现实生活中该如何选择？

我们可通过实验测试来对学习器的泛化误差进行评估，进而作出选择，因此需要一个测试集


#### 当我们好不容易得到数据集的时候，如何划分训练集和测试集

+ 测试集需要尽可能得不在训练集中

1. 留出法

直接将数据集D划分为两个*互斥*的集合， 比如按70%比例划分为训练集S，30%比例划分为测试集T


**训练/测试集的划分要尽可能保持数据分布的一致性**（类比中小学的期末考试要尽可能与平时的训练一致）


即使这样，还是可以划分出多种不同的训练/测试集，一般要采用若干次随机划分、重复进行实验评估，取平均值


2. 交叉验证法

将数据集D划分为k个大小相似的互斥子集，每个子集尽可能保持数据分布的一致性，每次用k-1个子集作为训练集，余下的那个子集作为测试集

这样就可以获得k组训练/测试集，从而进行k次训练和测试，最终返回的是这k个测试结果的均值

为减少因样本划分不同而引入的误差，k折交叉验证通常要随机使用不同的划分重复p次，最终的评价结果是这p次k折交叉验证结果的均值


#### 如何衡量模型的泛化能力

+ 错误率
+ 精度


对于二分类问题，可将样例根据其真实类别与学习器预测类别的组合划分为真正例（TP）、假正例（FP）、真反例（TN）、假反例（FN）

+ 查准率（准确率）P： TP/(TP+FP)
+ 查全率（召回率）R： TP/(TP+FN)


查准率与查全率是一堆矛盾的量，现实的任务中，通常需要在两者之间找到一个平衡，需要综合考虑查准率、查全率。例如，画P-R曲线，当一个学习器的P-R曲线
被另一个学习器的曲线完全“包住”时，可断言后者的性能优于前者；但如果有交叉，则难以判断。

这时候，一般通过F1度量
+ F1度量：基于查准率和查全率的调和平均


1/F1 = (1/2)*(1/P + 1/R)

当然还有其他的度量

+ ROC
+ AUC
+ 代价敏感错误率与代价曲线


#### 有了性能度量以后，如何比较两个算法呢，直接比“大小”么？

我们希望的是比较泛化性能，然而通过实验评估方法我们获取的是测试集上的性能，两者的对比结果可能未必相同

即使相同大小的测试集，若包含的测试样例不同，测试结果也会有不同

很多机器学习算法本身有一定的随机性，即使相同的参数设置在同一个测试集上多次运行，结果也会不同

**统计假设检验**为我们进行学习器性能比较提供了重要依据，基于假设检验结果我们可推断出，若在测试集上观察学习器A比B好，则A的泛化性能是否在统计意义上优于B，以及这个结论的把握有多大。
