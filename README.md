# Elastic Kubernetes Service (EKS)

## EKS Cluster Overview

An EKS (Elastic Kubernetes Service) cluster is built from several fundamental components described as follows:

**EKS Control Plane**: AWS offers the EKS Control Plane as a fully managed service, incorporating key Kubernetes master elements such as etcd, kube-apiserver, and kube-controller.

- Every EKS cluster operates with its own isolated control plane, maintaining separation across different clusters and AWS accounts.
- A minimum of two API server nodes and three etcd nodes power the control plane, distributed among three Availability Zones in a given region.
- AWS provides automatic monitoring and replacement of failing control plane instances, restarting them across the region's Availability Zones.

**Worker Nodes and Node Groups:** Application workloads execute on worker nodes, which are EC2 instances known in Kubernetes terminology as worker machines.
 
- These EKS worker nodes exist within your AWS account and establish connections to the cluster's control plane through the cluster API server endpoint.
- Groups of nodes contain one or multiple EC2 instances that operate within an EC2 Autoscaling group.
- Each instance in a node group must share identical characteristics: the same instance type, identical Amazon Machine Image (AMI), and common EKS worker node IAM role.

**Fargate Profiles (Serverless):** EKS supports running application workloads on Serverless Fargate profiles as an alternative to EC2 instances.

- AWS Fargate provides compute capacity for containers that scales on-demand with appropriate sizing.
- Using Fargate eliminates the requirement to provision, configure, or manage virtual machine groups for container operations.
- Fargate ensures each pod operates within its own isolated environment, preventing it from sharing underlying kernel, CPU, memory, or elastic network interface resources with neighboring pods.
- AWS developed dedicated Fargate controllers that identify and assign pods to Fargate profiles.

**VPC:** The AWS VPC (Virtual Private Cloud) establishes secure networking protocols essential for operating production-grade workloads on EKS.

- Network policies within AWS VPC are utilized by EKS to control traffic flow among control plane components in individual clusters.
- EKS cluster control plane components maintain isolation and prevent cross-communication with separate clusters or AWS accounts, unless specifically permitted via Kubernetes RBAC (Role-Based Access Control) policies.
- These security measures combined with high availability features position EKS as a trusted and advisable platform for production environments.
