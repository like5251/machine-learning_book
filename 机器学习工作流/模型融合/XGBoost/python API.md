# XGBoost Python API

```python
import xgboost as xgb
from xgb.sklearn import XGBClassifier as XGBC
```

1. 两种数据类型：
    1. xgb.DMatrix：xgb矩阵，用于表示数据集。对内存和速度进行了优化。您可以从numpy.arrays构造DMatrix。
    2. xgb.Booster：模型对象。常用于访问模型参数、predict预测、模型持久化存储。
2. 两个顶级函数：
    1. xgb.train：在给定训练集、Booster参数和训练参数的条件下进行训练，返回一个训练完成的Booster对象。
    2. xgb.cv：在给定训练集、Booster参数和交叉验证参数的条件下进行训练，返回验证结果list(string)。
3. 与sklearn的接口：
    1. xgboost.XGBClassifier：设置“三种参数”，返回一个sklearn风格的分类模型实例。方便使用sklearn中的参数名和其他方法，如网格搜索。
    2. xgboost.XGBRegressor：略
    
    
## 两种数据类型
### DMatrix
`class xgboost.DMatrix(data, label=None, missing=None, weight=None, silent=False, feature_names=None, feature_types=None, nthread=None)`

一般只用到前四个参数：
- data：特征空间数据集，`shape = [n_samples, n_features]`。支持ndarray-like数据，如DataFrame、Series或ndarray
- label：标记空间数据集，`shape = [n_samples]`。可选，支持的数据类型同上
- missing：自动填充缺失值，可选。
- weight：为每行样本赋权值，`shape = [n_samples]`。可选，支持的数据类型同上

```python
train = pd.read_csv()
featrues = [f for f in train.columns if condition]
target = 'label'

dtrain = xgb.DMatrix(train[featrues], train[target], missing = -999.0, weight=train.weight)

```

DMatrix的属性和方法不常使用。

### Booster
`class xgboost.Booster(params=None, cache=(), model_file=None`

关于params，有三种参数可以设置，详见“XGBoost调参”

#### 常用方法
1. 预测：`predict(data, output_margin=False, ntree_limit=0, pred_leaf=False, pred_contribs=False)`
    - data:DMtrix格式的特征空间
    - output_margin：是否输出原始的未转换的margin值
    - ntree_limit:限制预测数据中的树颗数，默认为0，使用所有树
    - 返回：numpy array格式的预测结果
2. 获取属性：Booster.attributes()
3. 设置参数：Booster.set_param(key=value)
4. 保存/加载模型：Booster.save_model('name.model')

## 两个顶级函数
### train
`xgboost.train(params, dtrain, num_boost_round=10, evals=(), obj=None, feval=None, maximize=False, early_stopping_rounds=None, evals_result=None, verbose_eval=True, xgb_model=None, callbacks=None, learning_rates=None)`

返回一个训练完成的Booster对象。

参数说明：
1. params(dict)：Booster参数，参见“XGB调参”
2. dtrain(DMatrix)：训练集
3. num_boost_round(int)：迭代次数
4. evals (list of pairs (DMatrix, string)) ：监测列表，每个监测对象用（数据集,字符串）表示，如[(dtrain,'train'),(dval,'val')]，可以在训练过程输出监测列表中多有对象的性能结果。
5. obj (function) ：用户自定义objective目标函数
6. feval (function) ：用户自定义的评估函数
7. maximize (bool) ：是够最大化fever
8. early_stopping_rounds :提前停止迭代。如果设为100，如果训练过程中任意相隔100次迭代的结果没有下降，则结束训练，返回最后一次迭代后的模型。需要evals中至少有一个元素，如果有多个元素则会以最后一个元素的在每轮迭代的性能得分作为评判标准。如果训练提前结束，模型会有三个属性`bst.best_score`, `bst.best_iteration`, `bst.best_ntree_limit`，分别对应最佳得分，最佳迭代次数、最佳树颗数限制（迭代次数+1）
9. learning_rates（列表或函数）：控制每一次迭代的学习率，注意与params中的eta不同。
10. verbose_eval (bool or int)：控制运行信息的打印频率

### cv
`xgboost.cv(params, dtrain, num_boost_round=10, nfold=3, stratified=False, folds=None, metrics=(), obj=None, feval=None, maximize=False, early_stopping_rounds=None, fpreproc=None, as_pandas=True, verbose_eval=None, show_stdv=True, seed=0, callbacks=None, shuffle=True)`

返回交叉验证的性能评估历史list(string)。

参数：基本=train参数+交叉验证参数（kfold metrics）

1. params(dict)：Booster params，参见XGB调参
2. dtrain (DMatrix) ： Data to be trained
3. num_boost_round (int) – Number of boosting iterations
4. nfold (int) – Number of folds in CV，参见[sklearn交叉验证](http://scikit-learn.org/stable/modules/cross_validation.html)
5. stratified (bool) – Perform stratified sampling.
6. folds (a KFold or StratifiedKFold instance) – Sklearn KFolds or StratifiedKFolds.类似于kf.split(train)返回的对象[([train indices],[val indices])...]
7. metrics (string or list of strings) – Evaluation metrics to be watched in CV.参见参数调整中eval_metrics
8. obj (function) – Custom objective function.
9. feval (function) – Custom evaluation function.
10. maximize (bool) – Whether to maximize feval.
11. early_stopping_rounds (int) – Activates early stopping. CV error needs to decrease at least every <early_stopping_rounds> round(s) to continue. Last entry in evaluation history is the one from best iteration.
12. fpreproc (function) – Preprocessing function that takes (dtrain, dtest, param) and returns transformed versions of those.预处理函数
13. as_pandas (bool, default True) – 返回pandas类型
14. verbose_eval (bool, int, or None, default None) – Whether to display the progress. If None, progress will be displayed when np.ndarray is returned. If True, progress will be displayed at boosting stage. If an integer is given, progress will be displayed at every given verbose_eval boosting stage.
15. show_stdv (bool, default True) – Whether to display the standard deviation in progress. Results are not affected, and always contains std.
16. seed (int) – Seed used to generate the folds (passed to numpy.random.seed).

### sklearn接口
`class xgboost.XGBRegressor(max_depth=3, learning_rate=0.1, n_estimators=100, silent=True, objective='reg:linear', booster='gbtree', n_jobs=1, nthread=None, gamma=0, min_child_weight=1, max_delta_step=0, subsample=1, colsample_bytree=1, colsample_bylevel=1, reg_alpha=0, reg_lambda=1, scale_pos_weight=1, base_score=0.5, random_state=0, seed=None, missing=None, **kwargs)`

返回：sklearn兼容的生model。

参数：三种参数，参见XGBoost调参






















