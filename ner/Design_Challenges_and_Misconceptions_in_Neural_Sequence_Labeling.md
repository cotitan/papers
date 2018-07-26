## Design Challenges and Misconceptions in Neural SequenceLabeling
#### COLING 2018
### Motivation
当前用于序列标注的模型很多，要从所有的模型中，选择效果最好的模型，并不是一件简单的事情，不能只看F1值，因为各模型的实验条件不同，最终得到的F1也不是在同一实验环境下得到的，故对比性不强。具体不同点如下
1. Dataset
2. Preprocessing
3. Features
4. HyperParameters
5. Evaluation
6. Hardware Environment

### Solution
为了解决上述问题，排除不同因素可能造成的影响，作者对比了12个模型（如下：
三行四列共12个模型）在三个benchmark (NER, POS, Chunking)上的表现。
|Char |Word LSTM+CRF|Word LSTM|Word CNN+CRF|Word CNN|
|------|------|------|------|------|
|No Char|||||
|Char LSTM|||||
|Char CNN|||||

### 本文实验参数配置
|Parameter|Value|Parameter|Value|
|------|------|------|------|
|char emb size|30|word emb size|100|
|char hiden|50|word hidden|200|
|CNN_window|3|word CNN layer|4|
|batch_size|10|dropout rate|0.5|
|L2-Reg |1e-8|lr decay|0.05|
|word LSTM lr|0.015|word CNN lr|0.005|
|word LSTM epochs|100|word CNN epochs|200|

### Conclusion
1. 字符级特征很重要
2. 加入字符级特征时，使用lstm还是cnn，几乎没差别。
3. LSTM模型在大多数情况下比CNN模型要好。
4. softmax和crf：在NER和trunking任务上，crf效果明显更好，在pos任务上，softmax效果更好。
5. 预训练词向量，相对初始化词向量，提升月约%，对比明显
6. BIOES比BIO效果更好
7. SGD比Adam,RMSProp等更好