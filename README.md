# Problem Statement
```
1.	Create container image that has Jenkins installed using Dockerfile. When we launch this image, it should 
    automatically starts Jenkins service in the container.
2.	Create a chain of jobs using build pipeline plugin in Jenkins.
3.	Job 1(GetFiles): Pull the Github repo automatically when a developer pushes repo to Github.
4.	Job 2(Deploy): By looking at the code or program file, Jenkins should automatically start the respective
    language interpreter install image container to deploy code ( eg. If code is of PHP, then Jenkins should
    start the container that has PHP already installed ).
5.	Job 3(Test): Test your app if it is working or not. If the app is not working, then send email to developer
    with error messages.
6.	Job 4(Monitor): If container where app is running, fails due to any reason then this job should automatically
    start the container again.
```

## Step 1 - Create Dockerfile & run Jenkins
   ![Dockerfile Jenkins](/images/Jenkins_Dockerfile.jpg)
``` 
We install Jenkins on centos. RUN commands execute while building and CMD commands execute while starting container. 
We need to install JDK because jenkins runs on java.
We configure Jenkins to able to use sudo.
When server is run/created http and jenkins automatically starts.
```
```
#docker build -t jenkins:v1 .
#docker run -dit -P --name j1 jenkins:v1
```
## Step 2 - Jenkins Plugins needed and their config.
```
GitHub Plugin
SSH Plugin
Build Pipeline Plugin
Email Notification

Provide your HOST IP in SSH settings.
Configure smtp.
```
![Dockerfile Jenkins](/images/email_setup.jpeg)

## Step 3 - Download docker images
```
#docker pull vimal13/apache-webserver-php
#docker pull python:alpine3.7
```
Please read https://www.wintellect.com/containerize-python-app-5-minutes/ for a better understanding of how to setup a python webapp in a docker container.

## Job 1 - Get Files From GitHub
   ![Dockerfile Jenkins](/images/getfromgithub1.jpg)
```
Clone remote repo to its workspace
```

   ![Dockerfile Jenkins](/images/getfromgithub2.jpg)
```
Copy workspace folder to host os which we will later attach to production server.
```
   
## Job 2 - Identify and deploy type of container
   ![Dockerfile Jenkins](/images/deploy1.jpg)
   ![Dockerfile Jenkins](/images/deploy2.jpg)
``` 
    If files are of type HTML/PHP we will deploy apache webserver else a python server.
    First if checks if server is already running.
    Else second condition checks if the server has stopped and restart it.
    Else third condition deploys a new server, exposes it and attaches a volume containing the files to the server.
```

## Job 3 -  Testing and Email Notification
   ![Dockerfile Jenkins](/images/test1.jpg)
   ![Dockerfile Jenkins](/images/test2.jpg)
   
## Job 4 - Monitor
``` We will continuously monitor our server. If it goes down, Jenkins will restart it```

   ![Dockerfile Jenkins](/images/monitor1.jpg)
   ![Dockerfile Jenkins](/images/monitor2.jpg)
   
### Build pipeline is used for better visualization
   ![Dockerfile Jenkins](/images/Build_Pipeline.jpg)
   
## Future Updates:
   Make the process more intelligent by implementing it through Kubernetes.
   K8s will automactically handle monitoring and replication(auto-scaling).
