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







