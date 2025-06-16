## Encoder-based Sentiment Analysis
**Dataset**
* [Sentiment140 dataset with 1.4 million tweets](https://www.kaggle.com/datasets/kazanova/sentiment140/data)
* 0 - *negative*, 2 - *neutral*, 4 - *positive*
* Concerned columns: **target** and **text**
---
**Code**
* Kaggle Notebooks [here](https://www.kaggle.com/code/kartikeysharmaah/1rt720-notebook-2), [here](https://www.kaggle.com/code/kartikeysharmaah/1tr720-notebook-3)
* Download [model parameters](https://www.kaggle.com/models/kartikeysharmaah/bert-encoder-model)
* Download training and validation dataset, and tokens from [here](https://www.kaggle.com/datasets/kartikeysharmaah/twitter-text-dataset)
---
**Multi-head Self-attention**
* Idea is to 'look' at past and future tokens
* Compute "self-attention" from a token as   
  $\implies sa[x_j] = \Sigma_{i=1}^{N}att[x_i,x_j]v_j$
* attention is the dot product *keys* and *queries*
* Keys and queries are weighted sums of $x$
* Formula in vector form   
  $\implies \text{SA} = \text{Softmax}(\frac{QK^T}{\sqrt{D_q}})V^T$   
![multi-headselfattention](https://miro.medium.com/max/469/1*GsLQLch51d7excmuAi4UzQ.png)
---
**Transformer (for Encoder)**
* Includes multi-head self-attention block
* passed through Layer norm
* passed through perceptron
* again passed through Layer norm
* Residual connections over self-attention block and perception
* Add positional encoding before passing through the block   
  <img src="https://heidloff.net/assets/img/2023/02/transformers.png" width="470px"/>
---
**Pre-training**
* Uses self-supervision
* **Mask certain tokens**
* Add *linear + softmax*
* Predict the masked tokens
* Expect the model to learn the syntax of the sentence
---
**Fine-tuning** for sentiment analysis
* add the 'cls' tag
* create embeddings
* apply linear+sigmoid
* train the encoder model
* Idea: this tag captures the sense of the entire tweet
* get logits for 'cls' tag and apply binary loss
---
**Results**
|Dataset|Accuracy|Binary Loss|
| :- | :- | :- |
|Training|77.36%|0.47|
|Validation|76.81%|0.48|
