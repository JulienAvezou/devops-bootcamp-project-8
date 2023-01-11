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

### Configure Autoscaling in EKS cluster
- autoscaling group created by default when created node group
- create custom policy to enable autoscaling & attach new policy to existing node group IAM role
![Capture d’écran 2023-01-10 à 10 56 36](https://user-images.githubusercontent.com/62488871/211519945-1467f882-8027-4e09-ad10-a4330a1bd4ea.png)
- check that tags are configured for autoscaling group (should be created by default)
![Capture d’écran 2023-01-11 à 08 10 42](https://user-images.githubusercontent.com/62488871/211740715-d3f39ad4-3318-48f1-859c-8cc439970946.png)
- create deployment for autoscaler
<img width="663" alt="Capture d’écran 2023-01-11 à 08 20 42" src="https://user-images.githubusercontent.com/62488871/211742470-2a50449f-7d36-485e-a9d4-883999c6a60f.png">
<img width="386" alt="Capture d’écran 2023-01-11 à 08 22 37" src="https://user-images.githubusercontent.com/62488871/211742829-dbba587a-fb36-479c-9601-08a0e502f5dc.png">
- edit the deployment (add annotation, replace placeholder with actual cluster name)
- check logs for pod running cluster-autoscaler
<img width="664" alt="Capture d’écran 2023-01-11 à 08 51 46" src="https://user-images.githubusercontent.com/62488871/211749091-e03b53ab-1233-4c55-8f87-b508cc15f077.png">
<img width="473" alt="Capture d’écran 2023-01-11 à 08 53 29" src="https://user-images.githubusercontent.com/62488871/211749113-b8c2a051-f113-4219-a1ea-6ab932d7cbc2.png">
<img width="629" alt="Capture d’écran 2023-01-11 à 08 53 49" src="https://user-images.githubusercontent.com/62488871/211749134-cd605445-f2cb-4013-8164-fff3764e99c1.png">
- change min nodes to 1 to check that autoscaler scales down to 1
![Capture d’écran 2023-01-11 à 09 12 33](https://user-images.githubusercontent.com/62488871/211752755-116215c0-83b4-4a9f-b31e-377b810e5247.png)

### Deploy app on EKS
- create deployment and service 
<img width="667" alt="Capture d’écran 2023-01-11 à 09 09 54" src="https://user-images.githubusercontent.com/62488871/211752882-1d182d47-ef31-4340-a3c7-bd5c09db0a09.png">

![Capture d’écran 2023-01-11 à 09 16 56](https://user-images.githubusercontent.com/62488871/211757980-f95993b1-ce7e-4051-a2e1-b2a6a0d57742.png)


