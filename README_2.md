## comp5511 assignment2
### Task2: NEURAL NETWORK FOR FASHION-MNIST
This project focuses on manually building a neural network using the PyTorch framework to solve the Fashion-MNIST image denoising problem.
### Neural Network Image Denoising
#### 1. Task Goal
Design and implement a neural network model manually to map images containing Gaussian noise (input) to corresponding clean images (labels) to achieve image denoising.
#### 2. Setup and Dependencies
The project code runs in a Python environment based on the PyTorch framework.
- Python 3.8+：Core programming language
- Torch 2.0.0+：Core framework for neural networks (PyTorch)
- NumPy 1.26.0：Scientific computing and array manipulation
- Pandas 2.1.0：CSV data reading and processing
- Matplotlib 3.7.2：Visualization of the training process and display of denoised results
  
```bash
pip install torch torchvision numpy pandas matplotlib
```
### 3.  Detailed Explanation of Neural Network Image Denoising

#### 3.1. Data Preprocessing and Loading

The code uses a custom `PairCsvDataset` class to process paired noisy and clean image data.

Data Alignment: `PairCsvDataset` reads `train_noisy.csv` and `train_clean.csv`, taking the noisy image as input $X$ and the corresponding clean image as label $Y$, ensuring each pair of data is correctly aligned.

Feature Normalization: The original pixel values ​​(0-255) are normalized to the range

$$0, 1$$

, which is standard practice for neural networks processing image data. This is achieved through the following operations:

X_{\text{norm}}, Y_{\text{norm}} = X / 255.0, Y / 255.0

Reshaping: Reshapes the one-dimensional pixel vector into a PyTorch tensor format [1, 28, 28], where 1 represents the number of channels (grayscale image).

Data Loader: A data loader is built using DataLoader, implementing batch processing (batch_size=128), data shuffling (shuffle=True), and multi-process loading (num_workers) to optimize training efficiency.

#### 3.2. Neural Network Architecture and Training

Network Architecture

A neural network is manually implemented in the code, with two main possible structural choices, both of which can be implemented as autoencoder structures:

Multilayer Perceptron (MLP) / Fully Connected Autoencoder:

Structure: Uses fully connected layers (nn.Linear). The input layer receives the flattened image vector ($28 × 28 = 784 neurons). Hidden layers contain multiple non-linear transformations, and the output layer re-outputs 784 neurons.

Example: $784 \to 512 \to 256 \to 512 \to 784$.

Convolutional Neural Network (CNN) / Convolutional Autoencoder:

Structure: Feature extraction (encoder) is performed using convolutional layers (nn.Conv2d), and image reconstruction (decoder) is performed using transposed convolutional layers (nn.ConvTranspose2d) or upsampling layers (nn.Upsample). This structure effectively preserves the spatial information of the image.

General Configuration: Hidden layers typically use **Rectified Linear Units (ReLU)** as the activation function; the output layer uses 784 neurons and may use a Sigmoid activation function (constraining the output to $[0, 1]$) or no activation function (directly regressing to normalized pixel values).

Loss Function and Training

Loss Function: Mean Square Error (MSE) loss (nn.MSELoss) is used, suitable for the regression task of denoising. It quantifies the average squared difference between the predicted pixel value $\hat{y}$ and the true pixel value $y$:

MSE = \frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2

Optimizer: An optimizer such as Adam or SGD is used.

Training Process: Iteration is performed for a specified number of epochs. In each batch, forward propagation is performed to calculate the loss, then backpropagation is used to calculate the gradient, and finally the network weights are updated using the optimizer.

Evaluation: During training, the MSE loss and the visualization of the denoising effect are periodically evaluated on the test set.
