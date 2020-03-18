---
toc: true
layout: post
description: Differentiation of Blackbox Combinatorial Solvers
categories: [markdown]
title: [REVIEW] Differentiation of Blackbox Combinatorial Solvers
---
#### Arxiv Paper: [Differentiation of Blackbox Combinatorial Solvers](https://arxiv.org/abs/1912.02175)

tl;dr: This paper presents for the first time a method for combining deep learning as a rich feature generator along with a combinatorial optimizer. 
The innovative thing they show here is that by approximating the piecewise continuous outputs from a combinatorial optimizer to make it continuous we can backpropagate the gradients to also learn the feature representations of the deep learner. 
 
Also disclaimer: This is all that I understood from the blog post and haven't read the paper in detail.

#### Overall impression
I think it is a cool idea that you can present to the combinatorial optimization a set of learnable features for the problem using such a rich feature representer like deep learning while also solving complex combinatorial optimization. 


#### Key ideas
- Realize that by posing the combinatorial optimizer as one of the intermediate layers of the deep learner you can solve the problem along with optimizing the weights of the deep learner to improve the feature representation.
- By ensuring that the output of the combinatorial optimizer can be made continuous by maintaining the same minima and maxima, you can end up passing the gradients through the combinatorial optimizer to update the weights of the neural network. 
- Different from the other papers is the fact that does a smarter piecewise approximation.  
- They take existing combinatorial solvers and use it as a black box "Layer" for deep learning. 

#### Technical details
- I don't fully understand it. 

#### Notes
- Questions and notes on how to improve/revise the current work  

- How this work would apply to improve your current research or new research directions
  - What would happen if you had another 1D deep learning interpolator to improve the approximation of the piece-wise continuous function? How much dependent is the learner as a function of the optimizer? 


#### Extra resources: 
- https://towardsdatascience.com/the-fusion-of-deep-learning-and-combinatorics-4d0112a74fa7 
- Extra points to note
