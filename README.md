# Overview

This lab introduces you to the Amazon Elastic Container Registry(AmazonECR)

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








