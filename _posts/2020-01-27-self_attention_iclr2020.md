---
toc: true
layout: post
description: On the Relationship between Self Attention and Convolutional Layers
categories: [markdown]
title: [REVIEW] On the Relationship between Self Attention and Convolutional Layers
---
#### Background: 
This paper banks on the concept of transformers and self attention both of which are foriegn to me. So i start out doing a brief review on what the two concepts are and then move onto what this paper does and how it uses them. 

Review of the [Illustrated Transformer Blog Post](http://jalammar.github.io/illustrated-transformer/). To start off with you need to first get an understanding of the attention mechanism in the Seq2Seq models starting [here](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/)

#### Key Ideas from the two blog posts on attention and transformers: 

#### Attention Mechanism: 
- The attention mechanism is the same concept as the attention that we think of in computer vision as heatmaps. In there the common practise is to use a grad-cam to backpropogate and weight the regions of the image which correspond to that class output. The same concept applies here as well. You use the idea of weighting the hidden layers of the encoder for every step of the decoder to highlight the importance. This is used along with the hidden layer of the decoder to predict the output of every step of the decoder. 

- One key difference in using attention networks versus classic seq-to-seq networks is the amount of information that gets passed onto the decoder. In classic case only the final Hidden State is passed to the decoder. Here all the hidden states are passed. 

- At each time step of the decoder, each of the hidden layers from the encoder is then weighted according to the scoring function (normalized) to give higher importance or attention to the relavent hidden state. 

- Further in transformers there is an attention mechanism in the encoder part as well 

- Note that the scoring is calculated at each time step of the decoder. 

This excellent illustration from Jay Alammar shows a gist of the seq2seq with attention. Plese refer to the [original blogpost](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/) for further details: 

<video width="100%" height="auto" loop autoplay controls>
   <source src="/images/attention_tensor_dance.mp4" type="video/mp4">
   Your browser does not support the video tag.
</video>

#### The transformer: 

- The transform is a different beast from what we have seen with the standard CNNs. It's also based on the attention mechanism but in a highly structured way. Compared to the earlier attention mechanism in the seq2seq work with attention, this one has three different parts **(Query, Key, Value)** to the self-attention mechanism. 

- The entire transformer network idea is to increase the number of self-attention heads and initialize them randomly so that you have enough different $$ W_Q, W_K, W_V $$ matrices trained to ensure that the words are propoerly attended to. 

- Further the decoder part of the network also has a similar attention mechanism to attend to the enconding output vectors. Unlike the original seq2seq with attention, here the network looks at the key and the value embeddings produced from the output of the final layer of the encoder. The weighting provided by the Query term of the decoder which only looks at the earlier positions of the output sequence is used to weight the attention for each decoder vector.   

- Two additional conceps of **residual connections** and **positional encodings** for the input vector embeddings are used to further enchance the network. Residual connections function similar to the residual blocks that are used in Resnets and DenseNets of computer vision, i.e. they reduce the problem of vanishing gradient which will affect such huge networks like the transformers. The positional encoding is an intersting idea. They way I think of it is to liken it to a method which helps spatially encoder the positioning. The original paper broke the two halves of the 512 vector embedding into sine and cosine based embedding vectors and then concatenated them.  

Additional Resource:
https://www.youtube.com/watch?v=rBCqOTEfxvg
http://nlp.seas.harvard.edu/2018/04/03/attention.html - A full step by step implementation of the paper with comments. 

----

#### Arxiv paper: [ON THE RELATIONSHIP BETWEEN SELF-ATTENTION AND CONVOLUTIONAL LAYERS](https://arxiv.org/abs/1911.03584) 
Blog post: http://jbcordonnier.com/posts/attention-cnn/

tl;dr: Self attention can express convolutional layer and the filters can be learnt in practise. The authors prove a theorem showing that with enough attention head, the self-attention can generalize the convolutional layer. I still haven't read the paper in detail but their blog post gave me enough of an idea to understand what the paper is doing 


#### Overall impression
Intersting take on correlating the attention head and cnns for images. The CNNs were originally designed to have limited to small fixed kernels which translated across the image to avoid having the whole image have differnt kernel weights. Now with the attention, it can attend to the whole image once again by posing it as an attention query problem. 

#### Key ideas
- Having multi head attention can generalize a CNN. Paper proves this theorem. 
- With multiple heads ensures that all areas of the imgage are attended to. 
- With positional encoding the problem of attention mechanism having equivariance is allieviated.
- Results on CFAIR show comparable performance to standard CNNs

#### Technical details
- Attention mechanism translated from 1D to images: Basically instead of having token length embeddings for every word every single pixel $$i,j$$ is assigned a key - value score. There is a bit of notation abuse in the paper wherin every $$A_p$$ and $$X_p$$ denotes a 2D index corresponding to the $$(x,y)$$ pixel position. 

#### Notes
- Questions and notes on how to improve/revise the current work  
   - Authors propose conditioning the receptive field on the input pixels 
   - Can this attention mechanism improve explainability. Can we better visualize what each region of the multiple heads are attending to for a given pixel or a region of pixels? 
   - Using transformers causes an explosion of paramters. And the main factor which is limiting it is the assumption that you take every pixel $$i,j$$ and attend to it. One simplification is to replicate what the embedding vector does in NLP. The same words would have the same embeddings. Maybe a simplification would be to have key-value pairs based on pixel intensity? Will the work out? 
  

I skimmed the proof because I really don't have any experience understanding what it is doing. 
