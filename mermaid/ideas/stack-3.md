```mermaid
graph TD

subgraph "Helm Chart Repo"
  stack1(Helm Chart 1)
  stack2(Helm Chart 2)
  stack3(Helm Chart 3)
end

subgraph "Kubernetes Cluster (EKS)"
  stack1 --> |Deploy| K8S1[Pod 1]
  stack2 --> |Deploy| K8S2[Pod 2]
  stack3 --> |Deploy| K8S3[Pod 3]
end

subgraph "AWS Infrastructure"
  K8S1 --> |Provision| EC2-1[EC2 Instance 1]
  K8S2 --> |Provision| EC2-2[EC2 Instance 2]
  K8S3 --> |Provision| EC2-3[EC2 Instance 3]
  K8S1 --> |Push| ECR1[ECR Repo 1]
  K8S2 --> |Push| ECR2[ECR Repo 2]
  K8S3 --> |Push| ECR3[ECR Repo 3]
end

subgraph "Terraform"
  EC2-1 --> |Terraform| TF1[Terraform Module 1]
  EC2-2 --> |Terraform| TF2[Terraform Module 2]
  EC2-3 --> |Terraform| TF3[Terraform Module 3]
end

subgraph "Micro Frontend Monorepo"
  subgraph "App 1"
    FE1(Docker Compose)
    FE1 --> |Docker| FE1D[App Docker Container]
  end

  subgraph "App 2"
    FE2(Docker Compose)
    FE2 --> |Docker| FE2D[App Docker Container]
  end

  subgraph "App 3"
    FE3(Docker Compose)
    FE3 --> |Docker| FE3D[App Docker Container]
  end
end

subgraph "Next.js with TypeScript"
  FE1D --> |Docker| Nextjs1[Next.js App 1]
  FE2D --> |Docker| Nextjs2[Next.js App 2]
  FE3D --> |Docker| Nextjs3[Next.js App 3]
end

subgraph "Module Federation"
  Nextjs1 --> |Module Federation| Nextjs2
  Nextjs2 --> |Module Federation| Nextjs3
end

subgraph "Node.js Backend"
  Nextjs1 --> |API| Node1[Node.js Backend 1]
  Nextjs2 --> |API| Node2[Node.js Backend 2]
  Nextjs3 --> |API| Node3[Node.js Backend 3]
end
