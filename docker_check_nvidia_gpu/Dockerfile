# Use an official PyTorch image as a parent image
FROM pytorch/pytorch:latest

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy the current directory contents into the container at /usr/src/app
COPY . .

# Install any needed packages specified in requirements.txt
# RUN pip install --no-cache-dir -r requirements.txt

# Run cuda_test.py when the container launches
CMD ["python3", "./cuda_test.py"]
