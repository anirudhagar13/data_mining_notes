# Artificial Neural Networks
- 1950-60s 1st Wave
- 1980-95s 2nd Wave
- 2000-present current Wave
- All other issues of data mining concern ANNs also

## Basic Idea:
- World War II (how to mimic human brain)
- *A complex non-linear function can be learnt as a composition of simple processing units*
- If an arbitrarily complex non-linear function can be learnt, all classification problems can be solved
- Neurons (simple processing units) are connected with edges: ANNs
- Weights of edges determine strength of connections b/w neurons

## Simplest architecture:
- Perceptron (single neuron) was the first generation
- Weighted sum of input + Bias (is learnt)
- y = sign(w^T * x) (sign is the activation function here)
- If sign(w^T * x) > 0; y = 1 | else y = -1
- Other activation function replaced here in case of logistic regression is **sigmoid**
- Learns *linear decision boundaries*
- It is treated as a *Black Box* as it is not interpretable

## Perceptron learning:
- Start with random weights
- Start a loop:
	- For each training example; compute y^
	- Update weights as: w_{k+1} = w_k + lambda(y^ - y_{k})x_{ij}
- Until stopping criteria is met (all samples are classified)
- Intuition if error is positive (y^ - y_{k}); error must be increased; else decreased

## Findings:
- If algorithm converges, then it works (weights are learnt without being programmed or computed)
- If there is a linear solution, it would be found by this algorithm
- People thought that they were able to built ANNs
- Logistic regression & Linear SVM are far more powerful than perceptron
	- Linear SVM would find separator with high margin, perceptron would high any one of separators
- Non-linearly separable problems **The XOR Problem (y = x1 XOR x2)**
- Lead to death of 1st gen of Neural Networks

## Multi-layer Neural Networks:
- 2 layered (one hidden + one output) - Feed forward Neural Networks
- These would be able to solve any type of classification tasks, including non-linear boundaries
- This would be able to solve XOR problem

## Why we need multi-layers:
- Hidden layers are: abstraction of features
- Complex features are formed from composition of simpler features
- Arbitrarily complex non-linear functions could be learnt by composition of simpler functions
- Activation function (Linear predictor) where Linear predictor = Sum(W.x) + b

## Learning algorithm for Multi-layer:
- Perceptron learning would not work here
- Problem: How to determine true values of hidden nodes - People stopped working on AI **<--- right here***

## Gradient Descent:
- Happened in the Mid 80s 
- Invented in 70s, but reinvented in 1985 by a group: 
- Error term would be a function of weights in the network (depends on weight of network)
- If error is differentiable function of weights, what change in weights would cause error to move in the right direction
- **Major change:** Change of activation from step function *non-differentiable* to sigmoid function *differentiable*.
- For every weight; we can figure out which direction each weight should be moved by little bit, then on the whole we are going in the direction of lower error.
- Can be implemented through **Back-propagation** algorithm.

## Design issues with ANN:
- Research went on for 10 years to 95s
- How many nodes in the input layer: (boolean vs categorical input)
- What should be number of nodes in the output layer (depends on how many k-class problem we have)
- How many hidden layers and how many nodes in each hidden layer (if there are sufficiently many nodes, in even one single hidden layer: It can appx. learn arbitrarily complex non-linear function.)
	- What is more prone to overfitting (one hidden layer with many nodes vs multiple hidden layers with smaller number of nodes)
		- Fixed structure in multiple layers (like in CNN), then overfitting goes highly down
- What should be the initial weights and biases (better to make them random, each start would lead to different local minima (Can create ensembles of NN with diff. initializations))
- What should be the hyperparameters: Learning rate, number of epochs, mini-batch size etc.

## Characteristics of ANN in 2nd gen:
- Multi-layer ANN is Universal approximator, but is prone to overfitting
- Gradient Descent may converge to local minima
- Model building is very extensive, testing is fast (as per the compute at the time)
- Can handle irrelevant / redundant attributes (ANN paradigm has built-in feature) by assigning them lower weights
	- Many of the classifier algorithms have this except KNN, it cannot tell this built-in by themselves
- Sensitive to noise in training data
	- Can handle this by building complexity in the loss function
- Struggle with handling missing attributes
	- Unlike Naive Bayes
- Great advantage was automatic feature construction
- When SVMs came along in 95s, these became obsolete (as SVMs guaranteed global optima)
	- Kernel were required, not every kernel fits in every case
- Late 90s ensemble methods came along

## Deep learning (started late 90s)
- 2010s people realized that advancements were made by Geoffry Hinton, Yaan LeCun
- People figured out how to efficiently train **deep** neural networks
- Some advancements include:
	- Responsive activation Functions (e.g. From Step Function to Sigmoid and now RelU)
		- RelU prefered over Sigmoid to solve for problem of vanishing gradient in deep layers of neural networks
	- Bringing in notion of model complexity inside error time, Regularization (e.g. Dropout)
	- Millions times faster computing through GPUs
	- Larger labeled training datasets (e.g. ImageNet challenge one of the big drivers)
	- Specialized ANN architectures:
		- CNNs, RNNs, Residual Networks (with Skip Connections), GANs
	- Supervised Pre-training (Transfer learning from Image Net)
	- Unsupervised Pre-training (Auto-encoders)
	- Generative Models: Generate distributions of data (backbone of neural networks)


	
