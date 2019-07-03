

一、名词解释（4*6=24分）
1.联想（Alssociation）
2分类（Classfication)*

机器学习模型的一种，将数据分离为两个或多个离散类别。例如，一个自然语言处理分类模型可以将一句话归类为法语、西班牙语或意大利语。分类模型与回归模型（regression model）成对比。

​	如果预测的是离散值，学习任务称为“分类”（classfication）*
3.回归（Regression）l

​	定量输出称为回归，或者说是连续变量预测；

​	定性输出称为分类，或者说是离散变量预测

4.聚类（Clustering）

​	*聚类*分析起源于分类学，但是*聚类*不等于分类。*聚类*与分类的不同在于，*聚类*所要求划分的类是未知的。

5.VG（vapnik-Cheronenkis）维

> VC维（外文名Vapnik-Chervonenkis Dimension）的概念是为了研究学习过程一致收敛的速度和推广性（Generalization performance），由统计学理论定义的有关函数集学习性能的一个重要指标。
>
> 简单来说，VC维是用来衡量研究对象（数据集与学习模型）**可学习性**的指标。

6.过拟合（Owerfiting）*

​	过拟合(overfitting)：一个在训练数据上表现良好，但对任何新数据的泛化能力却很差的模型。*
二、简答题（5*6=30分）
1.什么是强化学习？试举例说明其应用。

强化学习是一类算法, 是让计算机实现从一开始什么都不懂, 脑袋里没有一点想法, 通过不断地尝试, 从错误中学习, 最后找到规律, 学会了达到目的的方法. 这就是一个完整的强化学习过程. 实际中的强化学习例子有很多. 比如近期最有名的 Alpha go, 机器头一次在围棋场上战胜人类高手, 让计算机自己学着玩经典游戏 Atari, 这些都是让计算机在不断的尝试中更新自己的行为准则, 从而一步步学会如何下好围棋, 如何操控游戏得到高分. 

2.如何区别监督学习和无监督学习？并举例说明。

**有监督学习**是机器学习任务的一种。它从有标记的训练数据中推导出预测函数。有标记的训练数据是指每个训练实例都包括输入和期望的输出。一句话：**给定数据，预测标签**。

**无监督学习**是机器学习任务的一种。它从无标记的训练数据中推断结论。最典型的无监督学习就是聚类分析，它可以在探索性数据分析阶段用于发现隐藏的模式或者对数据进行分组。一句话：**给定数据，寻找隐藏的结构**。

**强化学习**是机器学习的另一个领域。它关注的是软件代理如何在一个环境中采取行动以便最大化某种累积的回报。一句话：**给定数据，学习如何选择一系列行动，以最大化长期收益**。

3.什么是MSE（Mean square crror）？其作用是什么？

均方误差　　**（Mean Squared Error）均方误差**

　　MSE是网络的性能函数,网络的均方误差，叫"Mean Square Error"。比如有n对输入输出数据，每对为[Pi,Ti],i=1,2,...,n.网络通过训练后有网络输出,记为Yi。 　　在相同测量条件下进行的测量称为等精度测量，例如在同样的条件下，用同一个游标卡尺测量铜棒的直径若干次，这就是等精度测量。对于等精度测量来说，还有一种更好的表示误差的方法，就是标准误差。 　　**标准误差定义为各测量值误差的平方和的平均值的平方根，故又称为均方误差**。

MSE是衡量“[平均误差](http://baike.baidu.com/view/3062550.htm)”的一种较方便的方法，MSE可以评价数据的变化程度，MSE的值越小，说明[预测模型](http://baike.baidu.com/view/1590251.htm)描述实验数据具有更好的精确度

4.Maximum Likelihood Estimation（MLF）、Maximum A Posteriori（VMAP）和Bayes estimation有何异同？
5.什么是Mahalanobis Distance？如果样本数据x-Na（u.），求Mahalanobis Distance的表达式。

马氏距离(Mahalanobis Distance)是度量学习中一种常用的距离指标，同欧氏距离、曼哈顿距离、汉明距离等一样被用作评定数据之间的相似度指标。但却可以应对高维线性分布的数据中各维度间非独立同分布的问题。

6.什么是维度规约，它有哪几种方法？



三、应用题（10~3=52分）
1.Given n independent and identically distributed samples of the data，X=（xl.……Xn}.
Assume the data generated via a probabilistic model x-Pa），where Pce）is the probability distribution underlying the data，and e is a set of fixed and unknown parameters.Estimate  that best describes the data by using（1）MLE and（2）MAP，respectively.(20分)

2.Assume we have a set of D-dimensional samples {xl，x，…，.xn}，N1 of which belong to the class or and N2 to the class o2.Project the set Xonto a line r=WTx where w is a vector with D-dimension and denotes direction of the line.Please infer Fisher's Linear Discriminant.（16分）

###### [Linear Discriminant Analysis 线性判别分析](https://blog.csdn.net/matrix_space/article/details/51375691)

3.For credit scoring classification problem，given observable samples x=[l，x2]，where xi and x2 respectively denote income and savings.To class the samples as low-risk and high-risk，we let class C={0，1}as Bernoulli random variables.Please use Bayesian Decision Theory to predict an applicant.（10分）

###### [贝叶斯决策理论](https://www.zhihu.com/question/27670909)

