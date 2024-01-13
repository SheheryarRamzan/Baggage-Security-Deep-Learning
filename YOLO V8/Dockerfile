# Use an official PyTorch runtime as a parent image
FROM pytorch/pytorch:latest

# Set the working directory in the container
WORKDIR /app

# Install required dependencies
RUN pip install ultralytics

# Copy the YOLOv8 project files into the container
COPY . /app

# Download and unzip your model weights (adjust the path accordingly)
ADD https://www.example.com/path/to/your/model_weights.zip /app/model_weights.zip
RUN unzip /app/model_weights.zip -d /app

# Expose any necessary ports
# EXPOSE 8080

# Define environment variable
# ENV NAME World

# Run your application
CMD ["python", "yolov8_project.py"]
