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

# Task 1 : Create an Amazon ECR Repositoryn this task , you will create an Elastic Container Registry Repository

In this task , you will create an Elastic Container Registry Repository .


 3. At the top of the AWS Management Console , to the right of Services , in the search bar search for ECS and then choose Elastic Container Service from the list

 4. In the left navigation pane , choose Repositories

 5. Choose `Create repository`

 6. For Repository name , type: myrepo

 7. Choose `Create repository`

 8. Copy your `Repository URI` to a text editor

✅ The `Repository` URL is as the top of the screen and will look like thefollowing952781235423.dkr.ecrus-west-2.amazonaws.com/myrepohe `Repository URI` Will be used later in the lab

 9. Choose the `myrepo` link

 10. In the left navigation pane , choose `Permissions`

 11. Choose `Edit`

 12. Choose `Add statement` to create a new permission statement

 13. For Statement name , type : `my_repository_statement`

 14. In the IAM entities section , search for `Ec2instancerole` andselect v Ec2instance Role

 15. In the `Actions` drop down , select all the displayed actions

 16. Choose `Save`

 This will save your repository statement
 
 
 # Task 2 : Pull , Tag and Push a Dockermage
 
 
 17. In the left navigation pane , copy the value `ofCommandhostsessionurl` , and paste it into a new tab
 
This will open a Session Manager windows into your instance
 
 18. Run this command to pull a Docker image from a publicepository
 
 `docker pull amazon/amazon-ecs-sample`

You will now tag your image so you can push it to the Amazon ECRrepository

 19. Copy this command into your Session manager window

`REPOSITORY=your-repository-uri` 

20. Replace your-repository-uri with the Repository URI that copiedearlier to your text editor

✅ The result should look similar to: 

```
REPOS/TORY = 285058481724 dkrecrus-west2.amazonas.com/myrepo
```

21. run the updated command


This command configures the `REPOSITORY` variable to point to your ECScluster

22. Run this command to tag your image so you can push it to theAmazon ECR repository

`docker tag amazon/amazon-ecs-sample:latest $REPOSITORY`


23. Copy and paste these command into your your Session Managerdol

```
aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin ACCOUNTID.dkr.ecr.us-west-2.amazonaws.com
```

24. Update `ACCOUNTID` with the value of ACCOUNTID located to the leftof these instructions

You should see the message : Login Succeeded .

25. Run this command to push the newly tagged image to yourAmazon ECR repository

`docker push $REPOSITORY`


# Task 3 : Create an Amazon ECSService with the New Image

26. At the top of the AWS Management Console , to the right of `Services` menu , in the search bar search for ECS and thenchoose Elastic Container Service from the list

27. the navigation pane on the left , choose Task Definitions

28. Choose `Create new Task Definition` then configure

  * Choose `EC2`
  * Choose `Next step`

29. Scroll to the bottom of the screen . then `chooseConfigure via JSON`

A Task Definition describes the components of your application , such asthe Docker containers to run , the resources they will use , and how theyk together . For this lab , you will use a sample template provided todisplay a simple web page

You can modify the parameters in the Task Definition ( for example , toprovide more CPU resources or change the port mappings ) to suit yourparticular applications


The Image parameter is the image to use for a container . This string ispassed directly to the Docker daemon . For this lab , youse theimage you pushed to Amazon ECR previously

The following task definition JSON file specifies one container that ispulled from an Amazon ECR repository

30. Delete the contents of the JSON editor panel

31. Copy and paste the task definition below into the JSON editorpane

```
{
  "family": "ecs-demo",
  "containerDefinitions": [
    {
      "volumesFrom": [],
      "memory": 128,
      "extraHosts": null,
      "dnsServers": null,
      "disableNetworking": null,
      "dnsSearchDomains": null,
      "portMappings": [
        {
          "hostPort": 80,
          "containerPort": 80,
          "protocol": "tcp"
        }
      ],
      "hostname": null,
      "essential": true,
      "entryPoint": null,
      "mountPoints": [],
      "name": "ecs-sample",
      "ulimits": null,
      "dockerSecurityOptions": null,
      "environment": [],
      "links": null,
      "workingDirectory": null,
      "readonlyRootFilesystem": null,
      "image": "YOUR-REPOSITORY-URI:latest",
      "command": null,
      "user": null,
      "dockerLabels": null,
      "logConfiguration": null,
      "cpu": 0,
      "privileged": null
    }
  ],
  "volumes": []
}
```
32. Replace `YOUR-REPOSITORY-URI` with your Repository URI ( Whichshould still be in your text editor

✅ The resulting line should look similar to：
 
  
 ```
 "mage": "268905983424.dkr.ecr.us-west2.amazonas.com/myrepo:latest",
 ```

33. Choose `Save`

The task definition is now раrsed тhe console shows the new taskdefinition registered in the `ecs-demo` family as defined in the son fe

34. Scroll to the bottom of the page , then choose `Create`

There may be more than one ecs-demo task definition present . Yourswill be the one with the highest revision numbe



# Task 4 : Create a Service

When you create an Amazon ECS service , you specify severalparameters that define what makes up your service and how it shouldbehave . These parameters create a service definition . Use the followingprocedure to create a service

35. In left navigation pane , below `Amazon ECS` , choose Clusters

36. Choose `ECSCuster>`.

37. On the `Services` tab , choose `Create` then configure

  * Launch type: `O EC2`
  * Service name: `MYSERVICENUMBER`
  * Replace NUMBER `with a random number`
  * Number of tasks: 1


This is the number of tasks you will launch and maintain on your cluster

38. Choose `Next step`

39. On `Step 2` , configure

  * Load balancer type: `O Network Load Balancer`
  * Service IAM role: `ecsServicerole`


40. Choose `Add to load balancer` then configure

41. Under `Service discovery (optional)` section , configure

   * Enable service discovery integration : 
   * ENamespace : Myprivatednsnamespace
 
42. Under DNS records for service discovery section , configure

  * TTL: 10 second(s)

43. Scroll to the bottom of the screen , then choose `Next step`

44. No Changes to `Set Auto Scaling(optional)`

45. On Step 3 , choose `Next step`

46. On Step 4 , Review the configuration and then choose `Create Service`

This will open the Launch Status page

47. On the Launch Status paqe choose View Service

48. Review the service you created

49. Choose the Tasks tab

Wait a few seconds and you will see the task you requested is beingcreated . You may need to choose refresh F for this to update


This task is running on the EC2 instances that were automaticallyprovisioned as part of the lab environment


50. Choose the Events tab

This will display the progress of the various tasks associated withyour service creation request . Choose refresh u until you see an eventdicating that your service has reached a steady state

If you now choose the Tasks tab you will see the tasks are all in thedesired Running state

51. Choose the Details tab

52. In the Details tab , choose your target group.

Your target group is named , my Targetgroup

The Target groups page is displayed

 
53. Select the check box for the my Targetgroup

54. Choose the Targets tab

In the `Targets` tab , you can see all of the registered targets
 
55. Choose the Details tab

56. Choose Myloadbalancer under the Load balancer

57. Select My Balancer and choose Description tab

58. Copy the DNS name of your load balancer to your clipboard

59. Open a new browser tab , then:

  * Paste the load balancer DNS name
  * Press Enter

# Conclusion

 Congratulations ! You now know how to:
 
 * Created an Amazon ECR repository
 * Push an image to an Amazon ECR repository
 * Deploy an application using images stored on Amazon ECR

 
 # Additional Resources
 
   * [Amazon Elastic Container Registry](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)
   * [Amazon Elastic Container Registry pricing](https://aws.amazon.com/ecr/pricing/)
