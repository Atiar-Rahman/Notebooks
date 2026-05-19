

##### key components  of ANN
-  Input layer
-  hidden layer
-  output layer

##### Common activation functions in ANN
activation functions are important in neural networks because they introduce non linearity and helps the neural networks to learn complex patterns.
1. [****Sigmoid Function****](https://www.geeksforgeeks.org/machine-learning/derivative-of-the-sigmoid-function/)****:****  Outputs values between 0 and 1
2. [****ReLU (Rectified Linear Unit)****](https://www.geeksforgeeks.org/deep-learning/relu-activation-function-in-deep-learning/)****:****  A popular choice for hidden layers, it  returns the input if positive and zero otherwise
3. [****Tanh (Hyperbolic Tangent)****](https://www.geeksforgeeks.org/deep-learning/tanh-activation-in-neural-network/)****:**** Similar to sigmoid but output values between -1 and +1
4. [****Softmax****](https://www.geeksforgeeks.org/deep-learning/the-role-of-softmax-in-neural-networks-detailed-explanation-and-applications/)****:**** Converts raw outputs into probabilities used in the final layer of a network for multi-class classification
5. [****Leaky ReLU****](https://www.geeksforgeeks.org/machine-learning/Leaky-Relu-Activation-Function-in-Deep-Learning/)****:**** a variant of ReLU that allows small negative values for inputs helps in prventing "dead nurons" during training.

##### Types of ANN
1. **feedforward neural Network (FNN)**: [Feedforward Neural Networks](https://www.geeksforgeeks.org/nlp/feedforward-neural-network/) are one of the simplest types of ANNs. In this network, data flows in one direction from the input layer to the output layer, passing through one or more hidden layers. There are no loops or cycles means the data doesn’t return to any earlier layers. This type of network does not use backpropagation and is mainly used for basic classification and regression tasks.
##### Optimization algorithms in ANN training
optimization algorithms adjust the weights of a neural networks duing training to minimize errors. The goal is to make the networks predictions more accurate

1. **Gradient Descent:** Most basic optimization algorithm that updates weights by calculating the gradient of the loss function
2. Adam(Aditive Moment Estimation): An efficient version of gradient descent that adapts learning rates for each weight used in deep learning
3. RMSprop: A variation of gradient descent that adjusts the learning rate based on the average of recent gradients, it is useful in training recurrent neural networks (RNNs).
4. Stochastic Gradient Descent (SGD):Updates weights using one sample at a time helps in making it faster but more noisy.


##### applications of ANN
1. social media
2. marketing and sales
3. healthcare
4. personal assistants
5. customer supports
6. finance
##### challenges in artificial neural networks
1. Data dependency
2. computational power
3. overfitting
4. Interpretability
5. Training time

![Activation-functions-in-Neural-Networks](https://media.geeksforgeeks.org/wp-content/uploads/20250528125143444422/Activation-functions-in-Neural-Networks.webp)



##### Introducing Non linearity in Neural Network
Non-linearity means that the relationship between input and output is not a straight line. In simple terms the output does not change proportionally with the input. A common choice is the ReLU function defined as σ(x)=max⁡(0,x)σ(x)=max(0,x).

##### why is non-linearity important in neural networks
Neural networks consist of neurons that operate using weights, biases and activation functions.

In the learning process these weights and biases are updated based on the error produced at the output—a process known as backpropagation. Activation functions enable backpropagation by providing gradients that are essential for updating the weights and biases.

Without non-linearity even deep networks would be limited to solving only simple, linearly separable problems. Activation functions help neural networks to model highly complex data distributions and solve advanced deep learning tasks. Adding non-linear activation functions introduce flexibility and enable the network to learn more complex and abstract patterns from data.



### Mathematical Proof of Need of Non-Linearity in Neural Networks

To illustrate the need for non-linearity in neural networks with a specific example let's consider a network with two input nodes (i1and i2​), a single hidden layer containing neurons h1 and h2​  and an output neuron (out).

We will use w1,w2​ as weights connecting the inputs to the hidden neuron and w5​​ as the weight connecting the hidden neuron to the output. We'll also include biases (b1​​ for the hidden neuron and b2b2​ for the output neuron) to complete the model.

1. ****Input Layer****: Two inputs i1​ and i2​
2. ****Hidden Layer****: Two neuron h1 and h2
3. ****Output Layer****: One output neuron.

![NeuralNetwok](https://media.geeksforgeeks.org/wp-content/uploads/20240503121617/NeuralNetwok.png)

The input to the hidden neuron h1​ is calculated as a weighted sum of the inputs plus a bias:

h1=i1.w1+i2.w3+b1

h2=i1.w2+i2.w4+b2

The output neuron is then a weighted sum of the hidden neuron's output plus a bias:

output=h1.w5+h2.w6+bias

Here, h_1 , h_2 \text{ and output} are linear expressions.

In order to add non-linearity, we will be using sigmoid activation function in the output layer:

σ(x)=11+e−x

final output=σ(h1.w5+h2.w6+bias)

final output=1/1+e−(h1.w5+h2.w6+bias)

This gives the final output of the network after applying the sigmoid activation function in output layers, introducing the desired non-linearity.

##### Impact of activation functions on Model performance
The choice of activation function has a direct impact on the performance of a neural network in several ways:

1. ****Convergence Speed:**** Functions like ReLU allow faster training by avoiding the vanishing gradient problem while Sigmoid and Tanh can slow down convergence in deep networks.
2. ****Gradient Flow:**** Activation functions like ReLU ensure better gradient flow, helping deeper layers learn effectively. In contrast Sigmoid can lead to small gradients, hindering learning in deep layers.
3. ****Model Complexity:**** Activation functions like Softmax allow the model to handle complex multi-class problems, whereas simpler functions like ReLU or Leaky ReLU are used for basic layers.

### Backpropagation in Neural Networks
Back Propagation is also known as "Backward Propagation of Errors" is a method used to train neural network . Its goal is to reduce the difference between the model’s predicted output and the actual output by adjusting the weights and biases in the network.
![Backpropagation-in-Neural-Network-1](https://media.geeksforgeeks.org/wp-content/uploads/20250701163824448467/Backpropagation-in-Neural-Network-1.webp)

Back Propragation plays a critical role in how neural networks improve over time.
1.  Efficient Weights Update: It computes the gradient of the loss function with respect to each weight using the chain rule making it possible to update weights efficiently
2. Scalability: The back propagation algorithm scales well to networks with multiple layers and complex architectures making deep learning feasible.
3. Automated learning: with back propagation the learning process becomes automated and the model can adjust itself to optimize its performance.

##### Working of Back Propagation Algorithm

The Back Propagation algorithm involves two main steps: the ****Forward Pass**** and the ****Backward Pass****.

1. Forward pass work
	In ****forward pass**** the input data is fed into the input layer. These inputs combined with their respective weights are passed to hidden layers. For example in a network with two hidden layers (h1 and h2) the output from h1 serves as the input to h2. Before applying an activation function, a bias is added to the weighted inputs.
	![Backpropagation-in-Neural-Network-2](https://media.geeksforgeeks.org/wp-content/uploads/20250701163954688803/Backpropagation-in-Neural-Network-2.webp)
2. Backward pass
	 In the backward pass the error (the difference between the predicted and actual output) is propagated back through the network to adjust the weights and biases. One common method for error calculation is the [****Mean Squared Error (MSE)****](https://www.geeksforgeeks.org/maths/mean-squared-error/) given by:

	MSE=(Predicted Output−Actual Output)2

##### example of Back propagation in machine learning

![Backpropagation-in-Neural-Network-3](https://media.geeksforgeeks.org/wp-content/uploads/20250701164029130520/Backpropagation-in-Neural-Network-3.webp)


- apply forward propagation
- find output
- error calculate mse
	```
	If your **target output** is `0.5` and your **predicted output** is `0.3`, here's how you compute the **loss and error signal** for backpropagation.

---

## 🎯 Given:

- **Target** y=0.5
    
- **Prediction** y^=0.3
    

---

### 🧮 1. Loss Calculation

Assume **Binary Cross-Entropy Loss**:

L=−(ylog⁡(y^)+(1−y)log⁡(1−y^))

Substitute values:

L=−(0.5⋅log⁡(0.3)+0.5⋅log⁡(0.7))L = -\left( 0.5 \cdot \log(0.3) + 0.5 \cdot \log(0.7) \right) L≈−(0.5⋅(−1.204)+0.5⋅(−0.357))L \approx -\left( 0.5 \cdot (-1.204) + 0.5 \cdot (-0.357) \right) L≈−(−0.602−0.179)=0.781L \approx -\left( -0.602 - 0.179 \right) = 0.781

✅ **Loss ≈ 0.781**

---

### 🔁 2. Error for Backpropagation (Output Layer)

Assuming:

- Output activation is **Sigmoid**
    
- Using simplified gradient for cross-entropy + sigmoid:
    

δ=y^−y=0.3−0.5=−0.2\delta = \hat{y} - y = 0.3 - 0.5 = -0.2

✅ **Error signal (δ) = -0.2**

This δ\delta is used to compute gradients for the weights leading into the output neuron.

---

Would you like to walk through a full weight update example with these numbers?

# What is Perceptron | The Simplest Artificial neural network


## What is Perceptron?

****Perceptron**** is a type of [neural network](https://www.geeksforgeeks.org/machine-learning/neural-networks-a-beginners-guide/) that performs binary classification that maps input features to an output decision, usually classifying data into one of two categories, such as 0 or 1.
### Types of Perceptron

1. [****Single-Layer Perceptron****](https://www.geeksforgeeks.org/python/single-layer-perceptron-in-tensorflow/) is a type of perceptron is limited to learning linearly separable patterns. It is effective for tasks where the data can be divided into distinct categories through a straight line. While powerful in its simplicity, it struggles with more complex problems where the relationship between inputs and outputs is non-linear.
2. [****Multi-Layer Perceptron****](https://www.geeksforgeeks.org/deep-learning/multi-layer-perceptron-learning-in-tensorflow/) possess enhanced processing capabilities as they consist of two or more layers, adept at handling more complex patterns and relationships within the data.

## Basic Components of Perceptron

A Perceptron is composed of key components that work together to process information and make predictions.

- ****Input Features:**** The perceptron takes multiple input features, each representing a characteristic of the input data.
- [****Weights****](https://www.geeksforgeeks.org/deep-learning/the-role-of-weights-and-bias-in-neural-networks/)****:**** Each input feature is assigned a weight that determines its influence on the output. These weights are adjusted during training to find the optimal values.
- ****Summation Function:**** The perceptron calculates the weighted sum of its inputs, combining them with their respective weights.
- [****Activation Function****](https://www.geeksforgeeks.org/machine-learning/activation-functions-neural-networks/)****:**** The weighted sum is passed through the ****Heaviside step function****, comparing it to a threshold to produce a binary output (0 or 1).
- ****Output:**** The final output is determined by the activation function, often used for ****binary classification**** tasks.
- [****Bias****](https://www.geeksforgeeks.org/deep-learning/effect-of-bias-in-neural-network/)****:**** The bias term helps the perceptron make adjustments independent of the input, improving its flexibility in learning.
- ****Learning Algorithm:**** The perceptron adjusts its weights and bias using a learning algorithm, such as the Perceptron Learning Rule, to minimize prediction errors.

In a fully connected layer, also known as a dense layer, all neurons in one layer are connected to every neuron in the previous layer


# Single Layer Perceptron

It is one of the oldest and first introduced neural networks. It was proposed by ****Frank Rosenblatt**** in ****1958****. Perceptron is also known as an artificial neural network. Perceptron is mainly used to compute the [logical gate](https://www.geeksforgeeks.org/physics/logic-gates/) like ****AND, OR and NOR**** which has binary input and binary output.

The main functionality of the perceptron is:-

- Takes input from the input layer
- Weight them up and sum it up.
- Pass the sum to the nonlinear function to produce the output.


