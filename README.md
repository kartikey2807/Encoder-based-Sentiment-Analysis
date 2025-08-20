# Encoder-based Sentiment Analysis
| [Dataset](https://www.kaggle.com/datasets/kazanova/sentiment140/data) | [Notebook 1](https://www.kaggle.com/code/kartikeysharmaah/1rt720-notebook-2) | [Notebook 2](https://www.kaggle.com/code/kartikeysharmaah/1tr720-notebook-3) | [model parameters](https://www.kaggle.com/models/kartikeysharmaah/bert-encoder-model) |

**Multi-head Self-attention**
* Idea is to **"attend to"** past and future tokens
* Compute the self-attention of each token as   
  $\implies sa[x_i] = \Sigma_{j=1}^{N}att[x_i,x_j]v_j$
* ***Query***: token that looks at other tokens
* ***Key***: the other 'looked at' tokens
* ***Value***: weights for each cross-attention term
* ***Attention***: Dot products between Keys and Queries
* ***Vector Form***   
  $\implies \text{SA} = \text{Softmax}(\frac{QK^T}{\sqrt{D_q}})V$   

![multi-headselfattention](https://miro.medium.com/max/469/1*GsLQLch51d7excmuAi4UzQ.png)

---
**Transformer (for Encoder)**
* Includes multi-head self-attention block
* passed through Layer norm
* passed through perceptron
* again passed through Layer norm
* Skip connection over self-attention and perceptron
* Positional encoding before passing to Encoder
<img src="https://heidloff.net/assets/img/2023/02/transformers.png" width="470px"/>

---
**Pre-training**
* Uses self-supervision
* **Mask certain tokens**
* Add *linear + softmax*
* Predict the masked tokens
* Expect the models to learn the syntax of a sentence
---

**Fine-tuning** for sentiment analysis
* add the \<cls\> tag
* apply BCE loss
* this tag captures the 'sentiment' of the overall tweet
---
**Results**
|Dataset|Accuracy|Binary Loss|
| :- | :- | :- |
|Training|77.36%|0.47|
|Validation|76.81%|0.48|
