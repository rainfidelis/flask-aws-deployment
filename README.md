# Deploying a Flask API

This is a mini project involving server deployment, containerization, and testing. 

The project's goal is to containerize and deploy a Flask API to a Kubernetes cluster using Docker, AWS EKS, CodePipeline, and CodeBuild.

The Flask app that will be used for this project consists of a simple API with three endpoints:

- `GET '/'`: This is a simple health check, which returns the response 'Healthy'. 
- `POST '/auth'`: This takes a email and password as json arguments and returns a JWT based on a custom secret.
- `GET '/contents'`: This requires a valid JWT, and returns the un-encrpyted contents of that token. 

The app relies on a secret set as the environment variable `JWT_SECRET` to produce a JWT and deployment is powered by the production-ready [Gunicorn](https://gunicorn.org/) server.



## Prerequisites

* Docker Desktop - Installation instructions for all OSes can be found <a href="https://docs.docker.com/install/" target="_blank">here</a>.
* Git: <a href="https://git-scm.com/downloads" target="_blank">Download and install Git</a> for your system. 
* Code editor: You can <a href="https://code.visualstudio.com/download" target="_blank">download and install VS code</a> here.
* AWS Account
* Python version between 3.7 and 3.9. Check the current version using:
```bash
#  Mac/Linux/Windows 
python --version
```
You can download a specific release version from <a href="https://www.python.org/downloads/" target="_blank">here</a>.

* Python package manager - PIP 19.x or higher. PIP is already installed in Python 3 >=3.4 downloaded from python.org . However, you can upgrade to a specific version, say 20.2.3, using the command:
```bash
#  Mac/Linux/Windows Check the current version
pip --version
# Mac/Linux
pip install --upgrade pip==20.2.3
# Windows
python -m pip install --upgrade pip==20.2.3
```
* Terminal
   * Mac/Linux users can use the default terminal.
   * Windows users can use either the GitBash terminal or WSL. 
* Command line utilities:
  * AWS CLI installed and configured using the `aws configure` command. Another important configuration is the region. Do not use the us-east-1 because the cluster creation may fails mostly in us-east-1. Let's change the default region to:
  ```bash
  aws configure set region us-east-2  
  ```
  Ensure to create all your resources in a single region. 
  * EKSCTL installed in your system. Follow the instructions [available here](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html#installing-eksctl) or <a href="https://eksctl.io/introduction/#installation" target="_blank">here</a> to download and install `eksctl` utility. 
  * The KUBECTL installed in your system. Installation instructions for kubectl can be found <a href="https://kubernetes.io/docs/tasks/tools/install-kubectl/" target="_blank">here</a>. 


## Initial setup

The following steps will help you to work with this project locally:

1. Fork the existing project repository.
2. Locally clone your forked version to begin working on the project.
```bash
git clone https://github.com/rainfidelis/aws-flask-deployment.git
cd aws-flask-deployment/
```
3. Remember to setup your local environment variables using the `env.example` sample file.
4. Finally, remember to configure the files marked below for your aws account:
```bash
.
????????? Dockerfile 
????????? README.md
????????? aws-auth-patch.yml #Edit
????????? buildspec.yml  #Edit
????????? ci-cd-codepipeline.cfn.yml  #Edit
????????? iam-role-policy.json  #Edit
????????? main.py
????????? requirements.txt
????????? simple_jwt_api.yml
????????? test_main.py #Edit
????????? trust.json   #Edit
```

     
## Project Steps

Completing the project involved the following steps:

1. Write a Dockerfile for a simple Flask API
2. Build and test the container locally
3. Create an EKS cluster
4. Store a secret using AWS Parameter Store
5. Create a CodePipeline pipeline triggered by GitHub checkins
6. Create a CodeBuild stage which will build, test, and deploy your code


## Authors and Contributors

This project was completed by myself, [Rainny Fidelis](https://github.com/rainfidelis), as the final project in the Udacity Full Stack Developer NanoDegree program. The starter files on which the project was built were provided by Udacity as part of the program.
