---
toc: true
layout: post
description: Detailed notes on some of the domain Adapatation papers
categories: [markdown]
title: Domain Adaptaion/Generalization survey notes
---

# [Multi-source Distilling Domain Adaptation](../_pdfs/Multi-source_Distilling_Domain_Adaptation.pdf)

(https://arxiv.org/abs/1911.11554)

#### Overall impression
The key concept in this work is a method of trying to uniquely maintain the individual source representations while at the same time fine-tuning the target to one of the sources based on a metric and choosing a weighting automatically to pick those sources that best represent a particular target. 

The advantages the authors claim is that they are not rounding off the features of a particular learner and making it more and more homogeneous just to make it adapt to one another. 

Instead, they are all learned uniquely and then the target feature extractor is fine-tuned to make sure that you can figure out if they can match the closest of the source target that represents it. 

This method seems to show SOTA on some of the benchmark datasets for unsupervised domain adaptation. 


#### Key ideas
- Previous works treat the single source and single target unsupervised domain adaptation which is not the case in real-life scenarios. 
- Several of multiple source DA work have common issues: a. Treating all the sources equally, b. Eliminating the discriminative properties of the features to learn the domain invariant features, c. Treating each sample from the same source equally and not acknowledging the fact that the same source dataset also can have differences w.r.t to the targets, d. vanishing gradient problem of the discriminator when the target can perfectly distinguish between the source and the target feature representations. 
- Fix for each of the issues in the proposed work: 
	- **Eliminating the discriminative properties of the features to learn the domain invariant features**: Each source set is individually trained to maintain the unique set of features and the feature maps are then frozen to prevent fine-tuning by the discriminator during adversarial training. 
	- **Vanishing gradient problem of the discriminator when the target can perfectly distinguish between the source and the target feature representations**: Each source is fixed and then adversarially map the target feature against each of the source datasets using the Wasserstein distance metric. This prevents vanishing gradients even when the source and the target are non-overlapping.
	- **Treating each sample from the same source equally and not acknowledging the fact that the same source dataset also can have differences w.r.t to the targets:** The targets are all fine-tuned with the source datasets that are closest to the target. 
	- **Treating all the sources equally:** Weighting the output of each of the sources to ensure that the ones closest to the sources are chosen. 


#### Technical details
- Each source is first fine-tuned for classification. The feature generator is then fixed. 
- The target feature generator with each module is trained separately along with the discriminator which maximizes the Wasserstein distance. Not only does this help align the feature generators of the target domain to each source, but the min-max two-player game also optimizes to maximize the Wasserstein distance which will later be used as a weighting function for the outputs of the feature generators on the test set. 
- Fine-tuning is performed based on the discriminator output and the classifier is fine-tuned with these source images to better align with the target domain. 

#### Notes
- How does doing every discriminator with the individual target help? I think it's inefficient. Wouldn't doing it together actually improve the outcomes better. 
- Yes, they make a point of the domain generalization removing the discriminative features but then you can also probably still have a smarter sort of domain aggregation for each of the targets because this just feels very similar to the individual source to domain matching. The only thing that they are doing differently is using the Wasserstein distance in the discriminator to prevent mode collapse and then weighting and fine-tuning the individual source domain classifiers to make them work better with the target. 
-The authors claim that by individually training and then fine-tuning for the target leads to more optimal solutions. But then I am not clear on what would happen if you don't have a particular source that is nowhere close to the set of datasets shown. What kind of weighting would help there? 


---
# [Domain Generalization Using a Mixture of Multiple Latent Domains](../_pdfs/Domain_Generalization_Using_a_Mixture_of_Multiple_Latent_Domain.pdf)

(https://arxiv.org/abs/1911.07661)

#### Overall impression
This paper's premise is that you sometimes don't have the domain labels since the images are sometimes web-crawled. This paper proposes how to deal with it and claims that it beats the state of the art in the field as well including beating those that have the domain labels as well.

To do so they do an iterative clustering of the feature space and then slowly aggregate similar domains together assuming the features represent the domain that you are interested in the right way. 

They assume that the latent domain in the image is represented by the style therefore it uses the style features for clustering since that better represents the features and the latent domains in the different sources. 

Overall the key ideas are the use of style transfer to represent the feature clustering, a pseudo domain labelling using a k-means clustering, adverserial learning along with an entropy term to improve the overall domain generalization for the problem. 

#### Key ideas
- The domain during training does not always stay the same. For eg. When training on web-crawled data the domain within the training set itself varies. 
- The work hypothesis that there is a mixture of multiple latent domains and that domain generalization can be achieved by a combination of these latent domains. 
- To acheive this, the authors propose to automatically cluster the latent domains in the training set and the domain invariant features which are common amongst the different latent domain sets. 
- They hypothesize that the style features from the hidden layers of the neural network best represents the hidden latent domains and clustering on these style features would help best represet the different latent domains. 


#### Technical details
- Style transfer originally used the gram matrices of the neural activation on the different convolutional layers of the neural network to show the style of the image. 
- It has been shown theoertically that the gram matrices of the convolutional layer activations are equivalent to minimizing the maximum mean descripancy with a second order polynomial by constructing another style loss image matching the convolutional feature statistics(mean and standard deviation) between the style image and the generated image. 
- The authors claim that you are trying to extract domain invariant features by making the outputs domain invariant and doing that will actually diminsh the domain discriminative features. And using style transfer should be able to help distinguish better. 
- Clustering is done use a k-means clustering algorithm. Since they are pseudo labels and might change every single iteration, a Kuhn-munkres algorithm is used to maximize the rate of cluster assignments and the pseudo domain labels
- No significant(no t-test mind you) correlation between the number of pseudo labels assigned and the classification accuracy. (I assume it is to some extent true and if you dice it more and more it will affect the results). 
- Ablation studies show that pseudo domain labels match the original domain labels and they become stable as the training progresses. 
- Github code: https://github.com/mil-tokyo/dg_mmld/


#### Notes
- The literature survey shows several intersting past works which they claim all require domain labels and hence they are different. there are works in a. Using auto encoder architecture, b. adverserial learning, c. Meta learning methods ([MetaReg: Towards Domain Generalization using Meta-Regularization](http://papers.nips.cc/paper/7378-metareg-towards-domain-generalization-using-meta-regularization)), d. Domain aggregator methods (which is similar to their clustering idea) and e. Using self-supervised and semi supervisied learning ([Domain Generalization by Solving Jigsaw Puzzles](http://openaccess.thecvf.com/content_CVPR_2019/html/Carlucci_Domain_Generalization_by_Solving_Jigsaw_Puzzles_CVPR_2019_paper.html)) (which also does not require domain labels but assumes that the domains of the different labels are not mixed up and stay the same).  
- Entropy loss so that at the decision boundary of the adverserial learning to prevent ambigious features. (Intuitively why? I beleive it's because they're the ones which are similar across differnt domains. That would be expected right.) 




---
# [Adversarial Domain Adaptation with Domain Mixup](../_pdfs/Adversarial_Domain_Adaptation_with_Domain_Mixup.pdf)

(https://arxiv.org/abs/1912.01805)

tl;dr: Summary of the main idea.

#### Overall impression
Describe the overall impression of the paper. 

#### Key ideas
- Summaries of the key ideas

#### Technical details
- Summary of technical details

#### Notes
- Questions and notes on how to improve/revise the current work  
- How this work would apply to improve your current research or new research directions


--
# [Unsupervised Multi-Target Domain Adaptation: An Information Theoretic Approach](../_pdfs/Unsupervised_Multi-Target_Domain_Adaptation-An_Information_Theoretic_Approach.pdf)

(https://arxiv.org/abs/1810.11547)

tl;dr: Use information theoretic concepts to do a domain adaptation from a single source to multiple target domains with the unknown labels in the target domain. By posing the problem as an unsupervised domain adaptation which tries to jointly maximize the mutual information between domain labels and the private (domain-specific) features and minimize the mutual information between the domain labels and the shared (domain-invariant) features, the problem is posed as an encoder-decoder setup to overall predict the domain labels, the unknown class labels. Tested on standard domain adaptation datasets showing that they beat the SOTA. 
 

#### Overall impression
Describe the overall impression of the paper. 

#### Key ideas
- The problem focuses on unsupervised domain adaptation from a single source to multiple targets. 
- This work tackles the problem of multiple target domains with no labels and a single source domain with labels. The aim is to find an information-theoretic approach to do domain adaptation such that the model finds a shared domain while also accounting for the private domain-specific features. 


#### Technical details
- Posing the problem as a mutual information approach you break down the different information bits you want to optimize accordingly. 
- $$I(x;z)$$ - mutual information between the input and the latent space. Encourages the latent space both the $$z = [z_p, z_s] $$ to improve the value 
- $$I(y;z_s)$$ - mutual information which encourages output 
- Overall the problem is posed as an encoder-decoder architecture. Outputs being the reconstruction $$\hat x$$, domain d and the label classification c. 


#### Notes
- They say it is used to tackle a single known source and multiple unknown target domains. Can this be adapted to multiple sources with a known target? How would it need to be adapted? 
- Lots of information theory math behind why they are doing their setup but overall it seems like a simple enough encoder-decoder architecture setup in an information-theoretic framework. 
- I liked the fact that they explicitly try to say that there are two separate aspects to a given domain adaptation problem, i.e. the private and the shared domain information and a given network is forced to learn both of them. 