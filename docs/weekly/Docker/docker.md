#  Install docker


## Sample use cases
5 Sample Build Deploy 
### 1. Docker and Mkdocs 
Build and deploy push Mkdocs to ECR/DockerHub
Clone this repo: [docs_docker_io](https://github.com/sosotechnologies/docs_docker_io.git)

***Install Docker***
```
sudo yum install docker -y
sudo systemctl status docker
sudo systemctl start docker
sudo systemctl enable docker
```
13. ### Build and Push Docker
```sudo docker build -t sosodocs .```

***Tag the sosodoc image***

```sudo docker tag sosodocs 088789840359.dkr.ecr.us-east-1.amazonaws.com/soso-repository:mkdocs-v1```

***Push image to repo***

```sudo docker push 088789840359.dkr.ecr.us-east-1.amazonaws.com/soso-repository:mkdocs-v1```

***Run the image with any one of the 2 commands, set yout ip:80***

```docker run -itd -p 80:80 --rm sosodocs```

```docker run -t -i -p 80:80 sosodocs```

And that is all, you should be able to navigate to http://127.0.0.1:80 and see the documentation website running.


***Optional BONUS!!!: DEPLOY TO AN EXISTING EKS CLUSTER***  

```
k expose deploy mkdocs --name=mkdocs-svc --port=80 --type=LoadBalancer --targetPort=80 --dry-run=client -o yaml > deploy.yaml
```

```
k expose deploy mkdocs --name=mkdocs-svc --port=80 --type=LoadBalancer --target-port=80 --dry-run=client -o yaml > service.yaml
```

***Optional***
Tag Your docker image with a version 

 ```sudo docker tag sosodocs sosodocs:v1```

Delete the existing running container, 26b43376e040 is mine, get yours.

```sudo docker rm 26b43376e040```    
           OR
```sudo docker rm 26b43376e040 --force```

Re-run the new versioned-image

 ```sudo docker run -itd -p 80:80 --rm sosodocs:v1```

To remove container or image:

```
docker rm [container]
docker rmi [image]
```