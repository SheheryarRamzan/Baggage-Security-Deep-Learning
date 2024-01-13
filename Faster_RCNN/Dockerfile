# Use an official PyTorch runtime as a parent image
FROM pytorch/pytorch:latest

# Set the working directory in the container
WORKDIR /app

# Clone the Faster R-CNN repository
RUN git clone https://github.com/sovit-123/fastercnn-pytorch-training-pipeline.git

# Enter the repository directory
WORKDIR /app/fastercnn-pytorch-training-pipeline

# Install the requirements
RUN pip install -r requirements.txt

# Download the dataset and unzip
RUN curl -L "https://universe.roboflow.com/ds/LCQNA858eV?key=dcGmfbKjWm" > roboflow.zip \
    && unzip roboflow.zip -d custom_data \
    && rm roboflow.zip

# Copy the custom dataset YAML file
COPY data_configs/custom_data_Project.yaml data_configs/custom_data_Project.yaml

# Training
RUN python train.py --data data_configs/custom_data_Project.yaml --epochs 5 --model fasterrcnn_resnet50_fpn_v2 --name custom_training --batch 8

# Expose any necessary ports
# EXPOSE 8080

# Define environment variable
# ENV NAME World

# Evaluation
CMD ["python", "eval.py", "--weights", "outputs/training/custom_training/best_model.pth", "--data", "data_configs/custom_data.yaml", "--model", "fasterrcnn_resnet50_fpn_v2", "--verbose"]
