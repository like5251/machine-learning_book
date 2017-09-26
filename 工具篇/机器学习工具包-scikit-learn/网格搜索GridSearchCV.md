[sklearn.model_selection.GridSearchCV](http://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)，用于自动搜索超参数的最优值。GridSearchCV从之前的grid_search模块移动到了model_selection模块。

## 简介
思路：
1. 按照超参数的重要度（依赖于经验和理论）依次对参数进行调优，对于每个参数或每两个参数，调优的过程如下
2. 首先猜测某个超参数的大致范围，其余参数取初始估计值
3. 将该超参数名作为key（字符串），对应的取值范围作为value（列表）构造出param_grid字典，连通其他参数一起传入GridSearchCV
4. GridSearchCV系统的遍历多种参数组合，通过交叉验证确定最佳的参数
5. 交叉验证中最重要的是确定[评估指标metrics](http://scikit-learn.org/stable/modules/classes.html)和评估方法(传入k-fold 的indices)
6. 通过GridSearchCV对象的best_params_ 属性获取最佳参数，best_score_属性获取最佳性能得分

缺点：
1. 这个方法适合于小数据集，一旦数据的量级上去了，很难得出结果。此时通常采用一种贪心算法：拿当前对模型影响最大的参数调优，直到最优化；再拿下一个影响最大的参数调优，如此下去，直到所有的参数调整完毕。这个方法的缺点就是可能会调到局部最优而不是全局最优，但是省时间省力，巨大的优势面前，还是试一试吧，后续可以再拿bagging再优化。

## 参数解读

```
class sklearn.model_selection.GridSearchCV(estimator, param_grid, scoring=None, fit_params=None, n_jobs=1, iid=True, refit=True, cv=None, verbose=0, pre_dispatch=‘2*n_jobs’, error_score=’raise’, return_train_score=True)[source]
```



## 常用属性

```python
da
```
