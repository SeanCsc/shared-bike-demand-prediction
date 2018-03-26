# shared-bike-demand-prediction
v1.1 - 以城市San Jose为例
数据感和实际意义。

目标： 预测某天某个城市的出行量
评价指标：RMSE

考虑到某个城市的人可能会选择该城市另一个相近的车站如果该车站没有自行车可以提供，因此预测某个城市某一天的出行量比预测某车站的出行量更有实际参考价值。

## 数据提取与导入

因为数据源来自于四个不同的文件（车站信息，trip信息，天气信息，status）,本次project只用到前三个表的信息。

从车站信息中可以提取车站所在的城市，以及车站的自行车数量，进而得到车站的自行车数量。

trip文件可以提供每天每个城市的出行数量，这个作为最后的预测输出值。从trip表中提取出日期，trip数量和城市。

weather可以提供某天的天气信息（温度，湿度等），通过zip code可以和城市连接起来

## Baseline:
使用每天trip数量的平均值作为预测，得到RMSE

## 特征工程和预处理

#### 缺失值处理

天气数据中存在比较多的缺失值，比如事件(event)中，将缺失值填充为normal,另外在event中，使用unique函数可以看到有不同的词来表示相同的意思，也进行合并。

其他缺失值使用中位数填充。

#### 数据转换
由于线性模型(Lasso, Ridge, Enet)通常要满足输出呈正态分布，因此先检测是否skewed,然后通过某些变换将其变为normal distribution。另外，
对于线性模型，最好去掉量纲（归一化）。使用make_pipeline完成，在输出线性模型前先进行RobustScaler()。

#### 特征添加与组合
时间特征：是否是weekday,是否是holiday,是否是business day， 年， 月， 周几， 

#### 特征属性转换
对于离散object 特征使用one-hot encoding转换

## 模型

#### 模型评估
使用cross validation进行模型评估。

#### 模型选择

利用GridSearch选择最佳参数。

模型选择：
线性模型（Lasso, Ridge, Enet)

树模型(XGBoost)











## 直观地解释
