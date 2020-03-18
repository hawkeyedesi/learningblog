---
toc: true
layout: post
description: Weight Agnostic Neural Networks
categories: [markdown]
title: An Example Markdown Post
---

# [REVIEW] Weight Agnostic Neural Networks

#### Resources
- **[Arxiv Paper](https://arxiv.org/abs/1906.04358)**
- **[Blogpost](https://weightagnostic.github.io/)**
- **[Slides](https://weightagnostic.github.io/slides/wann_slides.pdf)**
- **[Blog Github](https://github.com/weightagnostic/weightagnostic.github.io/issues)**
- **[Tutorial on MDL](https://arxiv.org/pdf/math/0406077.pdf)**

**Note: I am basing everything in these notes from the excellent blog post. I haven't gone through the paper yet.**

tl;dr: The paper introduces a method of designing neural network architectures that are not dependent on the node weights. Rather the trick here is to let the network evolve its architecture such that the architecture itself has the capacity required to solve the required tasks. The authors draw analogies with precocial animals such as snakes and iguanas wherein they are wired to run away from the prey. 

#### Overall impression
I think its a very cool concept in its nascent stages they have shown how without the burden of weight training, they employed a topology-based algorithm ([NEAT](http://www.cs.ucf.edu/~kstanley/neat.html)) to find and grow the topology. 

#### Key ideas
Quoting from the blog:
> While the aforementioned works focus on the information capacity required to represent the weights of predefined network architecture, in this work we focus on finding minimal architectures that can represent solutions to various tasks. 

- By making the network be independent of the weights or the tuning and solely depending on the architecture the work can use other algorithms besides gradient descent and backprop such as NEAT to solve the architecture 

- By weight sharing across the entire network with the weighting treated as a random sample from a uniform random distribution. 

- Introducing more than the common (e.g. linear, sigmoid, ReLU) and more exotic (Gaussian, sinusoid, step), the network is learning to include more of these connections. 

- By replacing the grunt work of the weights as filters, this work is now forcing the network connections to provide the right weighting or inductive biases for that particular problem.

- Further, instead of fixing the structure of the network and then biasing the weights of the network to solve a specific problem, you are instead relying on the network architecture structure. 

- By introducing nodes with a lot more sets of options such as inv, sin, cost gaussian, bias, etc (See paper and the code for details) you are replicating the functions a weight-based filter would do. That is a pretty cool concept. 

- Unlike NAS or other operations wherein you have to run the network every single time to compute a metric (for eg. accuracy) to see the performance, this proposed method instead just goes with random permutations of the network (I am assuming that's what the random trial paper does or some flavor of it). 


#### Technical details
- Not merely any weight agnostic neural network but one that can be described using a minimum descriptor length. 

- Significance of minimum description length models when choosing the weight agnostic NN: Using MDL inference, you are ensuring that the model that is being selected is the simplest one while still ensuring that it works just as well as the more complex network architectures. 

#### Notes
- Inductive Biases in Machine learning are a set of assumptions that the model learns to make during training to predict the unseen target data accurately. This [website](http://www.lauradhamilton.com/inductive-biases-various-machine-learning-algorithms) on inductive bias has a nice list of biases that are present for every task. 

- What is Minimum Description Length: MDL is an inference method that provides a generic solution to the model inference problem. The definition states that when you have different models that perform just as well, using MDL for model selection will ensure that you pick the simplest model that still performs as well as the more complex models. 

- Questions and notes on how to improve/revise the current work
  - How would it work for more complicated semi-supervised and supervised problems?
  - Are there more creative and interesting node functions to pick from that will help improve this? 
  - What happens if you start allowing more interesting connections such as skip connections in the feed-forward directions. Can you even do that and can it be optimized using the NEAT algorithm? 
  
#### Things I don't understand  
- What are the connection cost technique and I am not sure how it relates to the NEAT algorithm for model growing? 

- Further, how does dominance relations work to rank the networks based on mean overall performance, the weight values (how does it perform for the fixed selected weight. The paper chose a range between [-2,2]), max performance of the single best value and the number of connections in the network. 

- Does the domain relation ranking also consider the MDL inference internally and if so how? I still need to read those topics. 


