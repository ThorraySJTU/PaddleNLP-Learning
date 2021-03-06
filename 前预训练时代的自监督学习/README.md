# 前预训练时代的自监督学习

## 神经网络

模仿生物神经网络结构功能的非线性统计性数据建模工具 —— 分类/回归器

- 前向传播：给定输入，预测结果 
- 反向传播：给模型参数反馈预测结果和真是target的差距，并指导参数作出调整 —— 损失函数

负梯度反向传播 —— 负梯度方向进行搜索可以最快速的下降

## 自监督 词表示 学习

- 语言单元的表征

  - One-hot独热编码
    - 特征稀疏
    - 词之间相互独立，没有顺序关系
    - 不能表征词与词之间的关系，one-hot之间正交
  - Embedding编码
    - 特征稠密（将one-hot线性映射到低维空间）
    - 能够表征词与词之间的相互关系
    - 泛化性能更优，支持语义运算

- 词向量模型Word2Vec

  分布式假设：具有相似上下文的词语意应该是相近的，关系更加紧密

  - skip-gram（给定中间词 预测 上下文)
    - 输入：中间词wt的one-hot，上下文窗口为C
    - 中间词one-hot和词向量矩阵相乘，得到隐层向量
    - 在上下文窗口2C中采样num_skips个上下文单词作为target
    - 隐层向量乘输出权重矩阵，过softmax得到每个单词的预测概率
    - 输出：预测概率和采样的上下文单词的交叉熵loss
  - CBoW（给定上下文 预测 中间词)
    - 输入：上下文单词的one-hot，上下文单词数量为C
    - 上下文单词one-hot分别和词向量矩阵相乘，得到对应词向量，加和平均得到隐层向量
    - 隐层向量乘输出权重矩阵，过softmax得到每个单词的预测概率
    - 输出：真实中间词wt预测概率的交叉熵loss

## 句子编码神经网络

- 自回归语言模型 n-gram语言模型 —— 马尔可夫假设
- 循环神经网络
  - 作为Encoder对长度任意的序列进行特征提取
  - 作为Generators学习Language Model
  - 存在梯度爆炸、消失的风险
  - time step无法并行
  - 无法对具有层次结构的信息进行很好的表达
- Self-Attention
- Transformer Encoder（Attention - Residual connections - Layer normalization）
  - 为了保证数据特征分布的稳定性 —— 层归一化

## 自回归、自编码预训练学习

- GPT（自回归预训练） 

- BERT（自编码 AutoEncoder Pretraining）

