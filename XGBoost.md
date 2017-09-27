## XGBoost实战参考

### 一、官网参考
[xgboost官网](http://xgboost.readthedocs.io/en/latest/)的一些常用资源：

#### XGBoost理论
1. [提升树简介](http://xgboost.readthedocs.io/en/latest/model.html)

#### XGBoost示例
1. [XGBoost python简单实例](http://xgboost.readthedocs.io/en/latest/get_started/index.html)
2. [XGBoost更多实例](https://github.com/dmlc/xgboost/tree/master/demo)

#### XGBoost参数
1. [控制过拟合和不平衡数据的一般方法](http://xgboost.readthedocs.io/en/latest/how_to/param_tuning.html)
2. [XGBoost的参数-原版](http://xgboost.readthedocs.io/en/latest/parameter.html)
3. [XGBoost的参数-译文](https://jiayi797.github.io/2017/04/28/xgboost%E5%8F%82%E6%95%B0/)

#### python API
1. [python XGBoost工作流-原版](http://xgboost.readthedocs.io/en/latest/python/python_intro.html)
2. [python XGBoost工作流-翻译](http://blog.csdn.net/zc02051126/article/details/46771793)
3. [python XGBoost工作流-示例](https://github.com/tqchen/xgboost/tree/master/demo/guide-python)
4. [XGBoost Python API](http://xgboost.readthedocs.io/en/latest/python/python_api.html)
5. [XGBoost的源码和详细API（强力推荐）](https://rdrr.io/cran/xgboost/api/)

### 二、其他参考

[XGBoost原理解析.pdf]()
[陈天奇XGBOOST.pdf]()
[xgboost实战]()
[机器学习xgboost实战—手写数字识别](http://blog.csdn.net/eddy_zheng/article/details/50496186)
[XGBoost参数调优完全指南（附Python代码,强力推荐）](http://blog.csdn.net/u010657489/article/details/51952785)：有数据有代码有说明

[xgboost 调参经验-train参数说明](http://blog.csdn.net/u010414589/article/details/51153310)

[xgboost 调参经验](http://blog.csdn.net/u010414589/article/details/51153310)

### 三、实战用到

1. [sklearn-metrics性能指标分类](http://scikit-learn.org/stable/modules/model_evaluation.html#scoring-parameter)：xgboost中对数损失对应的是'logloss'，sklearn中对应'neg_log_loss'

2. [sklearn-gridsearch网格搜索](http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)：指定参数范围、模型、性能指标、k-fold验证、=》输出最佳参数

3. [xgboost-xgbcv交叉验证-迭代参数选择](http://xgboost.readthedocs.io/en/latest/python/python_api.html)

4. [xgboost-DMatrix带权重数据导入](http://xgboost.readthedocs.io/en/latest/python/python_intro.html)




## API

XGBoost

### 核心数据结构：
- DMatrix类：是xgboost使用的最基本的数据类型，在将data+label转化为DMtrix类型时，可以对每个样本赋权值。
- Booster类：xgboost模型的类型，最重要的shipredict()方法和模型持久化存储，获取特征排序；

### 机器学习相关API
`xgboost.train(params, dtrain, num_boost_round=10, evals=(), obj=None, feval=None, maximize=False, early_stopping_rounds=None, evals_result=None, verbose_eval=True, xgb_model=None, callbacks=None, learning_rates=None)`

- 


## xgboost调参
运行XGBoosth之前，必须设置三种参数：
1. 基本(General)参数：设置要使用的基本模型
2. 提升(Booster)参数：在每一步指导每个提升（树或回归）
3. 学习任务(Learning Task Parameters)参数：指导优化模型表现

### 1、基本参数

1. 【booster】[默认为gbtree]：每次迭代的基本模型类型。默认为gbtree，树模型；也可以是gblinear，线性模型
2. 【silent】[默认为0]：是否为静默模式。默认为0，运行时不打印running messages；若为1，则打印。
3. 【nthread】[默认最大线程]：进程数。默认为最大线程。

### 2、提升参数
树模型和线性模型的提升参数有所不同，这里只介绍tree booster，因为它的表现远远胜过linear booster，所以linear booster很少用到。

1. 【eta】[默认为0.3]：学习率，别名learning_rate。取值在[0,1]，越大算法收敛的越快，但过大的话损失函数会发生震荡。
2. 【max_depth】[默认为6]：每棵树的最大深度，越大学习能力越强也越容易过拟合；
3. 【min_child_weight】[默认为1]：最小叶节点权重和。
越大学习能力越若越容易欠拟合。
4. 【gamma】(默认为0)：节点分裂最小损失函数下降值。越大学习能力越若越容易欠拟合。
5. 【subsample】[默认1]：构建每棵树时对数据集的行采样比例。值越大学习能力越强，越容易过拟合，一般取值[0.5,1]。
6. 【colsample_bytree】[默认为1]：构建每棵树时对数据集的列采样比例。值越大每棵树用到的特征越多，越容易过拟合。一般取值[0.5,1]。
7. 【colsample_bylevel】[默认为1]：树的每一级的每一次分裂，对列数的采样的占比
8. 【alpha】[默认为0]：L1正则项系数，别名reg_alpha。值越大模型复杂度越小，越不容易过拟合。
9. 【lambda】[默认为1]：L2正则项系数，别名reg_lambda。值越大模型复杂度越小，越不容易过拟合。
10. 【max_leaves】[默认为0]：添加的最大叶子树。Only relevant for the ‘lossguide’ grow policy.
11. 【scale_pos_weight】[默认为1]：控制正负样本权重的平衡。一般对非平衡的很有用。一个很特殊的取值是：负样本个数/正样本个数。

### 3、 任务参数

1. 【objective】[默认为reg:linear]：可选的学习目标如下：
    - “reg:linear” –线性回归。
    - “reg:logistic” –逻辑回归。
    - “binary:logistic” –二分类的逻辑回归问题，输出为概率。
    - “binary:logitraw” –二分类的逻辑回归问题，输出的结果为wTx。
    - “count:poisson” –计数问题的poisson回归，输出结果为poisson分布。在poisson回归中，max_delta_step的缺省值为0.7。(used to safeguard optimization)
    - “multi:softmax” –让XGBoost采用softmax目标函数处理多分类问题，同时需要设置参数num_class（类别个数）
    - “multi:softprob” –和softmax一样，但是输出的是ndata * nclass的向量，可以将该向量reshape成ndata行nclass列的矩阵。没行数据表示样本所属于每个类别的概率。
    - “rank:pairwise” –set XGBoost to do ranking task by minimizing the pairwise loss
2. 【eval_metric】[默认值根据objective参数调整]：性能指标
    - rmse – root mean square error
    - mae – mean absolute error
    - logloss – negative log-likelihood
    - error – Binary classification error rate (0.5 threshold)
    - merror – Multiclass classification error rate
    - mlogloss – Multiclass logloss
    - auc: Area under the curve
3. 【seed】[默认为0]：随机数种子，置它可以复现随机数据的结果，也可以用于调整参数





















