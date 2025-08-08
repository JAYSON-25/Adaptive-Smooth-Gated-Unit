<font size="7">***ASGU: Adaptive Smooth Gated Unit***</font>

**About**

ASGU (Adaptive Smooth Gated Unit) is a novel deep learning activation function implemented in PyTorch, designed to enhance neural network performance and stability. It combines the smoothness of the sigmoid function, adaptive gating inspired by Swish, and flexible negative region handling akin to Leaky ReLU, with learnable parameters α and β. This package includes a PyTorch implementation and an example demonstrating its application on the MNIST dataset.
Note: This project is unrelated to other repositories named "ASGU" (e.g., AnarxismuS/ASGU), which focus on different domains. This ASGU is specifically a deep learning activation function.



**Comparison with Other Activation Functions**
ASGU distinguishes itself from other activation functions through:

ReLU: ReLU suffers from the dying neuron problem due to zero gradients for negative inputs. ASGU mitigates this with a learnable 
beta slope.

#Mathematical Definition
The ASGU activation function is defined as:

**f(x)=x⋅σ(αx)+βx⋅(1−σ(αx))**

Where:

x: Input to the neuron

σ(z): Standard sigmoid function

α: Learnable parameter controlling the steepness of the gating mechanism.

β: Learnable parameter for the slope in the negative region, with no constraints on its value. The sign and magnitude of β are determined during training.

This can be rewritten as:

**f(x)=x⋅[β+(1−β)⋅σ(αx)]**

**Behavior**
For large positive x, f(x)≈x (slope of 1)

For large negative x, f(x)≈βx (The slope is determined by the learned value of β.)

Near x=0, ASGU provides a smooth, nonlinear transition due to the sigmoid function.
Swish: Swish uses a fixed sigmoid-based gating mechanism. ASGU introduces learnable 
alpha and 
beta for fully adaptive behavior across layers and datasets.

Leaky ReLU: Leaky ReLU uses a fixed negative slope, whereas ASGU's 
beta is unconstrained, allowing it to dynamically adjust its behavior in the negative region (leaky, reflecting, or zero) based on the data.

**MNIST Comparison Experiment**
Experimental Setup
ASGU was evaluated on the MNIST dataset using a three-layer multilayer perceptron (MLP) with 500 hidden units per layer, implemented in PyTorch. The model was trained for 10 epochs with the Adam optimizer (learning rate: 0.001) and cross-entropy loss. The setup compared ASGU (with an unconstrained 
beta) against ReLU:

Dataset: MNIST (60,000 training, 10,000 test images).

Model: MLP with three hidden layers (784→500→500→500→10).

Training: Batch size of 100, shuffled training data.

Evaluation: Test loss and accuracy after 10 epochs.

**Results**

Training Loss: ASGU achieved lower training loss (0.0176) compared to ReLU (0.0219), indicating better optimization.

Test Accuracy: ASGU achieved 97.83% accuracy, slightly behind ReLU's 97.97% but comparable, with potential for improvement on more complex datasets.

Learned Parameters:

Layer 1: 
alpha=1.6729, 
beta=0.0058

Layer 2: 
alpha=1.6278, 
beta=0.0002

Layer 3: 
alpha=0.9881, 
beta=0.0170

Visualizations:

See examples/mnist_example.ipynb for the full experiment code.

**Future Improvements**
Parameter Initialization: Explore strategies for initializing 
alpha and 
beta to enhance convergence speed.

Regularization: Apply L1/L2 regularization or clamping to stabilize parameter learning.

Scalability: Test ASGU on deeper architectures (e.g., ResNet, Transformer) and larger datasets (e.g., CIFAR-100, ImageNet).

Theoretical Analysis: Investigate ASGU's convergence properties and gradient dynamics for deeper understanding.


**Example Usage**
https://colab.research.google.com/drive/1TKjoP1nPRG1IcpQRzKEMFVcrwA8Bu0K3?usp=sharing

**References**
Goodfellow, I., Bengio, Y., & Courville, A. (2016). Deep Learning. MIT Press.

Ramachandran, P., Zoph, B., & Le, Q. V. (2017). Searching for Activation Functions. arXiv preprint arXiv:1710.05941.

Maas, A. L., Hannun, A., & Ng, A. Y. (2013). Rectifier Nonlinearities Improve Neural Network Acoustic Models. ICML.

**License**
This project is licensed under the MIT License. See the LICENSE file for details.
