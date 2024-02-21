
# GPU-Accelerated Docker Environments for Windows using WSL2

## NVIDIA CUDA, WSL 2, and Docker Desktop Setup Guide

### Simple Terms : Asking my code to find my nvidia gpu if it exists and then perform a gpu model training which utilizes my GPU.


This guide provides detailed instructions for setting up NVIDIA CUDA on Windows, installing and configuring Windows Subsystem for Linux (WSL) 2, Docker Desktop for Windows, and running GPU-accelerated Docker containers. Additionally, it includes steps to clone and use the `docker_gpu` repository, which contains examples demonstrating NVIDIA GPU checks and a complete GPU use case within Docker.

## Prerequisites

- A Windows 10 or Windows 11 Pro/Enterprise system
- An NVIDIA GPU with the latest drivers installed

## Installation Steps

### 1. Install NVIDIA CUDA Toolkit for Windows

1. **Download the CUDA Toolkit**: Visit the [NVIDIA CUDA Toolkit website](https://developer.nvidia.com/cuda-downloads) and download the installer for Windows.
2. **Run the Installer**: Follow the on-screen instructions to install the CUDA Toolkit. Make sure to include the components you need, such as the CUDA compiler (`nvcc`), CUDA samples, and the necessary libraries.

### 2. Set Up Windows Subsystem for Linux (WSL) 2

1. **Enable WSL**: Open PowerShell as Administrator and execute:
   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   ```
2. **Enable Virtual Machine Platform**: Still in PowerShell, run:
   ```powershell
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```
3. **Set WSL 2 as Default**: Install the WSL 2 update from the Microsoft website, then set WSL 2 as the default version with:
   ```powershell
   wsl --set-default-version 2
   ```
4. **Install a Linux Distribution**: Choose a Linux distribution from the Microsoft Store (e.g., Ubuntu), install it, and set up a user account.

### 3. Install Docker Desktop for Windows

1. **Download Docker Desktop**: Go to the [Docker Hub](https://hub.docker.com/editions/community/docker-ce-desktop-windows/) and download Docker Desktop for Windows.
2. **Install Docker Desktop**: Run the installer and follow the prompts. Ensure the "WSL 2" feature is selected during installation.
3. **Configure Docker Settings**: After installation, open Docker Desktop settings, navigate to "General" and ensure "Use the WSL 2 based engine" is checked. In "Resources" > "WSL Integration", enable integration for your installed Linux distribution.

### 4. Clone the `docker_gpu` Repository

1. **Open WSL**: Launch your WSL terminal.
2. **Install Git** (if not already installed): For Ubuntu, use `sudo apt update && sudo apt install git`.
3. **Clone the Repository**:
   ```bash
   git clone https://github.com/Dheeraj-Bhaskaruni/docker_gpu.git
   ```
4. **Navigate to the Repository**:
   ```bash
   cd docker_gpu
   ```

### 5. Running the Docker Containers

#### docker_check_nvidia_gpu

This folder contains a `Dockerfile` and a Python script (`cuda_test.py`) to test the accessibility of CUDA within the Docker container.

1. **Build the Docker Image**:
   ```bash
   cd docker_check_nvidia_gpu
   docker build -t cuda-test .
   ```
2. **Run the Container**:
   ```bash
   docker run --gpus all cuda-test
   ```

#### docker_complete_gpu_use

This folder includes a `Dockerfile` and a Python script (`gpu_model_training.py`) for training a simple model using TensorFlow with GPU acceleration.

1. **Build the Docker Image**:
   ```bash
   cd docker_complete_gpu_use
   docker build -t tensorflow-gpu-test .
   ```
2. **Run the Container**:
   ```bash
   docker run --gpus all tensorflow-gpu-test
   ```

## Conclusion

This guide walks you through the setup required to leverage NVIDIA GPUs for computational tasks within Docker containers under Windows, using WSL 2. Following these instructions, you can run the provided examples to verify your setup and train a simple deep learning model with GPU acceleration.

## License

[MIT License](LICENSE)

## Acknowledgments

- NVIDIA for the CUDA Toolkit and GPU support
- The TensorFlow team for providing the machine learning library
- Docker for their container platform
