## An overview!!
Hey there everyone.Its kalam here. Let me provide you guys with an overview of how to automate the process of integration and deployment.This repo contains code which can be used to build and deploy pods to kubernetes cluster automatically when changes are triggered into github repository.CI/CD flow is an important part of the devops process which makes your life much much easier.However when talking about the traditional devops part in the CD part, it becomes irritating and quite hectic when a person having access to the cluster makes changes to the configuration files(changing the number of pods or rs )imperatively using queries. The development team has to resolve it after noticing it which takes considerable amount of time and lot of input.But dont be sad,i have some good news too!ArgoCD is here to keep your repo in sync with the deployment target cluster and monitors changes to the maifest file to remain in the desired state.It also seperates the CI and CD components which is a plus point for increased security.It has several advantages which i cannot discuss here, anyways this code is for demonstrating the automated CI/CD flow which triggers the jenkins jobs to build container images and deploy in to cluster whenever changes are made to github repository(using webhooks).DevOps best practices are implemented using GitOps.For that you have to launch jekins on an EC2 instance as desktop version wont work with webhooks as you have to provide it with a URL. Create two jenkins pipeline jobs one for building the conatiner image and the other for updating the maifest(use the SYKA-13/kmaisfest repo for this part).Use Argo CD to sync the kmanifest repo with the kubernetes cluster deployed either on cloud or open source kubernetes.

## What this does?
This repo along with https://github.com/SYKA-13/kmanifest creates a Jenkins pipeline with GitOps to deploy code into a Kubernetes cluster. CI part is done via Jenkins and CD part via ArgoCD (GitOps).

## Jenkins installation
Jenkins is installed on EC2. Follow the instructions on https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/ . You can skip "Configure a Cloud" part for this demo. Please note some commands from this link might give errors, below are the workarounds:

1. If you get daemonize error while running the command `sudo yum install jenkins java-1.8.0-openjdk-devel -y` then , run the commands from the answer of https://stackoverflow.com/questions/68806741/how-to-fix-yum-update-of-jenkins

2. Install Docker on the EC2 after Jenkins is installed by following the instructions on https://serverfault.com/questions/836198/how-to-install-docker-on-aws-ec2-instance-with-ami-ce-ee-update

3. Run `sudo chmod 666 /var/run/docker.sock` on the EC2 after Docker is installed.

4. Install Git on the EC2 by running `sudo yum install git`

### Jenkins plugins

Install the following plugins for the demo.
- Amazon EC2 plugin (No need to set up Configure Cloud after)
- Docker plugin  
- Docker Pipeline
- GitHub Integration Plugin
- Parameterized trigger Plugin

## ArgoCD installation 

Install ArgoCD in your Kubernetes cluster following this link - https://argo-cd.readthedocs.io/en/stable/getting_started/


