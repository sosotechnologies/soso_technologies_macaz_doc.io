# KOPS
***Installing kOps***

```
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x ./kops
sudo mv ./kops /usr/local/bin/
```
***Install Python PiP***

```
sudo apt -y update
sudo apt install python3-pip
```

***Install AWSCli***

```
 sudo apt  install awscli -y
```

***Install Kubectl***

```
curl -Lo kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

***Create S3 Bucket***

```
aws s3 ls
aws s3 mb s3://soso-kops-bucket.local
```

***OPTIONAL***
```
aws s3api create-bucket \
    --bucket soso-kops-bucket \
    --region us-east-1 
```

***Add env variables in bashrc***

```
vi .bashrc

export NAME=soso-kops-bucket.k8s.local                               
export KOPS_STATE_STORE=s3://soso-kops-bucket.local 
 
source .bashrc
```

***Generate an sshkeys before creating cluster***

```
ssh-keygen
```

***Install Cluster preconfig file***

```
kops create cluster \
    --name=${NAME} \
    --cloud=aws \
    --zones=us-west-2a \
    --node-size t2.medium \
    --master-size t2.medium \
    --master-count 1 --node-size t2.medium --node-count=1
```

***Edit the cluster name- OPTIONAL***

```
kops edit cluster --name ${NAME}
```

***Install Cluster***

```
kops update cluster --name ${NAME} --yes --admin
```
**NOTE: WAIT 10 Mins before Checking Nodes and Validating cluster***

***Get nodes***

```
kubectl get nodes
```

***Validate Cluster***

```
kops validate cluster --wait 10m
```

***Delete cluster***

```
kops delete cluster --name ${NAME}
               [OR]
kops delete cluster --name ${NAME} --yes
```




To deploy EFS-EKS-using Terraform, [clone My repo](terraform-EFS-Dynamic)

You can clone and build this Documentation and use the image [mkdocs-docker-build](https://github.com/sosotechnologies/docs_docker_io)