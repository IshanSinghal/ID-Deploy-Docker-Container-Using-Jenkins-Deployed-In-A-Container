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
## Step 3 - Download docker images
```
#docker pull vimal13/apache-webserver-php
#docker pull python:alpine3.7
```
Please read https://www.wintellect.com/containerize-python-app-5-minutes/ for a better understanding of how to setup a python webapp in a docker container.


