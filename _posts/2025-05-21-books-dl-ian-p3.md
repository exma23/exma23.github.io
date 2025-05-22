---
layout: post
title: Plantuml example
categories: example
tags: [plantuml]
---

# A; Skipping parts

1; Page 45 - 97

2; Page 156 -163

3; Page 176 - 223

4; Page 230 - 241

# B; Definitions in general

## I; Khái niệm

### 1; representation

- Page 3: of the data they are given.

⇒ dependence on representations is a general phenomenon that appears throughout computer science and even daily life.

- Trích xuất đặc trưng khác tiền xử lý dữ liệu
    - tiền xử lý dữ liệu: clean + fill in  + standardize
    - trích xuất đặc trưng → ResNet → học từ dữ liệu đầu vào thành các dữ liệu embedding khác

### 2; representation learning

- Page 4: discover not only the mapping from representation to output but also the representation itself.

⇒ For many tasks, it is difficult to know what features should be extracted. For example, suppose that we would like to write a program to detect cars in photographs. We know that cars have wheels, so we might like to use the presence of a wheel as a feature. Unfortunately, it is difficult to describe exactly what a wheel looks like in terms of pixel values. A wheel has a simple geometric shape but its image may be complicated by shadows falling on the wheel, the sun glaring off the metal parts of the wheel, the fender of the car or an object in the foreground obscuring part of the wheel, and so on.

⇒ Learned representations often result in much better performance than can be obtained with hand-designed representations.

⇒ representation learning algorithm can discover a good set of features for a simple task in minutes, or a complex task in hours to months.

### 3; autoencoder

- Page 4: example of a representation learning algorithm

⇒ combination of an encoder function that converts the input data into a different representation, and a decoder function that converts the new representation back into the original format.

⇒ Autoencoders are trained to preserve as much information as possible when an input is run through the encoder and then the decoder, but are also trained to make the new representation have various nice properties. Different kinds of autoencoders aim to achieve different kinds of properties.

### 4; factors of variation

- Page 4: usually to separate the factors of variation that explain the observed data.

⇒ they may exist either as unobserved objects or unobserved forces in the physical world that affect observable quantities. They may also exist as constructs in the human mind that provide useful simplifying explanations or inferred causes of the observed data.

⇒ a speech recording, the factors of variation include the speaker’s age, their sex, their accent and the words that they are speaking. When analyzing an image of a car, the factors of variation include the position of the car, its color, and the angle and brightness of the sun

⇒ disentangle: require us to disentangle the factors of variation and discard the ones that we do not care about.

### 5; multilayer perceptron

- Page 5: A function is formed by composing many simpler functions. We can think of each application of a different mathematical function as providing a new representation of the input.
    
    ⇒ deep learning solves the problem of disentangle by: combining simpler concepts, such as corners and contours, which are in turn defined in terms of edges.
    
- Another perspective on deep learning is that depth allows the computer to learn a multi-step computer program.
    
    ⇒ Sequential instructions offer great power because later instructions can refer back to the results of earlier instructions.
    
- visible layer: contains the variables that we are able to observe
- hidden: because their values are not given in the data; instead the model must determine which concepts are useful for explaining the relationships in the observed data.

### 6; ways of measuring the depth of a model.

- first: based on the number of sequential instructions that must be executed to evaluate
the architecture ⇒ length of the longest path through a flow chart that describes how to compute each of the model’s outputs given its inputs.
    - Just as two equivalent computer programs will have different lengths depending on which language the program is written in, the same function may be drawn as a flowchart with different depths depending on which functions we allow to be used as individual steps in the flowchart.
- second: deep probabilistic models ***(probabilistic modeling graph)***, regards the depth of a model as being not the depth of the computational graph but the depth of the graph describing how concepts are related to each other. In this case, the depthof the flowchart of the computations needed to compute the representation of each concept may be much deeper than the graph of the concepts themselves.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/868b16a0-9d12-41c0-8f35-2e8b284f6c65/Untitled.png)

### 7; hypothesis space

- page 112: the set of functions that the learning algorithm is allowed to select as being the solution. For example, the linear regression algorithm has the set of all linear functions of its input as its hypothesis space

### 8; Bagging

- page 256: bootstrap aggregating is a technique for reducing generalization error by combining several models

### 8; Ensemble methods

- page 256
    - VD: model averaging

### 9; Adversarial training (read ASAP)

- page 268: training on adversarially perturbed examples from the training set

### 10; Tangent Distance, Tangent Prop, and Manifold Tangent Classifier

### 11; Denoise autoencoder

- page: 512, 691

### 12; Denoising score matching

- page: 621

### 13; latent space

- a latent feature space or embedding space, is an embedding of a set of items within a manifold in which items resembling each other are positioned closer to one another.

### 14; latent variables

- mixture distribution: a mixture distribution is made up of several component distributions. On each trial, the choice of which component distribution generates the sample is determined by sampling a component identity from a multinoulli distribution

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/2d064122-c8a6-43b0-9ada-b0498eca510b/Untitled.png)

- ***Latent variable:*** a random variable that we cannot observe directly. The component identity variable c of the mixture model provides an example. Latent variables may be related to x through the joint distribution, in this case, P(x, c) = P(x | c) P(c). The distribution P (c) over the latent variable and the distribution P(x | c) relating the latent variables to the visible variables determines the shape of the distribution P (x) even though it is possible to describe P(x) without reference to the latent variable.

### 15.1; transfer learning

### 15.2; domain adaption

### 15.3; multitask learning

### 16; zero-shot learning and one-shot learning

# C; Fundamental mathematics

## I; Linear algerba

### 1; Tensors

In some cases we will need an array with more than two axes.

### 2; Span

of a set of vectors is the set of all points obtainable by linear combination of the original vectors.

Determining whether Ax = b has a solution thus amounts to testing whether b is in the span of the columns of A. This particular span is known as the column space or the range of A

### 3; Norms

measure the size of vectors using a function called a norm.

### 4; Eigendecomposition

⇒ an integer by decomposing it into prime factors, we can also decompose matrices in ways that show us information about their functional properties that is not obvious from the representation of the matrix as an array of elements.

⇒ decompose a matrix into a set of eigenvectors and eigenvalues. An eigenvector of a square matrix A is a non-zero vector v such that multiplication by A alters only the scale of v: Av = λv.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/8d6d9318-6dd5-4234-86fb-8509deaa18be/Untitled.png)

- Not every matrix can be decomposed into eigenvalues and eigenvectors.
- decomposition exists, but may involve complex rather than real numbers.
    - real symmetric matrix can be decomposed into an expression using only real-valued eigenvectors and eigenvalues
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/ad505eee-ee09-4b66-bdec-34a61315a60c/Untitled.png)
    
- eigendecomposition may not be unique. If any two or more eigenvectors share the same eigenvalue, then any set of orthogonal vectors lying in their span are also eigenvectors with that eigenvalue, and we could equivalently choose a Q using those eigenvectors instead. By convention, we usually sort the entries of Λ in descending order. Under this convention, the eigendecomposition is unique only if all of the eigenvalues are unique.
- eigendecomposition ⇒ many useful facts about the matrix. The matrix is singular if and only if any of the eigenvalues are zero. The eigendecomposition of a real symmetric matrix can also be used to optimize quadratic expressions of the form f(x) = xT.A.x. Whenever x is equal to an eigenvector of A, f takes on the value of the corresponding eigenvalue
- A matrix whose eigenvalues are all positive is called positive definite.
    
    A matrix whose eigenvalues are all positive or zero-valued is called positive semidefinite.
    
    Likewise, if all eigenvalues are negative, the matrix is negative definite
    
    if all eigenvalues are negative or zero-valued, it is negative semidefinite. 
    
    ⇒ Positive semidefinite matrices are interesting because they guarantee that ∀x, xAx ≥ 0.
    ⇒ Positive definite matrices additionally guarantee that xAx = 0 ⇒ x = 0.
    

### **5; SVD**

- provides **another way to factorize a matrix**, into **singular vectors and singular values**
- page 44-45

### 6; PCA

- how to generate the optimal code point c∗ for each input point x. One way to do this is to minimize the distance between the input point x and its reconstruction, g( c∗). We can measure this distance using a norm. In the principal components algorithm, we use the L2 norm:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/742765ed-7675-4eda-afe6-79403d0e6952/Untitled.png)

# D; Regularization techniques

## I; Noise robustness

- Add noise to input
    - imposing a penalty on the norm of the weights
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/76c65672-c28a-4427-85c6-93207214c532/Untitled.png)
    
    - This form of regularization encourages the parameters to go to regions of parameter space where small perturbations of the weights have a relatively small influence on the output. In other words, it pushes the model into regions where the model is relatively insensitive to small variations in the weights, finding points that are not merely minima, but minima surrounded by flat regions.
- Add noise to hidden units
    - an important topic as to merit its own separate discussion; the dropout algorithm described in Sec. 7.12 is the main development of that approach
- Add noise to weights
    - This can be interpreted as a stochastic implementation of a Bayesian inference over the weights.
        - The Bayesian treatment of learning would consider the model weights to be uncertain and representable via a probability distribution that reflects this uncertainty.
    - Adding noise to the weights is a practical, stochastic way to reflect this uncertainty. This can also be interpreted as equivalent (under some assumptions) to a more traditional form of regularization.
    - Has been shown to be an effective regularization strategy in the context of recurrent neural
    networks
- Add noise to outputs

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c6ea46c5-8480-4f92-9aa2-5f7a90ec1326/44f6b157-d775-472a-9311-3e1c9bc4ee6e/Untitled.png)

## II; Multitask learning

(page 244 - 246)

## III; Parameter Tying and Parameter Sharing

(page 253 - 254)

## IV; Sparse Representations

(page 254-255)

## V; Bagging and Other Ensemble Methods






<!-- ## My First PlantUML

### PlantUML Block-1
@startuml
Bob -> Alice : hello
@enduml


### PlantUML Block-2
``` plantuml!
Bob -> Alice : hello world
```


### PlantUML Block-3
@startuml
(*) --> "Initialization"

if "Some Test" then
  -->[true] "Some Activity"
  --> "Another activity"
  -right-> (*)
else
  ->[false] "Something else"
  -->[Ending process] (*)
endif
@enduml


### PlantUML Block-4

@startuml
skinparam handwritten true

skinparam usecase {
  BackgroundColor DarkSeaGreen
  BorderColor DarkSlateGray

  BackgroundColor<< Main >> YellowGreen
  BorderColor<< Main >> YellowGreen

  ArrowColor Olive
  ActorBorderColor black
  ActorFontName Courier

  ActorBackgroundColor<< Human >> Gold
}

User << Human >>
:Main Database: as MySql << Application >>
(Start) << One Shot >>
(Use the application) as (Use) << Main >>

User -> (Start)
User --> (Use)

MySql --> (Use)

@enduml -->
