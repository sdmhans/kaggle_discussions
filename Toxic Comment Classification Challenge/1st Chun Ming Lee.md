# Toxic Comment Classification Challenge
### 1st:[Chun Ming Lee][1]
原帖链接: [discussion][2]

- 1、多样化的预训练的embedding层(baseline，public榜0.9877)
  - 由于模型中超过90%的复杂度都位于嵌入层，我们决定重点关注嵌入层而不是嵌入层之后的层。
  - 嵌入层：最高维度(300d?还是900d?)的FastText和Glove，基于普通抓取的网页(Crawl)、Wikipedia或Twitter上的留言
  - 嵌入层之后：两个双向GRU层(gru结点数量?)，它们的输出被传入最后的两个全连接层(隐藏层数量?)

- 2、使用翻译后的文本作为训练/测试时的数据增强(TTA)(0.9877->0.9880)
  - Pavel Ostyakov的想法：使用机器翻译的结果来增强训练集和测试集的数据(先翻译成法语/德语/西班牙语后，再翻译回英语)
  - 防止信息泄露：确保了所有的翻译文本与其原文本在cv的同一fold中
  - 预测：将四种翻译后结果（原/法/德/西）的预测值进行平均
  - 效果：TTA后Bi-GRU模型从0.9862提升至0.9874（单模型比其他队伍的融合结果要好）
  - 用于“修正”非英语的评论：直接把原评论翻译成英文有副作用，不如完整的数据增强效果好

- 3、伪标签(pseudo-labelling)(0.9880->0.9885)
  - 尝试过很多PL的变种，如canonical per-batch updates(?)、修改损失函数等
  - 效果最好：使用最好的融合模型将测试集打上伪标签，将它们放入训练集中，然后训练至收敛
  - PL有助于解决训练集和测试集分布不一的问题

- 4、5fold CV+stacking框架(0.9885->0.9890)
  - 对算术平均和stacking做了加权平均，比这两种方法的单独使用高了~1个万分点
  - stack第二层使用LightGBM(比XGBoost快)，使用bayesian optimization可以获得稍高一些的CV分数
  - 参数选择：使用bayesian optimization运行250次选出最好的，关键：depth小、强l1正则
  - 避免stack过程中可能的方差：DART和GBDT使用不同随机seed各跑6次，然后bag
  - 选择模型：CV-log损失、CV-AUC、public榜AUC，抛弃stack+blend过程中三个指标都得不到提升的模型（防过拟合）

- 5、其他
  - 模型复杂度主要在预训练的嵌入层，网络架构的小改变对分数的影响不大
  - 预处理（包括拼写修正）影响不大（例外：使用fasttext时保留标点符号有助于stacking）
  - 很多评论的toxic之处在于其最后的几句话，使用最末尾的25-50个词来训练额外的模型有助于stacking
  - 一些方法很难处理词的排列顺序（两个词调换位置，意思会完全改变）。由于CNN方法依赖max-pooling，使用它们会比最好的RNN低~0.0015
  - 其他的模型很难达到与RNN相近的分数，除了Attention Is All You Need（Attention模型？），但是它训练时间很长
  - 可以把不同OOF分割方式的模型进行融合：只要不去对比不同OOF分割的分数
  - 主要的模型：RNN、几个CNN和一个

  [1]: https://www.kaggle.com/leecming
  [2]: https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/discussion/52557

