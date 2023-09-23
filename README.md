# Cloud Native Monitoring Application on Kubernetes and AWS EKS

## Introduction

In the ever-evolving world of DevOps and cloud computing, the need for robust and scalable monitoring solutions is paramount. As applications grow more complex and distributed, having insights into their performance and resource utilization becomes essential. In this tutorial, we'll take you through the journey of creating a Cloud Native Monitoring Application using Flask, Docker, Kubernetes (K8s), and Amazon EKS.

## Prerequisites

Before diving into the project, here are the prerequisites:

- AWS Account.
- Programmatic access and AWS configured with CLI.
- Python3 Installed.
- Docker and Kubectl installed.
- Code editor (Vscode)

## Let’s Start the Project

### Part 1: Deploying the Flask application locally

**Step 1: Clone the code**

Start by cloning the project repository to your local machine.

       git clone <repository_url>

**Step 2: Install dependencies**

The application utilizes Python libraries like psutil, Flask, Plotly, and boto3. Install them using pip:
pip3 install -r requirements.txt

**Step 3: Run the application**

Navigate to the project's root directory and execute the following command:
python3 app.py
This will start the Flask server on localhost:5000. You can access the application by opening your browser and going to http://localhost:5000/.

## Part 2: Dockerizing the Flask application

**Step 1: Create a Dockerfile**

In the project's root directory, create a Dockerfile.

**Step 2: Build the Docker image**

To build the Docker image, execute the following command:
docker build -t <image_name> .

**Step 3: Run the Docker container**

Run the Docker container with the following command:
docker run -p 5000:5000 <image_name>

This will start the Flask server in a Docker container on localhost:5000. You can access the application the same way as before.

## Part 3: Pushing the Docker image to ECR

Push your Docker image to Amazon ECR. Make sure you have created an ECR repository and configured AWS CLI with appropriate credentials.

  Log in to your ECR registry (replace <repository_uri> and <region>)
 
   aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <repository_uri>

Tag your Docker image (replace <ecr_repo_uri> with your repository URI)
 
   docker tag <image_name> <ecr_repo_uri>:<tag>

Push the Docker image to ECR
 
 docker push <ecr_repo_uri>:<tag>


## Part 4: Creating an EKS cluster and deploying the app using kubectl

Create an EKS cluster using the AWS Management Console and deploy your app using kubectl. Be sure to configure your kubeconfig to connect to your EKS cluster.
**DONT FORGET TO CONFIGURE YOUR AWS ACCOUNT AT CLI USING AWSCLIV2. AND RUN COMMAND AWS CONFIGURE.**

Create and configure the cluster (Use AWS Management Console for cluster creation)
   aws eks --region <region> update-kubeconfig --name <cluster_name>

Deploy the app to the EKS cluster (Use kubectl)
   kubectl apply -f deployment.yaml

After applying the deployment YAML file, your application will be deployed on the EKS cluster. You can access it via the LoadBalancer's endpoint.

Congratulations! You've successfully created a Cloud Native Monitoring Application and deployed it on Kubernetes with AWS EKS. This application can be extended to monitor various resources and provide valuable insights into your cloud infrastructure. Explore further and enhance your DevOps skills! 🚀
