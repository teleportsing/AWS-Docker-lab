# Amazon ECR: Elastic Container Registry(Amazon ECR)

 By the end of this lab you will be able to

  * Create an Amazon ECR repository
  * Push an image to an Amazon ECR repository
  * Deploy an application using images stored on Amazon ECR


# Lab Prerequisites

 Some familiarity with Amazon EC2 Instances is useful . Previous knowledgeof Docker container technology or other Linux container technologies isdesirable


# Other AWS ServicesOther 

  AWS Services than the ones needed for this lab are disabled by LAMpolicy during your access time in this lab . In addition , the capabilities of theservices used in this lab are limited to what's required by the lab and insome cases are even further limited as an intentional aspect of the labdesign . Expect errors when accessing other services or performing actionsbeyond those provided in this lab guide


# Amazon Elastic Container RegistryAmazon 

 Elastic Container Registry ( Amazon ECR ) is a fully-managedDocker container registry that makes it easy for developers to store ,manage , and deploy Docker container images . Amazon ECR is integratedwith Amazon Elastic Container Service ( Amazon ECS ) , simplifying yourdevelopment to production workflow

 Amazon ECR eliminates the need to operate your own containerepositories or worry about scaling the underlying infrastructure . AmazonECR hosts your images in a highly available and scalable architectuallowing you to reliably deploy containers for your applications Integrationwith AWS ldentity and Access Management ( AM ) provides resource-levelcontrol of each repository


# Components of Amazon ECR 

Amazon ECR contains the following components

 Registry : An Amazon ECR registry is provided to each AWS account ; youcan create image repositories in your registry and store images in them

 Authorization token : Your Docker client needs to authenticate to AmazonECR registries as an AWS user before it can push and pull images . The AWSCLI get-login command provides you with authentication credentials topass to Docker .

 Repository : An Amazon ECR image repository contains your Docker images .

 Repository policy : You can control access to your repositories and the images within them with repository policies

 Image : You can push and pull Docker images to your repositories . You canuse these images locally on your development system , or you can use themAmazon ECS task definitions

# Components of Amazon ECS
Amazon ECS contains the following components

 Container Instance : An Amazon EC2 Instance that is running the AmazonCS agent and has been registered into a cluster

 Container : A Linux container that was created as part of a task

 Cluster : A logical grouping of container instances that you can place tasks on 

 Task Definition , Task : A description of an application that contains one ormore container definitions . A Task is a single instantiation of a TaskDefinitio

 Service : An Amazon ECS service allows you to run and maintain a specifiednumber of instances of a task definition simultaneous

 # Scheduling Amazon ECS tasks

 Amazon Elastic Container Service ( Amazon ECS ) is a shared state ,optimistic concurrency system that provides flexible scheduling capabilitiesfor your tasks and containers . The Amazon ECS schedulers leverage clusterstate information provided by the Amazon ECS API to make an appropriateplacement decision

 Amazon ECS provides the service scheduler for long running statelessservices and applications . The service scheduler ensures that the specifiednumber of tasks are constantly running and reschedules tasks when a taskfails ( for example , if the underlying container instance fails for somereason ) . The service scheduler optionally also makes sure that tasks areregistered against an Elastic Load Balancing load balancer

 You can update your services that are maintained by the services schedulesuch as deploying a new task definition , or changing the running number ofdesired tasks


 # Service definition parameters

 A service definition defines which task definition to use with your service ,how many instantiations of that task to run , and which load balancers ( ifany ) to associate with your tasks

 Service load balancing

 Your Amazon ECS service can optionally be configured to use Elastic LoadBalancing to manage traffic

# Task 1 : Create an Amazon ECR Repositoryn this task , you will create an Elastic Container Registry Repository .

In this task , you will create an Elastic Container Registry Repository .


 3. At the top of the AWS Management Console , to the right of Services , in the search bar search for ECS and then choose Elastic Container Service from the list

 4. In the left navigation pane , choose Repositories

 5. Choose Create repository

 6. For Repository name , type: myrepo

 7. Choose Create repository








