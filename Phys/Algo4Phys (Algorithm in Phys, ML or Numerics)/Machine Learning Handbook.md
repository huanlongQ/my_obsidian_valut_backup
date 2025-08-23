**My Machine Learning Handbook**

# Review of deep research

# 1. History of Machine Learning

## 1.1 单层网络

感知机(perception) 
![[Pasted image 20250328110555.png]]

不能实现线性不可分问题(Linearly Non-separatable Problems), 如XOR异或等问题. 其原因在于单层perception本质上没有引入什么非线性.
![[Pasted image 20250328110630.png]] 
 
  

## 1.2 Backward Propagation and Multi-layers

引入Backward Propagation(Hinton)和Multi Layers Neural Network

## 1.3 CNN(LeCun) and Deep Learning(AlexNet, Ilya)

CNN(LeCun Yang) shows ML's ability of classification

AlexNet(Ilya) shows the same ability in image calssification

**AlexNet used GPU(Graphic Program Unit)**

## 1.4 Sequence Process

RNN -> LSTM

seq2seq(Ilya) word2vec(Ilya)

Attention -> Bert and Transformer

  

  

  

# 2. Ab initio Machine Learning

## 2.1 Training Strategy

1. Backward Propagation
    
Backward Propagation = optimal problem of  L_\theta(y,ML(x)) with respect to \theta

BP使用的是对\theta的梯度下降方法, 关键在于计算partial L / partial theta_i, 并全局地以learning_rate优化每一个theta_i.

$\partial L / \partial \theta_i = \partial L / \partial y \partial y / \partial x_{somelayer} ... \partial x_{somelayer} / \partial \theta$

BP的实现方法是在Neural Network的每个Neurons处存储grad值, 形成一个有结构的梯度图, 这个梯度图用于计算partial L / partial theta_i .

2. Supervised or Unsupervised
    
3. Reinforcement Learning
    

## 2.2 Function of Machine Learning

1. Classification(Softmax)
    
2. Clustering(聚类)
    **K means algorithm** 
3. Generative Model: GAN(Generative Adversary Net), Seq2seq(Next Token Prediction)
    
4. Representing Learning: 深入学习数据特征features, 如word2vec、Bert、CNN的浅层通用性、Contrastive Learning等
    
5.   
    

## 2.3 Obejcts of Machine Learning

1. Multi Modal:image (computer vision)
    
2. Nature Language Process
    
# 3. Details

## 1. Residual Connection

Residual Connection会导致Train的时间和内存消耗急剧加大, 其原因在于:

1. 为保证BP的正常运行, ResNet的各个Neurons必须同时存储两个grad
![[Pasted image 20250328110718.png]]

2. residual connection使用了没有经过GPU特定优化的运算算子, 这些算子会变慢.
    
3. etc
    

## 1.2 Overfit and Regularization

Regularization是神经网络训练中用于防止过拟合的重要技术, 常见的Regularization方法有:

1. **L1正则化（Lasso）**：向损失函数添加权重绝对值之和的惩罚项。这会导致稀疏的权重矩阵，有些权重被精确地设为零。
    
2. **L2正则化（Ridge/权重衰减）**：向损失函数添加权重平方和的惩罚项。这会使权重值变小但不会变为零。
    
3. **Dropout**：在训练过程中随机"丢弃"一部分神经元，使网络不过度依赖某些特征。
    
4. **早停（Early Stopping）**：当验证集上的性能开始下降时停止训练。
    
5. **数据增强（Data Augmentation）**：通过对训练数据进行变换来增加训练样本的多样性。
    
6. **Batch Normalization**：标准化每个mini-batch的输入，使网络更加稳定。
    

- Batch Norm: 对于(b,c,h,w), 它对b*h*w个数据进行统计分析, 形成c组统计量. 分通道的mini batch间计算.
    
- Layer Norm: 对于(b,c,h,w), 它对c*h*w个数据进行统计分析, 形成b组统计量. 完全的mini batch内计算.
    

7. **权重约束（Weight Constraints）**：对权重值的大小设置上限。


# 4. Hyperparameter adjustment
[望闻问切](https://www.zhihu.com/question/310816614)




