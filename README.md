# Deploying a Flask API to Kubernetes on AWS

This is the completed project for the course Server Deployment, Containerization, and Testing at **Udacity**.

In this project, I containerized and deployed a Flask API to a Kubernetes cluster using Docker, AWS EKS, CodePipeline, and CodeBuild.

The Flask app that was used for this project consists of a simple API with three endpoints:

- `GET '/'`: This is a simple health check, which returns the response 'Healthy'. As a test for automatic CodeBuild, the response was changed to "Healthy new commit"
- `POST '/auth'`: This takes a email and password as json arguments and returns a JWT based on a custom secret.
- `GET '/contents'`: This requires a valid JWT, and returns the un-encrpyted contents of that token. 

The app relies on a secret set as the environment variable `JWT_SECRET` to produce a JWT. The built-in Flask server was used for local development, but for production, I used the production-ready [Gunicorn](https://gunicorn.org/) server when deploying the app.



## Technologies used

* Docker Desktop - available <a href="https://docs.docker.com/install/" target="_blank">here</a>.
* Git: available <a href="https://git-scm.com/downloads" target="_blank">here</a> 
* Code editor: I used <a href="https://code.visualstudio.com/download" target="_blank">VS code</a>
* AWS Account: provided by Udacity through a sign-in token generated in the classroom
* Python: Version 3.10.4 was used. Check <a href="https://www.python.org/downloads/" target="_blank">here</a>
* Python package manager - PIP 22.0.2 was used which comes bundled with Python 3 >=3.4
* Terminal: Default terminal on Ubuntu 22.04 LTS was used
* Command line utilities:
  * AWS CLI was installed and configured using the `aws configure` command. Specifically, the region was set us-east-2
  * EKSCTL was installed using the instructions [available here](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html#installing-eksctl) or <a href="https://eksctl.io/introduction/#installation" target="_blank">here</a>
  * The KUBECTL was also installed following instructions [here](https://kubernetes.io/docs/tasks/tools/install-kubectl)


## Initial setup

1. I forked the repo at <a href="https://github.com/udacity/cd0157-Server-Deployment-and-Containerization" target="_blank">Server and Deployment Containerization Github repo</a> to my Github account.
2. I locally cloned the forked version to begin working on the project.
     
## Project Steps

Completing the project involved several steps:

1. Writing a Dockerfile for a simple Flask API
2. Building and testing the container locally
3. Creating an EKS cluster using Cloudformation template
4. Storing a secret using AWS Parameter Store
5. Creating a CodePipeline pipeline triggered by GitHub checkins
6. Creating a CodeBuild stage which will build, test, and deploy my code
7. Retrieving external IP for the deployed flask app
8. Incorporating an app test and testing the app for build-failure which test fails
