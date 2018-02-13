# kaggle discussions
Kaggle比赛经验总结

已完成的部分：
## 1、Recruit Restaurant Visitor Forecasting(381st/top 18%)

### 20th: 
- [YuyaYamamoto][4], [discussion][5]

### 22rd：
- [30CrMnSiA][1], [discussion][2], [kernel][3]


### 48th：
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

## 2、Corporación Favorita Grocery Sales Forecasting(31st/top 2%/silver)


## 3、Porto Seguro’s Safe Driver Prediction(584th/top 12%)


## 4、Statoil/C-CORE Iceberg Classifier Challenge(223rd/top 7%/bronze)