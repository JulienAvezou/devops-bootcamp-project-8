# devops-bootcamp-project-8
Demo for module 11 - EKS

### Create EKS Cluster w AWS mgmnt console

1. Create IAM Role in AWS account & assign role to EKS cluster managed by AWS
![Capture d’écran 2023-01-09 à 17 36 58](https://user-images.githubusercontent.com/62488871/211360041-c57895e1-a873-4194-94a0-033800e67695.png)

2. Create VPC for Worker Nodes
can use template with EKS specific config
![Capture d’écran 2023-01-09 à 18 05 38](https://user-images.githubusercontent.com/62488871/211365614-c6472012-ccb3-4af1-bd56-77fe2cfc2923.png)

3. Create EKS Cluster
ensure that eks cluster role is selected and that custom vpc is selected too
![Capture d’écran 2023-01-10 à 09 29 14](https://user-images.githubusercontent.com/62488871/211500061-d7782300-7377-4304-9e20-8ea448e00fa2.png)

4. Connect to eks cluster using kubectl 
aws eks update-kubeconfig --name eks-cluster-test (creates kubeconfig file)
<img width="662" alt="Capture d’écran 2023-01-10 à 09 47 54" src="https://user-images.githubusercontent.com/62488871/211504084-015295a3-27b7-41c7-aa87-5ed7e9863daa.png">
kubectl cluster-info -> check that cluster is running at same endpoint as shown on AWS console under API server endpoint section

5. Create EC2 Role for Node Group (worker nodes) with necessary policies attached
![Capture d’écran 2023-01-10 à 10 05 44](https://user-images.githubusercontent.com/62488871/211508229-8be8be72-ffef-4364-b469-5ab42f2ef181.png)

6. Add Node group to cluster
![Capture d’écran 2023-01-10 à 10 20 32](https://user-images.githubusercontent.com/62488871/211511618-c0d75cba-b0e0-4b21-9dfb-db5e69271bd7.png)
<img width="660" alt="Capture d’écran 2023-01-10 à 10 20 43" src="https://user-images.githubusercontent.com/62488871/211511626-095d8c51-ce97-461f-aa2c-76fd00a38f0f.png">


