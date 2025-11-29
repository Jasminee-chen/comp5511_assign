### comp5511 assignment2
### TASK3: LLM FOR NEURAL NETWORK

This task aims to explore and utilize Large Language Models (LLMs) to assist in the design, decision-making,
or analysis phases of a machine learning workflow, within the context of Task II (Image Denoising Neural Networks).

### 1. Task Goal

By consulting LLM, we obtained network architecture, loss function, and hyperparameter recommendations for the Fashion-MNIST image denoising task, 
and evaluated the impact of these recommendations on model performance (such as convergence speed and denoising quality). 
This task focuses on item 3 of Part B: hyperparameter recommendation, while LLM also provided additional architecture and loss function suggestions.
### 2. LLM Core Principle

The use of LLM in this task relies on its powerful natural language understanding and generation capabilities, 
as well as its internalization of massive amounts of literature and knowledge.

### 3.parameters
 -Recommended Loss Function：L1 Loss (MAE)

Recommended for image reconstruction. Compared to MSE Loss (Mean Squared Error), L1 Loss reduces blur and produces sharper edges.

 -Optimizer：Adam

Suitable for most deep learning tasks, with stable performance.

 -Learning Rate ($\alpha$)：$5 \times 10^{-4}$ to $1 \times 10^{-3}$

A reasonable initial range, requiring fine-tuning through experiments.

 -Batch Size：64 – 128

Balancing training speed and stability.

 -Training Epochs：10 – 30

Suggested training range; the final value should be determined in conjunction with the convergence curve.

 -Regularization (Weight Decay)：$1 \times 10^{-5}$

L2 regularization, recommended for enhancing the model's generalization ability and preventing overfitting.
#### 4. Setup and Dependencies
The project code runs in a Python environment based on the PyTorch framework.
- Python 3.8+：Core programming language
- Torch 2.0.0+：Core framework for neural networks (PyTorch)
- NumPy 1.26.0：Scientific computing and array manipulation
- Pandas 2.1.0：CSV data reading and processing
- Matplotlib 3.7.2：Visualization of the training process and display of denoised results
  
```bash
pip install torch torchvision numpy pandas matplotlib
```
