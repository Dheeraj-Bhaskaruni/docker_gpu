# Use the official TensorFlow image as the base image
FROM tensorflow/tensorflow:latest-gpu

# Set the working directory in the container
WORKDIR /app

# Copy the Python script into the container
COPY gpu_model_training.py /app

# Install any required packages (already handled by the base image in this case)

# Run the Python script when the container launches
CMD ["python3", "gpu_model_training.py"]
