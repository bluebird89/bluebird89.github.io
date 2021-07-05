# Machine learning

* 研究计算机怎样模拟或实现人类的学习行为，以获取新的知识或技能，重新组织已有的知识结构使之不断改善自身的性能
* 人工智能的核心，是使计算机具有智能的根本途径，其应用遍及人工智能的各个领域，它主要使用归纳、综合而不是演译
* 在过去的十年中，机器学习帮助我们自动驾驶汽车，有效的语音识别，有效的网络搜索，并极大地提高了人类基因组的认识
* 机器学习是当今非常普遍，可能会使用这一天几十倍而不自知。很多研究者也认为这是最好的人工智能的取得方式

* 利用事物本身具有的数据特征用数学来表达并构建模型，然后完成既定任务，总的来说模型就是特征到任务结果的某种数学规律
* 主要关乎算法与数据，尤其是数据;:可以没有复杂的算法，但不能没有好的数据。
* 除非你有许多数据，否则你应该坚持使用简单的模型:基于数据识别模式，构建由参数定义的模型。如果你的参数定义过多，你很容易过度拟合。详细的解释需要更多数学知识，但是机器学习的原则是：尽可能使模型简单。
* 机器学习的性能受到输入数据质量限制:"无用输入，无用输出"巧妙地点明了机器学习的关键，机器学习只能发现输入数据中的模式。对于有监督的机器学习任务，例如分类，输入数据必须标记正确，特征明显。
* 机器学习需要具有代表性的数据:过去的表现不对未来结果作保证。机器学习则只能对与训练数据分布相同的样本外有良好效果。因此，应对训练数据和样本外数据的偏离表示警觉，经常性地重新训练你的模型以免失效。
* 机器学习中大部分的困难工作为数据转换:用于数据清洗和特征工程（将原始特征转化为更有代表性的特征）上。
* 深度学习将一些传统需要特征工程的工作自动化进行，特别是在图像和视频领域。但是深度学习并不是一种新技术，仍然需要在数据清理和转化方面付出巨大的努力。
* 机器学习系统极易受操作者误差影响:机器学习算法不会杀死人，只有人会杀死人。当机器学习算法系统奔溃时，一般很少是由于机器学习算法错误。而是因为大多数时候，你在训练数据中引进了人为误差，或者一些系统误差。所以，永远保持质疑。
* 机器学习可以漫不尽心地创造自我实现的预言:你今天做的决定将影响明天收集的训练数据。一旦机器学习系统中嵌入偏差，它就会生成更多新的数据强化这些偏差，有一些偏差会毁掉人的生活。负责任一点：不要创造可自我实现的预言。
* AI不会拥有自我意识，不用担心崛起并毁灭人类

## 理论

* 学习它们的模型函数、目标函数，从模型函数到目标函数的运算过程，各个函数相应的物理意义，最优化的方法
* 再与特征工程结合
* 完成任务
  - 处理输入
    + 需要获得已有的数据
    + 需要对数据做矢量化操作，把原本丰富多样的数据变成有若干列的矢量
    + 需要对数据做特征工程，找出可能蕴涵了知识、值得被学习的那些特征项
  - 获得模型
    + 实际上很多时候你可以使用现成的模型，包括：（i）下载现成的离线模型，或者（ii）使用在线的人工智能服务
    + 如果没有现成的模型，你也可以考虑使用现有的数据来自行训练模型
  - 提供产出
    + 机器学习的结果可能通过某种人-机（UI）或机-机界面（API）被用户直接使用
    + 作为项目的产出，机器学习模型需要被嵌入到整个数据流水线中
    + 作为项目的产出，机器学习模型的开发、测试、部署需要有DevOps的支撑

## 问题

* 业务上要解决什么问题
* 该问题涉及到的信息管道有哪些
* 如何采集数据，数据源在哪
* 数据是完整的吗，数据刻度最小是多少
* 数据是定期发布的还是实时获取的
* 确定影响模型的有价值因素
* 工作量

## 监督学习

* 最终目标:使模型可以更准确地对我们所需要的响应变量建模
  - 需要提供一组学习样本，包括相关的特征数据以及相应的标签
  - 程序可以通过这组样本来学习相关的规律或是模式，然后通过得到的规律或模式来判断没有被打过标签的数据是什么样的数据
* 对于同一个模型而言，可以用不同的算法来求解模型的参数。这是机器学习的一个核心特点
* 模型
  - 线性模型 Linear Regression
    + 线性回归对现实场景是如何抽象的。顾名思义，线性回归认为现实场景中的响应变量（比如房价、比如票房）和数据特征之间存在线性关系。而线性回归的数学假设有两个部分
      * 响应变量的预测值是数据特征的线性变换。这里的参数是一组系数。而预测值是系数和数据特征的线性组合。
      * 响应变量的预测值和真实值之间有一个误差。这个误差服从一个正态（高斯）分布，分布的期望值是 0，方差是σ的平方。
    + 线性回归模型的参数是如何求解的
      * 线性回归的解析解虽然简单优美，但是在现实计算中一般不直接采用，因为需要对矩阵进行逆运算，而矩阵求逆运算量很大。解析解主要用于各种理论分析中
      * 数值计算的办法，比如梯度下降（Gradient Descent）的方法求得近似结果。然而梯度下降需要对所有的数据点进行扫描。当数据量很多的时候，梯度下降会变得很慢
      * 随机梯度下降（Stochastic Gradient Descent）算法就应运而生。随机梯度下降并不需要对所有的数据点扫描后才对参数进行更新，而可以对一部分数据，有时甚至是一个数据点进行更新。
    + 如何评估线性回归模型。由于线性回归是对问题的响应变量进行一个实数预测。那么，最简单的评估方式就是看这个预测值和真实值之间的绝对误差。如果对于每一个数据点都可以计算这么一个误差，那么对于所有的数据点而言，就可以计算一个平均误差。
  - 决策树模型
    + 决策树（Decision Tree）:根据属性构造一个树形的决策策略，按各个属性值不断往下便能确定最终的结果。训练时可以以信息增益作为准则。比如自动化放贷、风控。
  - 神经网络模型
    + 神经网络（感知机、BP神经网络、卷积神经网络、循环神经网络），神经网络基础版本是感知机和BP神经网络，通过模拟人脑神经一样构建起一个神经网络，并通过梯度下降之类的学习模型参数。后面通过加深网络层数和引入卷积等操作发展成卷积神经网络，此外还有改造成循环神经网络等，也就是后来的深度学习。
* 问题
  - 分类问题的核心是如何利用模型来判别一个数据点的类别
  - 回归问题的核心则是利用模型来输出一个预测的数值
    + 线性回归，比较简单且直观的回归算法，线性回归可以有n个属性值，然后每个属性的线性组合组成一个预测函数，通过定义误差函数然后最小化样本整体的误差来确定预测函数的参数。
    + 逻辑斯蒂回归，可以说它是广义线性模型，原来的线性回归无法用于分类任务，那么通过一个sigmoid函数可以将其用于分类任务，这便是逻辑斯蒂回归。线性函数被映射到了S函数中，以0.5为分割点可作为二分类。逻辑斯蒂回归往多分类推广则变为softmax回归，可用于多分类任务。
    + 逻辑回归（Logisitic Regression）。一种强大的统计学方法，可以用一个或多个变量来表示一个二项式结果。它可以用于信用评分、计算营销活动的成功率、预测某个产品的收入等。

* 朴素贝叶斯分类（Naive Bayesian classification）:概率论中非常经典的方法，核心就是贝叶斯定理，通过条件独立假设来简化模型，通过样本来学习联合概率分布，其中涉及到先验概率分布和条件概率分布。可以用于判断垃圾邮件，对新闻的类别进行分类，比如科技、政治、运动，判断文本表达的感情是积极的还是消极的，以及人脸识别等
* 最小二乘法（Ordinary Least Squares Regression）。算是一种线性回归。
* 支持向量机（Support Vector Machine，SVM）:规定了最优分类线不仅能正确将两类分开，而且还要使分类间隔最大，当然对于高维空间则是超平面。它的本质问题是凸二次规划问题的极小问题，这方面涉及到凸优化理论。对于线性不可分的情况可以引入核函数，将低维空间线性不可分的点映射到高维空间中，从而使得它们可分。可以用于基于图像的性别检测，图像分类等。
* 集成方法（Ensemble methods）。通过构建一组分类器，然后根据它们的预测结果进行加权投票来对新的数据点进行分类。原始的集成方法是贝叶斯平均，但是最近的算法包括纠错输出编码、Bagging 和 Boosting

* 方法
  - 模型:究竟和现实问题的联系是什么
    + 正则化
    + 交叉验证
    + 生成方法
      * 朴素贝叶斯
      * 隐马尔可夫
    + 判别方法
      * k近邻法
      * 感知机
      * 决策树
      * 逻辑斯蒂回归模型
      * 最大熵模型
      * 支持向量机
      * 提升方法
      * 条件随机场
  - 策略|算法求解:取决于模型本身的复杂度和成熟度
  - 评估则在现实生产中至关重要
* 泛化能力：根据上界定义
* 标注分类
  - 分类器
    + 精确率
    + 召回率
* 回归
  - 单变量回归
  - 多变量线性回归

* 集成学习（boosting、bagging、stacking），集成学习核心思想是结合多个模型算法来完成任务，这个假设了单个算法学习的知识是局限的，多个算法组合则能发挥各个算法模型的长处，从而增加模型性能。boosting、bagging、stacking分别是三种不同的集成方式，boosting的个体学习器有强依赖关系，每个个体学习器依赖于前一个个体学习器的输出，bagging个体学习器之间没有依赖关系且通过一定的结合策略产生最终输出，stacking则是一种分层特征学习的结构。
* 聚类（kmeans、密度聚类、层次聚类），聚类就是通过一定的算法将属性相近的个体聚集到一起，并将属性不同的个体尽量隔离远一点。kmeans是基于距离的聚类，密度聚类则是寻找被低密度区域分离的高密度区域，层次聚类congratulation上往下将大集群进行分割。
* 降维（PCA、LDA），PCA主成分分析将数据congratulation原来的坐标转换到新坐标使得可以用更少维度来表示数据，LDA线性判别分析将高维样本投印到最佳鉴别矢量空间以达到压缩特征空间维度的效果。

## 无监督学习

* 核心是希望发现数据内部的潜在结构和规律，为进行下一步决断提供参考
* 无监督学习，特别是深度学习支持下的无监督学习，是目前机器学习乃至深度学习的前沿研究方向
* 不同的无监督学习方法对数据内部的结构有不同的假设。因此，无监督学习不同模型之间常常有很大的差别。在众多无监督学习模型中，聚类模型无疑是重要的代表
* K 均值算法（K-means）
  - K 均值算法认为数据由 K 个类别组成。每个类别内部的数据相距比较近，而距离所有其他类别中的数据都比较遥远。这里面的数学假设，需要定义数据到一个类别的距离以及距离函数本身。在 K 均值算法中，数据到一个类别的距离被定义为到这个类别的平均点的距离。这也是 K 均值名字的由来。而距离函数则采用了欧几里得距离，来衡量两个数据点之间的远近。
  - 直接求解 K 均值的目标函数是一个 NP 难（NP-hard）的问题。于是大多数现有的方法都是用迭代的贪心算法来求解。
* 对聚类问题、对无监督学习任务的评估都是机器学习的一个难点。无监督学习没有一个真正的目标，或者是我们之前提到的响应变量，因此无法真正客观地衡量模型或者算法的好坏。
  - 对于 K 均值算法而言，比较简单的衡量指标就是，看所有类别内部的数据点的平均距离和类别两两之间的所有点的平均距离的大小。如果聚类成功，则类别内部的数据点会相距较近，而类别两两之间的所有点的平均距离则比较远。

## 数据

* 待收集的数据可能是表格数据、一串实时数据，N维矩阵或其他类型数据，同时也可能是多种存储介质，通过ETL处理将混合的数据源转成我们需要的格式，生成结构化数据类型。
* 对于收集的数据，可能存在缺陷，比如空值、异常值或数据产生器本身引起的偏差。这些缺陷可能导致模型效果不佳，同时为了优化更快收敛，需要做数据标准化处理，所以需要进行数据预处理。
  - 比如缺失值可以简单设为0、列平均值、中值、最高频率值、甚至是稳健算法和knn等等。
  - 比如标准化数据集，使数据集正态分布，平均值为0标准差为1。而且还达到了特征缩放效果

## 模型定义

机器学习主要就是模型问题，通过机器学习来对现实进行抽象建模，以解决现实问题。所以机器学习主要工作就是使用哪种模型来建模，尽管各种大大小小模型一大堆，但大体上也有些套路

* 回归问题：预测结果
* 分类问题：对数据进行分类
  * 监督学习：需要数据标记
  * 否则是非监督学习，使用聚类技术。
* 数据是否为连续的，是的话考虑序列模型，比如自回归和RNN之类的。
* 尽量使用简单模型，如果能用比如用单变量或多变量的线性回归或逻辑回归。
* 简单模型解决不了的情况，可通过多层神经网络解决，比如复杂的非线性。
* 使用了多少个维度的变量，将作用大的特征提取出来，并把不重要的特征去掉，比如用PCA降维。
* 不是监督也不是非监督？考虑强化学习

## 特征

* 把“【模型在训练集上的表现】与【期望值】之间的差距”叫做Bias
* 模型在训练集上的表】与【模型在测试集上的表现】之间的差距”叫做Variance
* High Bias：模型在训练集上的表现远低于期望，模型还不能实用（此时Variance如何并不重要）
  - 拟合不足”（Under-fitting）
  - 使用更复杂的机器学习算法
  - 使用更复杂的神经网络架构
* Low Bias, High Variance：模型在训练集上表现好，但是在测试集上表现差，模型还不能实用
  - 过度拟合”（Over-fitting）
  - 引入Regularization通常能降低over-fitting的程度
  - 通过特征工程可以避免一些over-fitting的情况，例如排除掉一些严重过度拟合的特征
  - 引入更多的训练数据，包括数据量和特征量
* Low Bias, Low Variance：模型在训练集和测试集上表现都好，可以投入实用

## 模型训练

* 迭代，表示模型计算和调整的一次过程
* 批，数据集每次以一批为单位输入到模型中
* epoch，每当整个数据集被处理完称为一个epoch

## 数据分割

一般将整个数据集分成三组，比例是7:2:1

* 训练集(training set）:用于调整模型参数
* 验证集(validation set）:用于比较多个模型直接的表现
* 测试集(test set）:用于测试训练得到的模型准确性

## 模型效果

模型训练完后要看效果如何，要看看泛化的能力。

* 对于回归问题，可以通过下面几个指标来了解拟合效果。
  - 平均绝对误差
  - 中值绝对误差
  - 均方误差等等
* 对于分类问题，可以通过下面几个指标来了解分类效果。
  - 准确性
  - 精确率
  - 召回率
  - F值
  - 混淆矩阵
* 对于聚类问题，可以通过下面几个指标来了解聚类效果。
  - 轮廓系数
  - 同质性
  - 完整性
  - V度量

## [SMO](https://mp.weixin.qq.com/s/oNKBpZpqX-Y6opBQ2e9oqQ)

## 机器学习数学基础

* 机器学习的数学基础
  - 函数与数据的泛化
  - 推理与归纳 (Deduction and Induction)
* 线性代数（Linear Algebra）
  - 向量与矩阵 (Vector and Matrix)
  - 特征值与特征向量
  - 向量与高维空间
  - 特征向量（Feature Vector）
* 概率与统计（Probability and Statistics）
  - 条件概率与经典问题 (Conditional Probability)
  - 边缘概率 (Marginal Probability)
* 作业/实践： 财宝问题的概率计算程序
  * 统计推理（Statistical Inference）
    - 贝叶斯原理与推理 (Bayesian Theorem)
    - 极大似然估计 (Maximum Likelihood)
    - 主观概率（Subjective Probability）
    - 最大后延概率（MAP)
  * 随机变量（Random Variable）
    - 独立与相关 (Independence)
    - 均值与方差 （Mean and Variance）
    - 协方差 (Co-Variance)
  * 概率分布（Probability Distributions)
  * 中心极限定理（Central Limit Theorem)
  * 作业/实践： 概率分布采样与不同随机变量之间协方差计算
  * 梯度下降（Gradient Descent）
    - 导数与梯度（Derivative and Gradient）
    - 随机梯度下降（SGD）
    - 牛顿方法（Newton's Method)
  * 凸函数（Convex Function）
    - Jensen不等式（Jensen's Inequality）
    - 拉格朗日乘子（Lagrange Multiplier）
  * 作业/实践： 利用牛顿方法求解给定的方程

## 机器学习的哲学（Philosophy of ML）

* 算法的科学（Science of Algorithms）
  - 输入与输出的神话（Mystery of I/O）
  - 奥卡姆剃刀（Occam’s Razor）
* 维数的诅咒（Curse of Dimensionality）
  - 高维的几何特性 (Geometric Properity )
  - 高维空间流形（High-dimensional Manifold）
* 机器学习与人工智能（Machine learning and AI）
* 机器学习的范式（Paradigms of ML）

## 经典机器学习模型（Classical ML Models）

* 样本学习（Case-Based Reasoning）
  - K-近邻（K-Nearest Neighbors）
  - K-近邻预测（KNN for Prediction）
  - 距离与测度（Distance and Metric）
* 朴素贝叶斯（Naïve Bayes Classifier)
  - 条件独立（Conditional Independence）
  - 分类（Naive Bayes for Classification)
* 作业/实践：垃圾邮件分类的案例
* 决策树（Decision Tree Learning）
      - 信息论与概率
      - 信息熵（Information Entropy）
      - ID3
* 预测树（CART）
      *Gini指标（Gini Index）
      * 决策树与规则（DT and Rule Learning）
* 作业/实践：决策树分类实验
* 集成学习（Ensemble learning）
  - Bagging and Boosting
  - AdaBoost
  - 误差分解（Bias-Variance Decomposition）
  - 随机森林（Boosting and Random Forest）

- 模型评估（Model Evaluation）
  - 交叉验证（Cross-Validation）
  - ROC (Receiver Operating Characteristics)
  - Cost-Sensitive Learning

* 作业/实践：随机森林与决策树分类实验的比较

## 线性模型（Linear Models）

* 线性模型（Linear Models）
  - 线性拟合（Linear Regression）
* 最小二乘法（LMS）
  - 线性分类器（Linear Classifier）
* 感知器（Perceptron）
* 对数几率回归（Logistic Regression）
* 线性模型的概率解释 (Probabilistic Interpretation)
* 作业/实践：对数几率回归的文本情感分析中应用
* 线性判别分析 (Linear Discrimination Analysis)
* 约束线性模型 (Linear Model with Regularization)
      - LASSO
      - Ridge Regression
* 稀疏表示与字典学习
      - Sparse Representation & Coding
      - Dictionary Learning

## 核方法（Kernel Methods）

* 支持向量机SVM（Support Vector Machines）
  - VC-维（VC-Dimension）
  - 最大间距（Maximum Margin）
  - 支撑向量（Support Vectors）
* 作业/实践：SVM不同核函数在实际分类中比较
* 对偶拉格朗日乘子
* KKT条件（KKT Conditions）
* Support Vector Regression (SVR)
* 核方法（Kernel Methods）

## 统计学习（Statistical Learning）

* 判别模型与生成模型
  - 隐含变量（Latent Variable）
* 混合模型（Mixture Model）
  - 三枚硬币问题（3-Coin Problem）
  - 高斯混合模型（Gaussian Mixture Model）
* EM算法（Expectation Maximization）
  - 期望最大（Expectation Maximization）
  - 混合模型的EM算法（EM for Mixture Models）
  - Jensen 不等式 (Jensen's Inequality)
  - EM算法推导与性能 (EM Algorithm)
* 隐马可夫模型（Hidden Markov Models）
  - 动态混合模型（Dynamic Mixture Model）
  - 维特比算法（Viterbi Algorithm）
  - 算法推导 (Algorithm)
* 条件随机场（Conditional Random Field）
  * 层次图模型（Hierarchical Bayesian Model）
    - 概率图模型 (Graphical Model)
    - 从隐含语义模型到p-LSA (From LSA to P-LSA)
    - Dirichlet 分布与特点（Dirichlet Distribution）
    - 对偶分布（Conjugate Distribution）
  * 主题模型（Topic Model – LDA）
    - Latent Dirichlet Allocation
    - 文本分类（LDA for Text Classification）
* 中文主题模型（Topic Modeling for Chinese）
* 其他主题模型（Other Topic Variables）

## 无监督学习（Unsupervised Learning）

* 数据是没有被标注过的，所以相关的机器学习算法需要找到这些数据中的共性
* 让大量未标识的数据能够更有价值，找到人类很难发现的数据里的规律或模型
* K-均值算法（K-Means）
  - 核密度估计（Kernel Density Estimation）
  - 层次聚类（Hierarchical Clustering）
* 蒙特卡洛(Monte Carlo)
  - 蒙特卡洛树搜索（Monte Carol Tree Search）
  - MCMC（Markov Chain Monte Carlo）
  - Gibbs Sampling
* 聚类算法（Clustering Algorithms）。聚类算法有很多，目标是给数据分类
* 主成分分析（Principal Component Analysis，PCA）。PCA 的一些应用包括压缩、简化数据，便于学习和可视化等
* 奇异值分解（Singular Value Decomposition，SVD）。实际上，PCA 是 SVD 的一个简单应用。在计算机视觉中，第一个人脸识别算法使用 PCA 和 SVD 来将面部表示为“特征面”的线性组合，进行降维，然后通过简单的方法将面部匹配到身份。虽然现代方法更复杂，但很多方面仍然依赖于类似的技术
* 独立成分分析（Independent Component Analysis，ICA）。ICA 是一种统计技术，主要用于揭示随机变量、测量值或信号集中的隐藏因素

## 流形学习（Manifold Learning）

* 主成分分析（PCA）
  - PCA and ICA
* 低维嵌入（Low-Dimensional Embedding）
  - 等度量映射（Isomap）
  - 局部线性嵌入（Locally Linear Embedding）

## 概念学习（Concept Learning）

* 概念学习（Concept Learning）
  - 经典概念学习
  - One-Short概念学习
* 高斯过程学习（Gaussian Process for ML）
  - Dirichlet Process

## 强化学习（Reinforcement Learning）

* 奖赏与惩罚（Reward and Penalty）
  - 状态空间 (State-Space Model)
  - Q-学习算法 (Q-Learning)
    * 路径规划 （Path Planning）
    * 游戏人工智能 （Game AI）
    * 作业/实践：小鸟飞行游戏的自动学习算法

## 神经网络

* 多层神经网络
  - 非线性映射（Nonlinear Mapping）
  - 反向传播（Back-propagation）
* 自动编码器（Auto-Encoder）

## 面试

* 在介绍自己实习时候用过XGBoost预测股票涨跌的过程中，就会由浅入深依次考察下列问题：
  - GBDT 原理（知识）
  - 决策树节点分裂时是如何选择特征的？（知识）
  - 写出Gini Index和Information Gain的公式并举例说明（知识）
  - 分类树和回归树的区别是什么？（知识）
  - 与Random Forest作比较，并以此介绍什么是模型的Bias和Variance（知识）
  - XGBoost的参数调优有哪些经验（工具）
  - XGBoost的正则化是如何实现的（工具）
  - XGBoost的并行化部分是如何实现的（工具）
  - 为什么预测股票涨跌一般都会出现严重的过拟合现象（业务）
  - 如果选用一种其他的模型替代XGBoost或者改进XGBoost你会怎么做，为什么？（业务+逻辑+知识）

## 实战

* [Kaggle](https://www.kaggle.com/)
  - [kaggle](https://github.com/apachecn/kaggle):Kaggle 项目实战（教程） = 文档 + 代码 + 视频
  - [Kaggle 路线](https://github.com/apachecn/kaggle)
  - [如何赢得数据科学竞赛：向顶尖 Kaggler 学习（How to Win a Data Science Competition: Learn from Top Kagglers）](https://www.coursera.org/learn/competitive-data-science)
* [image-net](http://www.image-net.org/)
* [天池大数据](https://tianchi.aliyun.com/home/)
* [datacastle](http://www.pkbigdata.com/)
* [datafountain](https://www.datafountain.cn/)
* [biendata](https://biendata.com/)
* [kesci](https://www.kesci.com/)
* [Jdata](https://jdata.jd.com/)

## 教程

* [ml-beginners](https://github.com/microsoft/ML-For-Beginners) 12 weeks, 24 lessons, classic Machine Learning for all <https://aka.ms/ml-beginners>
* [machine-learning-specialization](https://github.com/learnml/machine-learning-specialization)
* [EasyML](https://github.com/ICT-BDA/EasyML):Easy Machine Learning is a general-purpose dataflow-based system for easing the process of applying machine learning algorithms to real world tasks.
* [kubeflow](https://github.com/kubeflow/kubeflow):Machine Learning Toolkit for Kubernetes
* [100-Days-Of-ML-Code](https://github.com/Avik-Jain/100-Days-Of-ML-Code):100 Days of ML Coding
* [Learn_Machine_Learning_in_3_Months](https://github.com/llSourcell/Learn_Machine_Learning_in_3_Months):This is the code for "Learn Machine Learning in 3 Months" by Siraj Raval on Youtube
* [机器学习（Machine Learning）吴恩达（Andrew Ng）](https://www.bilibili.com/video/av9912938)
  - [吴恩达机器学习](https://study.163.com/course/courseMain.htm?courseId=1004570029)
  - [吴恩达《Machine Learning》](https://www.coursera.org/learn/machine-learning)
      * [machine-learning-yearning-cn](https://github.com/deeplearning-ai/machine-learning-yearning-cn):Machine Learning Yearning 中文版 - 《机器学习训练秘籍》 - Andrew Ng 著 <https://deeplearning-ai.github.io/machine-learning-yearning-cn/>
      * [中文笔记及作业代码](https://github.com/fengdu78/Coursera-ML-AndrewNg-Notes)
      * [ml-coursera-python-assignments](https://github.com/dibgerge/ml-coursera-python-assignments):Python assignments for the machine learning class by andrew ng on coursera with complete submission for grading capability and re-written instructions.
  - [吴恩达 CS229](http://cs229.stanford.edu/)
    + [斯坦福大学机器学习课程](http://open.163.com/special/opencourse/machinelearning.html)
    + [中文笔记](https://kivy-cn.github.io/Stanford-CS-229-CN/#/)
    + [速查表](https://zhuanlan.zhihu.com/p/56534902)
    + [作业代码](https://github.com/Sierkinhane/CS229-ML-Implements)
    + [stanford-cs-229-machine-learning](https://github.com/afshinea/stanford-cs-229-machine-learning):VIP cheatsheets for Stanford's CS 229 Machine Learning <https://stanford.edu/~shervine/teaching/cs-229>
  - [斯坦福大学2014（吴恩达）机器学习教程中文笔记](https://www.coursera.org/course/ml)
  - [Andrew Ng 老师的机器学习课程](http://coursegraph.com/coursera-machine-learning) <http://coursegraph.com/coursera_ml>
* [李宏毅 Machine Learning](https://www.bilibili.com/video/av15889450)
  - [机器学习-李宏毅(2019) Machine Learning](https://www.bilibili.com/video/av35932863)
    + [李宏毅《机器学习》大纲](https://datawhalechina.github.io/Leeml-Book/#/)
    + [site](http://speech.ee.ntu.edu.tw/~tlkagk/courses_ML17.html)
  - 资料：<http://speech.ee.ntu.edu.tw/~tlkagk/courses_ML19.html>
  - 课程视频：<https://www.bilibili.com/video/av46561029/>
  - <https://www.youtube.com/playlist?list=PLJV_el3uVTsOK_ZK5L0Iv_EQoL1JefRL4>
  - [李宏毅机器学习(2017)](https://www.bilibili.com/video/av10590361/)
  - <https://blog.csdn.net/soulmeetliang/article/details/77461607>
  - [ML-Foundation-and-ML-Techniques](https://github.com/Doraemonzzz/ML-Foundation-and-ML-Techniques):台大机器学习课程作业详解
* 林轩田《机器学习基石》
  - [中文视频](https://www.bilibili.com/video/av36731342)
  - [中文笔记](https://redstonewill.com/category/ai-notes/lin-ml-foundations/)
  - [配套教材《Learning From Data》](http://amlbook.com/)
* 林轩田《机器学习技法》
  - [中文视频](https://www.bilibili.com/video/av36760800)
  - [中文笔记](https://redstonewill.com/category/ai-notes/lin-ml-techniques/)
* [机器学习中的数学基础](https://www.bilibili.com/video/av15673238/)
* [Machine Learning 10-701/15-781, Spring 2011](http://www.cs.cmu.edu/~tom/10701_sp11/lectures.shtml)
* [Your-first-machine-learning-Project---End-to-End-in-Python](https://github.com/DeqianBai/Your-first-machine-learning-Project---End-to-End-in-Python):一个完整的，端到端的机器学习项目，非常适合有一定基础后拿来练习，以提高对完整机器学习项目的认识
* [Learning-from-data](https://github.com/Doraemonzzz/Learning-from-data):记录Learning from data一书中的习题解答 <http://amlbook.com/>
* [徐亦达](https://github.com/roboticcam/machine-learning-notes)
  - YouTube： <https://www.youtube.com/channel/UConITmGn5PFr0hxTI2tWD4Q>
  - 哔哩哔哩： <https://space.bilibili.com/327617676>
  - 优酷： <http://i.youku.com/i/UMzIzNDgxNTg5Ng>
* [Built on the AWS Cloud. Developed for Amazon developers and engineers.](https://aws.amazon.com/training/learning-paths/machine-learning/)
* [machine_learning_beginner](https://github.com/fengdu78/machine_learning_beginner)
* [A Course in Machine Learning](http://ciml.info/)
* [Machine-Learning-Study-Path-March-2019](https://github.com/clone95/Machine-Learning-Study-Path-March-2019)
* [mlcourse.ai](https://github.com/Yorko/mlcourse.ai):Open Machine Learning Course <https://mlcourse.ai>
* [golearn](https://github.com/sjwhitworth/golearn):Machine Learning for Go
* [Mathematics for Machine Learning Specialization（面向机器学习的数学专项课程系列）](http://coursegraph.com/coursera-specializations-mathematics-machine-learning):For a lot of higher level courses in Machine Learning and Data Science, you find you need to freshen up on the basics in maths – stuff you may have studied before in school or university, but which was taught in another context, or not very intuitively, such that you struggle to relate it to how it’s used in Computer Science. This specialisation aims to bridge that gap, getting you up to speed in the underlying maths, building an intuitive understanding, and relating it to Machine Learning and Data Science. In the first course on Linear Algebra we look at what linear algebra is and how it relates to data. Then we look through what vectors and matrices are and how to work with them. The second course, Multivariate Calculus, builds on this to look at how to optimise fitting functions to get good fits to data. It starts from introductory calculus and then uses the matrices and vectors from the first course to look at data fitting. The third course, Dimensionality Reduction with Principal Components Analysis, uses the maths from the first two courses to do simple optimisation for the situation where you don’t have an understanding of how the data variables relate to each other. At the end of this specialisation you will have gained the prerequisite mathematical knowledge to continue your journey and take more advanced courses in machine learning.
  - [Mathematics for Machine Learning: Linear Algebra（面向机器学习的数学：线性代数）](http://coursegraph.com/coursera-linear-algebra-machine-learning):vectors and matrices. Then we look through what vectors and matrices are and how to work with them, including the knotty problem of eigenvalues and eigenvectors, and how to use these to solve problems. Finally we look at how to use these to do fun things with datasets – like how to rotate images of faces and how to extract eigenvectors to look at how the Pagerank algorithm works. Since we’re aiming at data-driven applications, we’ll be implementing some of these ideas in code, not just on pencil and paper. Towards the end of the course, you’ll write code blocks and encounter Jupyter notebooks in Python, but don’t worry, these will be quite short, focussed on the concepts, and will guide you through if you’ve not coded before. At the end of this course you will have an intuitive understanding of vectors and matrices that will help you bridge the gap into linear algebra problems, and how to apply these concepts to machine learning.
  - [Mathematics for Machine Learning: Multivariate Calculus（面向机器学习的数学：多变量微积分）](http://coursegraph.com/coursera-multivariate-calculus-machine-learning):This course offers a brief introduction to the multivariate calculus required to build many common machine learning techniques. We start at the very beginning with a refresher on the “rise over run” formulation of a slope, before converting this to the formal definition of the gradient of a function. We then start to build up a set of tools for making calculus easier and faster. Next, we learn how to calculate vectors that point up hill on multidimensional surfaces and even put this into action using an interactive game. We take a look at how we can use calculus to build approximations to functions, as well as helping us to quantify how accurate we should expect those approximations to be. We also spend some time talking about where calculus comes up in the training of neural networks, before finally showing you how it is applied in linear regression models. This course is intended to offer an intuitive understanding of calculus, as well as the language necessary to look concepts up yourselves when you get stuck. Hopefully, without going into too much detail, you’ll still come away with the confidence to dive into some more focused machine learning courses in future.
  - [Mathematics for Machine Learning: PCA（面向机器学习的数学：主成分分析）](http://coursegraph.com/coursera-pca-machine-learning):This course introduces the mathematical foundations to derive Principal Component Analysis (PCA), a fundamental dimensionality reduction technique. We’ll cover some basic statistics of data sets, such as mean values and variances, we’ll compute distances and angles between vectors using inner products and derive orthogonal projections of data onto lower-dimensional subspaces. Using all these tools, we’ll then derive PCA as a method that minimizes the average squared reconstruction error between data points and their reconstruction. At the end of this course, you’ll be familiar with important mathematical concepts and you can implement PCA all by yourself. If you’re struggling, you’ll find a set of jupyter notebooks that will allow you to explore properties of the techniques and walk you through what you need to do to get on track. If you are already an expert, this course may refresh some of your knowledge.

## 图书

* 机器学习：算法视角（原书第2版）
* Spark机器学习（第2版）》 作者：[印]拉结帝普·杜瓦 , [印]曼普利特·辛格·古特拉 , [南非]尼克·彭特里思 译者：蔡立宇 , 黄章帅 , 周济民
* 百面机器学习
  - 知识：主要是指对machine learning相关知识和理论的储备
  - 工具：将machine learning知识应用于实际业务的工具
  - 逻辑：举一反三的能力，解决问题的条理性，你发散思维的能力，你的聪明程度
  - 业务：深入理解所在行业的商业模式，从业务中发现motivation并进而改进模型算法的能力
* [机器学习 西瓜书](https://github.com/datawhalechina/pumpkin-book)周志华,基本涵盖机器学习的所有分支，如监督学习，无监督学习，半监督学习，强化学习，特征选择等
  - [在线阅读](https://datawhalechina.github.io/pumpkin-book/)
  - [Machine-learning-learning-notes](https://github.com/Vay-keen/Machine-learning-learning-notes)
  + [读书笔记](https://www.cnblogs.com/limitlessun/p/8505647.html#_label0)
  + [公式推导](https://datawhalechina.github.io/pumpkin-book/#/)
  + [南瓜书](https://github.com/datawhalechina/pumpkin-book)
  + [课后习题](https://zhuanlan.zhihu.com/c_1013850291887845376)
* 《Pattern Recognition and Machine Learning》
* 《Reinforcement Learning: An Introduction》：强化学习入门
*  [Hands-on Machine Learning with Scikit-Learn and TensorFlow Scikit-Learn 与 TensorFlow 机器学习实用指南](https://www.oreilly.com/library/view/hands-on-machine-learning/9781491962282/ch01.html)
  - [源代码](https://github.com/ageron/handson-ml):A series of Jupyter notebooks that walk you through the fundamentals of Machine Learning and Deep Learning in python using Scikit-Learn and TensorFlow.
  - [翻译](https://github.com/apachecn/hands-on-ml-zh)
* [《面向机器学习的特征工程》](https://github.com/apachecn/feature-engineering-for-ml-zh)
* [Model-Based Machine Learning](http://mbmlbook.com/index.html)
* [Evolutionary Learning: Advances in Theories and Algorithms）](https://www.springer.com/cn/book/9789811359552)
* [machine-learning-systems-design](https://github.com/chiphuyen/machine-learning-systems-design):A booklet on machine learning systems design with exercises
* 《[数据之巅](https://www.amazon.cn/gp/product/B00JUE9DXW)》
* 《[矩阵分析](https://www.amazon.cn/gp/product/B00NTM5GK0)》
* 《[机器学习](https://www.amazon.cn/gp/product/B002WC7NH2)》
* 《[机器学习导论](https://www.amazon.cn/gp/product/B01AG3ZV9K)》
* 《[机器学习实战](https://www.amazon.cn/gp/product/B00D747PTK)》
* 《漫谈人工智能》 集智俱乐部
* [dive-into-machine-learning](https://github.com/hangtwenty/dive-into-machine-learning):Dive into Machine Learning with Python Jupyter notebook and scikit-learn! <http://hangtwenty.github.io/dive-into-machine-learning/>
* [机器学习基础 Foundations of Machine Learning](https://cs.nyu.edu/~mohri/mlbook/)
* [Mathematics for Machine Learning](https://mml-book.github.io/book/mml-book.pdf)

## 工具

* [guess](https://github.com/guess-js/guess):Libraries & tools for enabling Machine Learning driven user-experiences on the web
* [gorgonia](https://github.com/gorgonia/gorgonia):Gorgonia is a library that helps facilitate machine learning in Go.
* [ray](https://github.com/ray-project/ray):A system for parallel and distributed Python that unifies the ML ecosystem. <https://ray.readthedocs.io/en/latest/>
* [jax](https://github.com/google/jax):GPU- and TPU-backed NumPy with differentiation and JIT compilation.
* [UCI-ML-API](https://github.com/tirthajyoti/UCI-ML-API):UCI ML网站引入一个简单直观的API，用户可以轻松查找数据集描述，搜索他们感兴趣的特定数据集，甚至可以按大小或机器学习任务分类下载数据集。
* [guess](https://github.com/guess-js/guess):Libraries & tools for enabling Machine Learning driven user-experiences on the web <https://guess-js.github.io/>
* [streamlit](https://github.com/streamlit/streamlit):Streamlit — The fastest way to build custom ML tools <https://streamlit.io>
* [turicreate](https://github.com/apple/turicreate):Turi Create simplifies the development of custom machine learning models.
* [chineseocr_lite](https://github.com/ouyanghuiyu/chineseocr_lite):超轻量级中文ocr，支持竖排文字识别, 支持ncnn推理 , psenet(8.5M) + crnn(6.3M) + anglenet(1.5M) 总模型仅17M
* [turicreate](https://github.com/apple/turicreate):Turi Create simplifies the development of custom machine learning models.
* [onnxjs](https://github.com/Microsoft/onnxjs)：ONNX.js: run ONNX models using JavaScript
* [Kubeflow](https://www.kubeflow.org/):The Machine Learning Toolkit for Kubernetes
* [spleeter](https://github.com/deezer/spleeter):Deezer source separation library including pretrained models. <https://research.deezer.com/projects/spleeter.html>
* [Scikit-Learn 官方文档](https://scikit-learn.org/stable/index.html): <http://sklearn.apachecn.org/#/>

## 参考

* [Machine Learning From Scratch](https://github.com/eriklindernoren/ML-From-Scratch):Machine Learning From Scratch. Bare bones NumPy implementations of machine learning models and algorithms with a focus on accessibility. Aims to cover everything from linear regression to deep learning.
* [awesome-machine-learning](https://github.com/josephmisiti/awesome-machine-learning)A curated list of awesome Machine Learning frameworks, libraries and software.
  - [awesome-machine-learning-cn](https://github.com/jobbole/awesome-machine-learning-cn):机器学习资源大全中文版，包括机器学习领域的框架、库以及软件
* [machine-learning-for-software-engineers](https://github.com/ZuzooVn/machine-learning-for-software-engineers):A complete daily plan for studying to become a machine learning engineer.
* [aerosolve](https://github.com/airbnb/aerosolve):A machine learning package built for humans. <http://airbnb.github.io/aerosolve/>
* [MachineLearning](https://github.com/wepe/MachineLearning)Basic Machine Learning and Deep Learning
* [nyu-mlif-notes](https://github.com/wizardforcel/nyu-mlif-notes):📖 NYU 金融机器学习 中文笔记
* [mlflow](https://github.com/mlflow/mlflow):Open source platform for the machine learning lifecycle <https://mlflow.org>
* [Machine-Learning](https://github.com/zhaozhengcoder/Machine-Learning)：关于机器学习的内容
* [practicalAI](https://github.com/GokuMohandas/practicalAI):A practical approach to learning machine learning.
* [MachineLearning_Lab](https://github.com/sea-boat/MachineLearning_Lab):Code lab for machine learning. Including Least Square Method,Gradient Descent,Newton's Method,Hierarchy Cluster,KNN,Markov,Adaboost,Random Number Generation(all kinds of distributions),N Sigma outlier detection,outlier detection based on median,FFT outlier detection,DBSCAN,Kmeans,Naive Bayes,perceptron,reinforcement learning.
* [machine-learning-notes](https://github.com/roboticcam/machine-learning-notes):My continuously updated Machine Learning, Probabilistic Models and Deep Learning notes and demos (1000+ slides) 我不间断更新的机器学习，概率模型和深度学习的讲义(1000+页)和视频链接
* [构建可扩展的机器学习系统（一）：你所需的架构设计知识](https://towardsdatascience.com/being-a-data-scientist-does-not-make-you-a-software-engineer-c64081526372)
* [MIT Deep Learning](http://www.deeplearningbook.org/)：Bengio写的MIT Press《Deep learning》
* [machine-learning-yearning-cn](https://github.com/deeplearning-ai/machine-learning-yearning-cn):Machine Learning Yearning 中文版 - 《机器学习训练秘籍》 - Andrew Ng 著
* [ML-NOTE](https://github.com/yhangf/ML-NOTE):📙慢慢整理所学的机器学习算法，并根据自己所理解的样子叙述出来。(注重数学推导)
* [](https://github.com/apache/predictionio)
* [Bilibili-机器学习白板系列](https://www.yuque.com/bystander-wg876/yc5f72)
* [Support Vector Machine](https://mp.weixin.qq.com/s/SackOqskC88pB0582bDg8A)

* 火光摇曳：腾讯技术大牛们的博客 <http://www.flickering.cn/>
* 美团技术团队的博客：<https://tech.meituan.com/>
* 苏剑林的博客里面也全是干货 <https://spaces.ac.cn/>
* Netflix：Netflix技术博客，很多干货。 <https://medium.com/netflix-techblog>
* Towards Data Science：主要分享些概念、idea和代码。 <https://towardsdatascience.com/>
