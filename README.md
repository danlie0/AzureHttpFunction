﻿# 1. helloworldAzureFunc

I have created a dockerised azure function. The function uses a HttpTrigger

## Deploy a local instance
On the server/machine you want to run  this, you'll first need a machine with docker installed, then grab the this source using git:

```
git clone git@github.com:Zaniar0/AzureHttpFunction.git

```
go inside the project directory and build the docker image

```
docker build --tag myfunctionimage:v1.0.0 .
```
You can upload the image to docker up by including your docker-id if you wish 


now verify that the image you built works by running the Docker image in a local container.

```
docker run -p 8080:80 -it myfunctionimage:v1.0.0
```



now browse to http://localhost:8080. you should see a home page saying "your function app 2.0 is now running"


## 2. sonarQube
I have deployed  a sonarQube server using the ARMtemplate

`
https://sonarqube-azureappservice725a.azurewebsites.net
`

I have created a project and key which will be used in the build pipeline.



## 3. function app 
The function app is hosted on Azure. There is a consumption app service plan with 3 slots, `dev`, `uat` and `nearlyprod`. 

## 4. the build pipeline
The pipeline is written in yaml. The key file to change is `azure-pipline.yml` if you want to change the build or release.

The yaml docalso includes the code for 
- building the function as a docker container
- uploading it to the azure container registry
- running sonarqube analysis
- publishing the results
- then finally deploying to azure functions app slots.

## 4. Deployment conditions
I have setup a deployment condition so that the one of the stages of the pipeline requries approval. 

![pipeline](img/2019-08-15-01-50-58.png)

## 6 Test the function app

Once your function app is deployed to Azure you can test it by going to the end point. For example ...

https://hellworldfunc.azurewebsites.net/api/MyHttpTrigger?code=3Tvmwo0D3bScNp1fQYA8RM8JNDF4AaXOTLHvd6rOH77jSFk/aM6L8A==&name=zaniar
