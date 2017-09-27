xgboost有两种使用方式：标准方式和sklearn方式。鉴于sklearn提供了更丰富的功能（如网格搜索），并且使用广泛，推荐使用后者（通用-强大）。

## sklearn方式
```python
# 导入方式
from xgboost.sklearn import XGBClassifier as XGBC
import pandas as pd
```
### 1. 数据准备
sklearn方式对数据要求比较轻松，只要是array-like类型的就可以。

```pyton
train = pd.read_csv()
test = pd.read_csv()

featrues = [f for f in train.columns if condition]
target = 'label'

```
### 2. 模型选择
1. 先通过XGBClassifier构建一个“生”模型，参数取初始预估值

```python
xgb1 = XGBClassifier(
        learning_rate =0.1,
        n_estimators=3,
        max_depth=8,
        min_child_weight=3,
        gamma=0,
        subsample=1,
        colsample_bytree=0.7,
        objective= 'binary:logistic',
        nthread=4,
        scale_pos_weight=1,
        seed=27)
```

2.  






