# What's Red Hat OpenShift
Red Hat OpenShift, the industry's leading hybrid cloud application platform powered by Kubernetes, 
brings together tested and trusted services to reduce the friction of developing, modernizing,
deploying, running, and managing applications. 
See official link: [Openshift](https://www.redhat.com/en/technologies/cloud-computing/openshift)

## Getting Started - Steps
- Signup/signin to Openshift account: [See-Link](https://cloud.redhat.com/openshift/install)
- Navigate to: Clusters -> Cluster Type -> Amazon Web Services -> Installer-provisioned infrastructure
   ![openshift](photos/install.png)

### Install OpenShift on AWS
AWS Openshift installation Link: [See-Link](https://console.redhat.com/openshift/install/aws/installer-provisioned)
There are ***Two*** Cluster-Setup options to choose: a customized cluster ***or*** quickly install.

  - Install the Openshift installer and client on your local computer.
  - Move that file to your remote linux machine. You're see the client and installer.
  - Extract the installer and client: 

     ```tar xvf openshift-install-linux.tar.gz```
     ```tar xvf openshift-client-linux.tar.gz```

  - Move the oc, kubectl and installer to usr/bin directoory

    ```sudo mv oc /usr/local/bin/```
    ```sudo mv kubectl /usr/local/bin/```
    ```sudo cp openshift-install /usr/local/bin/```
    ```which openshift-install```
    ```oc help```

  - Copy the secret content and paste in a file. This secret is from the redhad account, 
    used to Map the AWS Cluster with the redHat account.
  - ***In the AWS Console, setup the following:***
      - Route53 public Hoster Zone
      - IAM Adminstrative User
      - Create Access and Secret Keys for the user

  - Create an SSH Key in the root directory
    ```[root@ip-172-31-12-23 ~]# ssh-keygen -t rsa -b 4096 -N '' -f id_rsa```

  - Evaluate and add to root
    ```
    [root@ip-172-31-12-23 ~]# eval "$(ssh-agent -s)"
    [root@ip-172-31-12-23 ~]# ssh-add id_rsa
    ```
  - ***Copy*** and ***cd*** to the rsa keys to the /usr/local/bin/ folder 
   ```cp id_rsa id_rsa.pub /usr/local/bin/```
   ```cd /usr/local/bin/```
  
  - Now install Openshift
  ```./openshift-install create cluster``` 

 SEE MY workflow process

 ```
 [ec2-user@ip-172-31-12-23 s]$ ls
 openshift-install-linux.tar.gz  README.md
 [ec2-user@ip-172-31-12-23 s]$ tar xvf openshift-install-linux.tar.gz 
 README.md
 openshift-install
 [ec2-user@ip-172-31-12-23 s]$ ls
 openshift-install  openshift-install-linux.tar.gz  README.md
 [ec2-user@ip-172-31-12-23 s]$ ls
 openshift-client-linux.tar.gz  openshift-install  openshift-install-linux.tar.gz  README.md
 [ec2-user@ip-172-31-12-23 s]$ tar xvf openshift-client-linux.tar.gz 
 README.md
 oc
 kubectl
 [ec2-user@ip-172-31-12-23 s]$ ls
 kubectl  oc  openshift-client-linux.tar.gz  openshift-install  openshift-install-linux.tar.gz  README.md
 [ec2-user@ip-172-31-12-23 s]$ 
```







https://www.youtube.com/watch?v=vP-epd-Fyx0&t=4s

https://github.com/cloudacademy/openshift-voteapp-demo

AWS Openshift installation Link: [See-Link](https://docs.openshift.com/container-platform/4.1/installing/installing_aws/installing-aws-account.html)



mkdir key && touch so.sh
ssh-keygen -t rsa -b 4096 -N '' -f root/id_rsa/so.sh

chmod 400 ssh-add keys/so.sh
ssh-add keys/so.sh 


