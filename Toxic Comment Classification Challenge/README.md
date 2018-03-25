## Toxic Comment Classification Challenge
### 1st:(见1st Chun Ming Lee.md)
- [Chun Ming Lee][1], [discussion][2]

### 3rd:
1、[Alexander Burmistrov][3]0.9872的单模型, [discussion][4]
- 预处理
  - embedding层除了同时使用fasttext和glove外，额外添加一维（该单词是否全部由大写字母组成）
- 架构
  - embedding层(501维=fasttext300+glove twitter200+1)

### 其它待填的坑
- 理论
  - embedding层训练
  - 双向GRU&LSTM结构
  - Attention
  - DPCNN
  - CapsuleNet
  - HAN
  - Wordbatch

- 实验
  - Alexander Burmistrov的0.9872bi-GRU[讨论帖][3]
  - PL（伪标签）
  - stacking(xgb和hyperopt的对比)
  - 机器翻译做数据增强


  [1]: https://www.kaggle.com/leecming
  [2]: https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/discussion/52557
  [3]: https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/discussion/52644
  [4]: https://www.kaggle.com/mrboor
  [5]: https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/discussion/52644