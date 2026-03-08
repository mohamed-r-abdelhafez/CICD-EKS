# End-to-End CI/CD Automation for Amazon EKS
This repository demonstrates designing and automating infrastructure for modern cloud-native applications. The project showcases how leverage CI/CD pipelines, containerization, and Kubernetes orchestration to deliver scalable, reliable, and automated deployments on Amazon EKS.
# Pipeline
![Pipeline](https://github.com/mohamed-r-abdelhafez/CICD-EKS/blob/main/pipeline.png)
# Infrastructure 
**CloudFormation templates** to provision AWS resources.  
Automated environment setup to ensure reproducibility and consistency across deployments.
* **Security Groups**
  
* **ECR**
  * store docker images after build
* **IAM**
    * EKS Cluster  
        1- AmazonEKSClusterPolicy
    * EKS Node Group  
        1- AmazonEC2ContainerRegistryReadOnly  
        2- AmazonEKS_CNI_Policy  
        3- AmazonEKSWorkerNodePolicy  
        4- AWSXrayWriteOnlyAccess  
        5- CloudWatchAgentServerPolicy  
        6- AmazonElasticContainerRegistryPublicReadOnly  
    * Jenkins slave instance  
        1- AmazonEC2ContainerRegistryFullAccess   
        2- AmazonEKSWorkerNodePolicy  


