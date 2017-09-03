## 何谓机器学习
### 机器学习的定义
>  A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P if its performance at tasks in T, as measured by P, improves with experience E.

> 如果一个计算机程序在某类任务T上的性能P通过经验E得到了提升，那么就说关于T和P，该程序学习了经验E。
>
> —— Tom Mitchell《Machine Learning》

> 机器学习是研究学习算法的学科。（学习算法时指通过数据来改进程序性能的算法）

> 从广义上来说，机器学习是一种能够赋予机器学习的能力以此让它完成直接编程无法完成的功能的方法。但从实践的意义上来说，机器学习是一种通过利用数据，训练出模型，然后使用模型预测的一种方法。

### 机器学习的范围
![](/assets/ml.png)

#### 模式识别（Pattern Recognition）
模式识别 = 机器学习
> 模式识别源自工业界，而机器学习来自于计算机学科。不过，它们中的活动可以被视为同一个领域的两个方面。
> ——《Pattern Recognition And Machine Learning》

#### 数据挖掘（Data mining）
数据挖掘 = 机器学习 + 数据库
> Data mining is the analysis step of the "knowledge discovery in databases.

#### 统计学习（statistical learning）
统计学习 = 同统计方法研究机器学习

> 统计学习是关于计算机基于数据构建概率统计模型并运用模型对数据进行预测与分析的一门学科。统计学习也称为统计机器学习（statistical machine learning）。
> ——《统计学习方法》

#### 计算机视觉（Computer vision）
计算机视觉 = 机器学习 + 图像处理
> Computer vision is an interdisciplinary field that deals with how computers can be made for gaining high-level understanding from digital images or videos.

#### 语音识别（Speech recognition）
语音识别 = 机器学习 + 语音处理
> Speech recognition is the inter-disciplinary sub-field of computational linguistics that develops methodologies and technologies that enables the recognition and translation of spoken language into text by computers.

#### 自然语言处理（Natural language processing）
自然语言处理 = 机器学习 + 文本处理
> Natural language processing (NLP) is a field of computer science, artificial intelligence and computational linguistics concerned with the interactions between computers and human (natural) languages, and, in particular, concerned with programming computers to fruitfully process large natural language corpora.

### 人工智能&机器学习&深度学习
> Artificial intelligence(AI,also machine intelligence, MI) is intelligence exhibited by machines, rather than humans or other animals(natural intelligence,NI).

> 狭义的人工智能是指让机器获取认知/学习的能力，机器可以不断地通过数据来改善自身的性能。广义的人工智能包括狭义人工智能、人工情感与人工意志三个方面。
> —— 西部世界

> 生命本身就是不断处理数据的过程，生物本身就是算法。
> —— 尤瓦尔•赫拉利《未来简史》

> 人也不过是一台有灵魂的机器而已。
> —— 丹尼尔·丹尼特《意识的解释》

![](/assets/1-1.jpeg)

### 机器学习的工作方式
![](/assets/1-2.jpeg)

①选择数据：将你的数据分成三组：训练数据、验证数据和测试数据
②模型数据：使用训练数据来构建使用相关特征的模型
③验证模型：使用你的验证数据来验证你的模型
④测试模型：使用你的测试数据检查被验证的模型的表现
⑤使用模型：使用完全训练好的模型在新数据上做预测
⑥调优模型：使用更多数据、不同的特征或调整过的参数来提升算法的性能表现

### 机器学习对传统编程的改进
![](/assets/1-4.png)

①传统编程：软件工程师编写程序来解决问题。首先存在一些数据→为了解决一个问题，软件工程师编写一个流程来告诉机器应该怎样做→计算机遵照这一流程执行，然后得出结果
②统计学：分析师比较变量之间的关系
③机器学习：数据科学家使用训练数据集来教计算机应该怎么做，然后系统执行该任务。首先存在大数据→机器会学习使用训练数据集来进行分类，调节特定的算法来实现目标分类→该计算机可学习识别数据中的关系、趋势和模式
④智能应用：智能应用使用人工智能所得到的结果，如图是一个精准农业的应用案例示意，该应用基于无人机所收集到的数据

## 机器学习的发展
![](/assets/1-5.jpeg)

### 机器学习中的五大流派
几十年来，人工智能研究者的各个「部落」一直以来都在彼此争夺主导权，现在这些部落开始联合起来，因为合作和算法融合是实现真正通用人工智能（AGI）的唯一方式。

学派|核心理念|主算法|灵感来源
---|---|---|---
符号学派|使用符号、规则和逻辑来表征知识和进行逻辑推理|规则/决策树|逻辑学
贝叶斯学派|获取发生的可能性来进行概率推理|贝叶斯/马尔科夫|统计学
连接学派|使用概率矩阵和加权神经元来动态地识别和归纳模式|反向传播/神经网络|神经科学
进化学派|生成变化，然后为特定目标获取其中最优的|基因编程|遗传学
类推学派|根据约束条件来优化函数（尽可能走到更高，但同时不要离开道路）|支持向量机|数学最优化

### 机器学习的历史演化阶段

![](/assets/1-6.jpeg)

时间|1980s|1990-2000|2000-2010s
---|---|---|---
主导学派|符号学派|贝叶斯学派|联结学派
架构|服务器或大型机|小型服务器集群|云服务器
主导理论|知识工程|概率论|神经科学和概率
优势|决策支持系统|可扩展的对比|在图像和语音识别、情感分析领域更加准确

### 机器学习的未来发展趋势
![](/assets/1-7.jpeg)

时间|Late 2020s|2020s+|2040s+
---|---|---|---
主流学派|连接学派+符号学派|联结主义+符号主义+贝叶斯+……|算法融合
架构|云计算|云计算和雾计算|无处不在的服务器
主导理论|记忆神经网络、大规模集成、基于知识的推理|通过神经网络来感知、通过规则来决策|最佳组合的元学习
场景|简单问答系统|简单的感知-推理-行动|基于通过多种学习方式获得的知识或经验采取行动或做出回答
























