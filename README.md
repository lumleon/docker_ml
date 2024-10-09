# docker_ml

#Step-by-Step Guide to build Machine Learning model in docker

1. Set Up Your Environment
Before you start, make sure you have installed Docker on your machine. You can download it from the Official Docker Website.


2. Build Your Machine Learning Model
You need to have a trained machine-learning model ready to be deployed. For this tutorial, take an example in Python using scikit-learn.

 
3. Create a requirements.txt File.
List down all the Python dependencies that your app requires in this file. In this case:

requirements.txt:
scikit-learn
 

4. Create a Dockerfile
The Dockerfile is a script that contains a series of instructions used to build a Docker image.
Following is the simple dockerfile for our app. Make sure that the dockerfile is created with no extension, as it allows Docker to recognize it without requiring any additional arguments when building an image.

Dockerfile:

# Use a base image with Python
FROM python:3.11-slim

# Set the working directory in the container
WORKDIR /app

# Copy the necessary files into the container
COPY requirements.txt requirements.txt
COPY model.py model.py

# Install the required Python libraries
RUN pip install -r requirements.txt

# Run the Python script when the container starts
CMD ["python", "model.py"]
 

Now let’s understand what each of the keywords in the Dockerfile means.

FROM: It specifies the base image for our Dockerfile. We are using Python 3.11-slim in our case.
WORKDIR: It sets the working directory to the given path. After this, all commands will be executed relative to this directory.
COPY: This command copies the contents from your local machine to the Docker container. Here, it’s copying requirements.txt and model.py files.
RUN: It executes the command inside a shell (within the image's environment). Here, it is installing all the project dependencies listed in the requirements.txt file.
CMD: This command specifies the default command to run when the container starts. It is running a model.py script using Python in this case.
 

5. Build a Docker Image
Open your command prompt or terminal, navigate to the working directory where your Dockerfile is located, and run the following command.

docker build -t ml-model .
 

This command builds a docker image named ml-model using the current directory.

 

6. Run the Docker Container
Once the docker image is built, we are finally ready to run the container. Run the following command.

docker run ml-model
 

Following is the output:

Model trained and saved as model.pkl
Prediction for [5.1, 3.5, 1.4, 0.2]: 0
 

7. Tag & Push the Container to DockerHub
Docker Hub is a repository for Docker images, making it easy to share, version, and distribute containers across teams or production environments.

Create an account on Docker Hub. Once you have it, log in through the terminal by running the following command.

docker login
 

You have to tag the docker image with your username so that it will know where to push the image. Run the following command by replacing your username.

docker tag ml-model yourdockerhubusername/ml-model
 

Once the image has been tagged, you can push the image to the Docker hub by the following command.

docker push yourdockerhubusername/ml-model
 

Anyone can now pull and run your Docker image by:

docker pull yourdockerhubusername/ml-model
docker run yourdockerhubusername/ml-model
