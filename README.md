# Encoder-based Sentiment Analysis
| [Dataset](https://www.kaggle.com/datasets/kazanova/sentiment140/data) | [Notebook 1](https://www.kaggle.com/code/kartikeysharmaah/1rt720-notebook-2) | [Notebook 2](https://www.kaggle.com/code/kartikeysharmaah/1tr720-notebook-3) | [model parameters](https://www.kaggle.com/models/kartikeysharmaah/bert-encoder-model) |

**Multi-head Self-attention**
* Idea is to ***"look"*** at past and future tokens
* Compute "self-attention" from the token as   
  $\implies sa[x_i] = \Sigma_{j=1}^{N}att[x_i,x_j]v_j$
* *Queries*: How does this word attend to others?
* *Keys*: the other attended words
* *Values*: weights associated with self-attention term
* *Attention* is the dot product between key and queries
* Keys and queries are weighted sums of $x$
* Formula in vector form   
  $\implies \text{SA} = \text{Softmax}(\frac{QK^T}{\sqrt{D_q}})V$   
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
* add the \<cls\> tag
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
