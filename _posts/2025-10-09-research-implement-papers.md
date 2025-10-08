---
layout: post
title: Research tips - implementing papers
subtitle:
categories: research
author: tangha1004
tags: [research]
---

[What makes some CS papers easier to implement than others?](https://www.quora.com/unanswered/What-makes-some-CS-papers-easier-to-implement-than-others)

# Answer 1
The following is my style of reading the CS research papers.

1. Download the relevant papers related to your work (Atleast 15 papers in your area)
2. Read only the abstract in the first stage (Write it into bullet points). Don't read anything beyond the abstract (in this stage)
3. Do this for all the 15 papers that you have in that area of domain.
4. Once done , read the entire points that you have noted down. (You will definitely come to an idea of what each paper is talking about). You may get a new idea also from the points you have noted. (It really works!!!!)
5. Some of the points might not have any connectivity with the others (so discard those papers). Rest of these, you can catch hold of some.
6. Read those papers that draws your attention and follow.
7. Read the literature of those papers (as this will help you in identifying the other papers that you have missed in that domain..)
8. You need to understand the mathematics behind any models (without knowing markov models, you can’t understand Markov chain or Markov process, etc) . Read a book to know the basic of these models.
9. Have a note book or note taking software with you to note down the points when you understand or read. (While reading the paper, you might understand, but after a day or two you will forget… so use a pen and a paper to note down the points)…

# Answer 2

There is definitely no standard way but I would follow this path:

- Learn TensorFlow, get your hands on some basic tutorials, understanding clearly every single line of code written by you. Please don’t assume! I have seen students assuming operations in TensorFlow code and it just takes them in the wrong direction.
- Try searching for some repositories or implementations of the paper that you are thinking of implementing in TensorFlow. You might get the code in TensorFlow itself…Congrats! If not then you would get a mathematical structure towards implementing the paper. It would help you to a great extent.
- Once you are clear with the idea and the implementation that has been done, start writing your code in TensorFlow. Don’t forget to test the various sections of the code separately, like some sanity check experiments. It might be as silly as checking whether or not you are matrix multiplication and shapes of tensors are coming out to be as expected by you.
- Once done, replicate the results published in the paper. If they are almost same you are through. 

Else, check your implementation or contact the authors!
Hope it helps!

Cheers

# Answer 3

- What are some must-implement deep learning papers that every DL researcher should implement?
- Hmm interesting question, thanks for the A2A! It’s generally non-trivial to re-implement an existing deep learning paper. So I’ll answer this question in a slightly different way by suggesting papers that I think every DL researcher ought to know (and understand!) to grok the fundamental ideas. Obviously this list is subjective and is reflective of my own background/thinking, so others will probably have a different list.

- “Reducing the Dimensionality of Data with Neural Networks” (https://www.cs.toronto.edu/~hinton/science.pdf) gives a nice high-level overview of how an auto-encoder works (implemented with a RBM). This paper is quite old and the actual model itself is not all that important, since most DL research has moved away from RBM. But this paper is still highly relevant for illustrating what a neural net is doing when modelling data, which is a pretty insightful read before diving into the more recent literature. In particular, it captures the main principles behind the idea of feature-based learning that is fundamental to deep learning.

- “ImageNet Classification with Deep Convolutional Neural Networks” (https://www.nvidia.cn/content/tesla/pdf/machine-learning/imagenet-classification-with-deep-convolutional-nn.pdf) is the OG-paper that jump-started the dominance of CNNs in computer-vision. Moreover, it reignited interest in neural net research after having been largely abandoned for a couple decades (Yann LeCun has some interesting stories of what it was like to be doing CNN research pre-2010s). On top of the historical relevance, it also illustrates why a feature-learning based approach is desirable for large scale AI problems.

- “A Neural Probabilistic Language Model” (http://www.jmlr.org/papers/volume3/bengio03a/bengio03a.pdf) is one of the older papers (2003?) that described how a neural net can be applied to the problem of language modelling. It was one of the first few papers that illustrated the notion of using a neural net to learn word-embeddings. Once you’ve read through this paper, you should have a pretty intuitive notion of how word-embeddings work and what sort of properties they capture.

- “Deep Sparse Rectifier Neural Networks” (http://proceedings.mlr.press/v15/glorot11a/glorot11a.pdf) is really nice for understanding what a ReLu activation function is doing when training deep networks and the problems it addresses. Moreover, it should give you a pretty good idea of when and when not to use ReLu activation functions.

- “Dropout: A Simple Way to Prevent Neural Networks from Overfitting” (http://www.jmlr.org/papers/volume15/srivastava14a.old/source/srivastava14a.pdf) is a highly relevant paper for understand what’s going on when training a network with dropout. Research on dropout-related methods has exploded since this paper was published, with some approaches superseding the approach described here in state-of-the-art systems. But its still important to understand this paper in order to connect all those other works together in your head and know how they all relate to one another.

# Answer 4

How can I become a deep learning and machine learning expert, so I can read any research paper in the field?


Whenever a question like this comes up, it usually indicates that someone wants the fruits without putting in the labor. All the best material on machine learning and deep learning (textbooks, research papers from ICLR/ICML/NIPS/JMLR, video lectures, data science competitions) as well as advice on how to consume it gently is there. But people wish to be experts by using some magic shortcuts that someone provides them on Quora. The world has no incentives to either create shallow experts or provide you any professional progress out of turn. Hence, some pain, frustration, helplessness, and sacrifice of other pursuits is going to be involved if you want to be an expert. Start with the Deep Learning textbook by Goodfellow et al or Murphy’s ML textbook. If things don’t make sense, fill in gaps using other prerequisite references in linear algebra, probability and statistical inference, and optimization. If you still don’t understand some part, post a question here on Quora and tag it with the machine learning topic. Bug me or other Ml quorans you trust to answer your queries. Understanding ML is not really that difficult once you are on the ML roller coaster. The correct and efficient implementation of algorithms and frameworks from scratch is the tricky part but most people don’t do that anyway.


# Answer 5
