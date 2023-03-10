# AR MNIST

AR MNIST (autoregressive MNIST) is a simple autoregressive model for compressing MNIST handwritten digits. The model is mostly intended as an educational tool to demonstrate the close relationship between machine learning and data compression.

<img src='./diagram.png'>

## Overview

Autoregressive models are statistical models which predict future data from past data. Most generally, they aim to approximate the distribution $p(x_n|x_1,\dots,x_{n-1})$ for some sample $x_1,\dots,x_n$. However using arbitrarily long contexts is usually impossible due to computational limitations. As such, most models operate on a fixed (or bounded) length context $x_{n-1-k},\dots,x_k$ where $k$ is the context (or history) length. Examples of autoregressive models include GPT3 and Facebook's Phrophet. Many autoregressive models are also generative models such that their predictions can be used recursively to sample from the approximate distribution $\hat p$.

To compress data using autoregressive models is rather straightforward. All that's needed is to entropy code the data using $\hat p$ as likelihood model. If the KL divergence between $\hat p$ and the true distribution $p$ is small, then this will result in very good compression. In the limit, this will result in **optimal**   compression, according to Shannon's source coding theorem. 

Hence, our aim will be to develop models which accurately approximate $p$ for images. Note that the value of pixel $x_n$ is not *entirely determined* by all previous pixel, so we shouldn't expect *any* autoregressive model to achieve perfect accuracy. Nonetheless, there's enough mutual information given from previous pixels to achieve considerable compression.
