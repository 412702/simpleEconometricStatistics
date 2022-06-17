### simpleEconometricStatistics
#### 计量经济学课程作业，简单做个回归与检验
 
数据处理使用Python 再Jupyter 环境下进行，整个程序包可在Jupyter下直接打开

统计过程使用的计算的包有sklearn（https://scikit-learn.org/stable/）
和statsmodels（https://www.statsmodels.org/）

绘图使用的是plot（https://plotly.com/python/）
文中使用的公式大多参考自大工经管学院陈德湖老师课程所讲内容。

## 最后 注 -- 发现statsmodels 进行White检验的时候发现源程序包存在问题
源码中White检验存在问题，在检验中，源码要求检验自由度（断言），自由度要最终检验要求应当是  变量数-常量数 == 样本秩-1，但是源码中使用的OLS回归并没有加入 hasconst=True
同时另一个问题是，参考资料上White检验中是包含一次项的，但是源码中只有二次项，没有一次项

问题源码包位置~/statsmodels/stats/diagnostic.py Line 999, 这里会报错

解决方案就是在OLS回归那一行中加上一个参数就好了 hasconst=True
```python
resols = OLS(y ** 2, exog).fit()
```

改成 

```python 
resols = OLS(y ** 2, exog, hasconst=True).fit()
```
