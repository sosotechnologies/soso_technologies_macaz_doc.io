# System Requirements

 Windows OS systems will be the preferred OS that will be used throughout 
 this program. Students with MaC OS can still use their MAC pcs, but may have 
 some diffuculties with running some Windows-specific commands.
  ## Installation links
### IAM-Role-EKS-authenticator
[IAM Auth link](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)
```
curl -o aws-iam-authenticator https://amazon-eks.s3.us-west-2.amazonaws.com/1.15.10/2020-02-22/bin/linux/amd64/aws-iam-authenticator
chmod +x ./aws-iam-authenticator
sudo mv ./aws-iam-authenticator /usr/local/bin
aws-iam-authenticator help
```
### install docker in ec2
[Docker installation link](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/create-container-image.html)


Before you can use [Giscus], you need to complete the following steps:

1.  __Install the [Giscus GitHub App]__ and grant access to the repository
    that should host comments as GitHub discussions. Note that this can be a
    repository different from your documentation.
2.  __Visit [Giscus] and generate the snippet__ through their configuration tool
    to load the comment system. Copy the snippet for the next step. The
    resulting snippet should look similar to this: