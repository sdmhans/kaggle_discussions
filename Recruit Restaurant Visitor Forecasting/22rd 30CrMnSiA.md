# Recruit Restaurant Visitor Forecasting
### 22rd：[30CrMnSiA][1]
原帖链接：[discussion][2], [kernel][3]
holiday规则: private榜能够提升9个千分点
- 将节假日视作周六
- 如果节假日前一天为工作日，将该天视作周五
- 如果节假日后一天为工作日，将该天视作周一

private(17.4.29~17.5.31)中的假日有4.29(周六),5.3(周三),5.4(周四),5.5(周五)，且lightGBM的预测值有明显的week周期性（同曜日相近），故具体做法如下：
- 4.28(周五，情况2)：本身是周五，不做处理
- 4.29(周六，情况1)：本身是周六，不做处理
- 4.30(周日，情况3)：非工作日，不做处理
- 5.2(周二，情况2)：使用4.28(周五)和5.12(周五)预测值的几何平均
- 5.3/5.4/5.5(周三/四/五，情况1)：使用4.29(周六)和5.13(周六)预测值的几何平均
- 5.6（周六，情况3）：非工作日，不做处理

测试：我们队private最优为0.516（public0.474），使用该trick后private为0.509(conservative版)和0.510(radical版)

一点心得体会：时序题：观察数据规律，尝试解释极大极小值（节假日、周末、特殊天气、特殊事件）

  [1]: https://www.kaggle.com/h4211819/
  [2]: https://www.kaggle.com/c/recruit-restaurant-visitor-forecasting/discussion/49100
  [3]: https://www.kaggle.com/h4211819/holiday-trick/code
  