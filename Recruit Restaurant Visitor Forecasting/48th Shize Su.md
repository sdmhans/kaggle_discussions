# Recruit Restaurant Visitor Forecasting
### 48th：[Shize Su][1]
原帖链接：[discussion][2]

- 分数：
  - 使用30CrmnSiA的holiday trick后，xgb模型private:0.516->0.508
  - xgb: public 0.470, private 0.516, nn: public 0.476, private 0.528, 0.7-0.3融合这两个模型:public 0.468, private 0.515

- 验证集：
  - 从17.3.12（周日）开始的最后39天（与Corporación的类似）

- 特征(300+)：在surprise-me-2-neural-networks-keras的基础上做的
  - 同air_store_id同曜日的前14次游客数量(lagging visitors features)：该比赛中较深的lag效果好
  - 同air_store_id的前14次游客数量
  - lagging特征的一阶差分(13个)，四阶差分(10个)
  - lagging特征的加权移动平均(WeightedMovingAverage)
  - 同曜日状态信息：前14，28，60，90，120，180，364天内同air_store_id同曜日的mean/median/min/max/(percentile10,30,70,90)/sum/count 游客数量记录
  - 同曜日状态信息：前14，28，60，90，120，180，364天内同air_store_id同曜日的mean/median/min/max/(percentile10,30,70,90)/sum/count 游客数量记录

- 防过拟合：
  - 对LB中的每一天分别提取特征，因为当我们想对LB中的第n天进行预测时，前(n-1)天的数据是无法获取的，因此我们必须去**除去训练集前(n-1)天内的游客数量信息**，订位(reservation)信息同理，只能使用订位日期在(n-1)天之前的信息

- [Danijel Kivaranovic][3](5th)的做法（没有专门post）
  - 使用很深的lag：周平均数量使用了20个lag，月平均数量使用了8个lag
  - 使用holiday的0/1标志特征：前一/两天或后一/两天是否是节假日（可以捕获一部分的节假日信息）

- 验证集误差总是小于训练误差，是训练nround不够的原因吗？
  - 是正常的，因为训练数据的方差就较大，如果数据分布更加相似/稳定时，验证误差反而会大于训练误差
  - 判断训练nround是否足够：使用早停，或尝试增大nround看验证误差是否下降（相信验证误差的结果）

  [1]: https://www.kaggle.com/sushize
  [2]: https://www.kaggle.com/c/recruit-restaurant-visitor-forecasting/discussion/49174
  [3]: https://www.kaggle.com/danijelk