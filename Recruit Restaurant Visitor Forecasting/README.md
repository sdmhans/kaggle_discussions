## Recruit Restaurant Visitor Forecasting
### 11th:
- [Xiuqi][9], [discussion][10]
- 验证集：2016.12.29开始的33天+2017.4.22结束的33天（新年和黄金周有相似之处，无eda）
- 去除预测天前7天内的预订信息（防过拟合）
- 移动加权平均（按每个店）
- 距离上/下一个节假日的天数
- 天气：下雨和平均气温
- 模型融合：LGBM,XGB,RF和prophet(private:0.535)

### 20th: (未完成)(见22rd 30CrMnSiA.md)
- [YuyaYamamoto][4], [discussion][5]

### 22rd：(见22rd 30CrMnSiA.md)
- [30CrMnSiA][1], [discussion][2], [kernel][3]

### 48th：(见48th Shize Su.md)
- [Shize Su][6], [discussion][7], 含[Danijel Kivaranovic][8](5th)

比赛小总结：
- golden week的一些解决方案
  - eda，节假日视作周六，节前一天非工作日时视作周五，节后一天非工作日时视作周一(30CrMnSiA)
  - 距离上/下一个节假日的天数(Xiuqi)
  - 视holiday和weekend为相同：holiday_flg2(piupiu)
- 验证集的选择
  - 39天（与LB相似）(Shize Su)
  - 80天(fakeplastictrees)
  - 回归类型的kfold(Max Halford):可能不是一个较好的选择
- 使用较深的lag特征(Shize Su, Danijel Kivaranovic)
- 加权移动平均(Shize Su)
- 防过拟合、订位信息的正确使用：分天预测，线下cv中第n天预测的训练集不应包括前(n-1)天的数据(Shize Su)

  [1]: https://www.kaggle.com/h4211819
  [2]: https://www.kaggle.com/c/recruit-restaurant-visitor-forecasting/discussion/49100
  [3]: https://www.kaggle.com/h4211819/holiday-trick/code
  [4]: https://www.kaggle.com/nejumi
  [5]: https://www.kaggle.com/c/recruit-restaurant-visitor-forecasting/discussion/49328
  [6]: https://www.kaggle.com/sushize
  [7]: https://www.kaggle.com/c/recruit-restaurant-visitor-forecasting/discussion/49174
  [8]: https://www.kaggle.com/danijelk
  [9]: https://www.kaggle.com/lixiuqi
  [10]: https://www.kaggle.com/c/recruit-restaurant-visitor-forecasting/discussion/49177
