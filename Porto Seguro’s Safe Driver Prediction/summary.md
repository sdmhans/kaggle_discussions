## Porto Seguro's Safe Driver Prediction
### 8th：(未完成)
- [ironbar][1], [discussion][2], [kernel][3]

- 缺失值处理（代码未给出）
  - 缺失值数量小于50时，使用众数替换；否则创建专门的一个缺失的类别

- 特征工程
  - calc特征：去除
  - cat类别特征：独热编码
  - 数值离散型特征（只有少量的类别）：使用数值型特征的大小关系，判断该值是否大于其他的值
  - 数值离散型+cat类别特征：target encoding（类似贝叶斯平滑？留个坑）
  - target encoding后删去cat类别特征

- 特征标准化
  - 数值特征：非二元(bin)、类别(cat)、数值离散编码(cbe)、目标编码(tef)的特征
  - 需要标准化的特征为数值特征 + tef特征
  - 均值+标准差（非归一化，不一定是0-1区间）
  - 限制最大值（负数取绝对值）为5：大于时，按照$5/max\_value$进行缩放(将最大值同比缩小为5)

- 特征分类（数据集构造）
  - 按individual/region/car和cat/non-cat分为6类
  - cat特征:cat+cbe
  - 非cat特征：bin+numeric（包含数值离散特征）+tef


  [1]: https://www.kaggle.com/ironbar
  [2]: https://www.kaggle.com/c/porto-seguro-safe-driver-prediction/discussion/44601
  [3]: https://www.kaggle.com/ironbar/taylor-made-nn-for-0-285-plb-part-of-8/