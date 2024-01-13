# Use an official TensorFlow GPU runtime as a parent image
FROM tensorflow/tensorflow:latest-gpu

# Set the working directory in the container
WORKDIR /app

# Clone the RetinaNet repository
RUN git clone https://github.com/fizyr/keras-retinanet.git

# Enter the repository directory
WORKDIR /app/keras-retinanet

# Install the requirements
RUN pip install .

# Build the Cython modules
RUN python setup.py build_ext --inplace

# Create a directory for the dataset
RUN mkdir /app/dataset_retinanet

# Copy the dataset from Google Drive
COPY /content/drive/My\ Drive/dataset_retinanet/train.zip /app/dataset_retinanet
RUN unzip -u /app/dataset_retinanet/train.zip -d /app/dataset_retinanet

# Copy the modified CSV file
COPY modified.csv /app/keras-retinanet/modified.csv

# Copy the classes CSV file
COPY classes.csv /app/keras-retinanet/classes.csv

# Download the initial pretrained model from Fizyr
RUN wget https://github.com/fizyr/keras-retinanet/releases/download/0.5.1/resnet50_coco_best_v2.1.0.h5 -O /app/keras-retinanet/snapshots/_pretrained_model.h5

# Set the pretrained model path
ENV PRETRAINED_MODEL='/app/keras-retinanet/snapshots/_pretrained_model.h5'

# Train the RetinaNet model
CMD ["keras_retinanet/bin/train.py", "--freeze-backbone", "--random-transform", "--weights", "$PRETRAINED_MODEL", "--batch-size", "8", "--steps", "500", "--epochs", "8", "csv", "modified.csv", "classes.csv"]
