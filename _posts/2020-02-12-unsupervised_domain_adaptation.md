---
toc: true
layout: post
description: A Briefy Survey of the Latest in Unsupervised Domain adapatation
categories: [markdown]
title: An Example Markdown Post
---

# A Briefy Survey of the Latest in Unsupervised Domain adapatation

## Detialed notes on some of the papers survey can be found [here](_2020-02-17-multisource_distilling_DA.md)


Most commonly cited papers in the literature: 
-

[[1702.05464] Adversarial Discriminative Domain Adaptation](https://arxiv.org/abs/1702.05464)

[[1607.03516] Deep Reconstruction-Classification Networks for Unsupervised Domain Adaptation](https://arxiv.org/abs/1607.03516)

[[1809.02176] Multi-Adversarial Domain Adaptation](https://arxiv.org/abs/1809.02176)


Latest Papers from AAAI Conference: 
-

[Multi-source Distilling Domain Adaptation](_2020-02-17-multisource_distilling_DA.md)

[Domain Generalization Using a Mixture of Multiple Latent Domains](_2020-02-17-multisource_distilling_DA.md)

[Adversarial Domain Adaptation with Domain Mixup](_2020-02-17-multisource_distilling_DA.md)

[[2001.01046] Adversarial-Learned Loss for Domain Adaptation](https://arxiv.org/abs/2001.01046)

Other Papers: 
-

[Unsupervised Multi-Target Domain Adaptation: An Information Theoretic Approach](_2020-02-17-multisource_distilling_DA.md)


[[1801.07593] Mitigating Unwanted Biases with Adversarial Learning](https://arxiv.org/abs/1801.07593)
This paper attempts to define the different types of biases that can occur and then tries to reduce it using adverserial techinques. The work is shown on both text and tabular data. Results show good outputs without dependence on the bias variable. 

[High-performance medicine: the convergence of human and artificial intelligence \| Nature Medicine](https://www.nature.com/articles/s41591-018-0300-7)

A nice review paper on the overall state of ai in medicine. Nothing in particular related to domain adaptation mentioned although it is a review paper I am sure one of teh many papers cited would have done some bit of it. 


[International evaluation of an AI system for breast cancer screening \| Nature](https://www.nature.com/articles/s41586-019-1799-6)


[[1809.07294] Generative Adversarial Network in Medical Imaging: A Review](https://arxiv.org/abs/1809.07294)
A nice review of gans again not really specifically on domain adapatation. 


[IJCAI 2018: Unsupervised Cross-Modality Domain Adaptation of ConvNets for Biomedical Image Segmentations with Adversarial Loss](https://www.ijcai.org/Proceedings/2018/0096.pdf)

Idea is to do a cross domain segmentation using ct and mris. The network is posed as a domain adapatation problem with a adverserarial part. Idea here is to reduce the variances in the feature space between the source and the target dataset since the final task is the same, i.e. whole heart segemntation. This is acheived by having a seperate module trained for the target feature generator part (they call it DAM (domain adapatation module)) alond with a domain critic module (DCM) which uses the wasserstein distance to quanitfy the feature space differences between the MRI and the CT. 

only feature space alignment with a few layers. only works on the same modality of the body parts does not or will not probabaly work if the source and the target datasets are acquired differently. 
