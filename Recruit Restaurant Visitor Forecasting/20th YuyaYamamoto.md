# Recruit Restaurant Visitor Forecasting
### 20th：[YuyaYamamoto][1]
原帖链接：[discussion][2]

###1、问题的设置
虽然训练集包括16~17年4月的数据，然而大多数餐馆并没有16年1月的观测数据。最糟糕的情况是，某些餐馆的第一次观测数据为17年3月，即紧挨着测试集。

###2、验证方法
在做特征工程之前，我们把训练集最后一个月的数据作为线下验证集。验证集又被分为线下public（前6天）和线下private（其余），这一方法可以避免对public榜的过拟合。

###3、特征工程
- 目标编码（target encoding）



- 天气特征



  [1]: https://www.kaggle.com/nejumi
  [2]: https://www.kaggle.com/c/recruit-restaurant-visitor-forecasting/discussion/49328