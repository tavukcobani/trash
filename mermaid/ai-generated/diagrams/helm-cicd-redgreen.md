# CI/CD Pipeline

```mermaid
graph TD
  style build fill:#3498db,stroke:#2980b9
  style test fill:#2ecc71,stroke:#27ae60
  style deploy_staging fill:#f39c12,stroke:#d35400
  style deploy_helm_repo fill:#9b59b6,stroke:#8e44ad
  style deploy_production fill:#e74c3c,stroke:#c0392b
  style deploy_mfe fill:#27ae60,stroke:#2ecc71
  style deploy_mfe_green fill:#27ae60,stroke:#2ecc71
  style deploy_mfe_red fill:#e74c3c,stroke:#c0392b
  
  subgraph CI/CD Pipeline
    build(Build) -->|Artifacts| test(Test)
    test -->|Pass| deploy_staging(Deploy to Staging)
    deploy_staging -->|Success| deploy_helm_repo(Package and Push Helm Charts)
    deploy_helm_repo -->|Success| deploy_production(Deploy to Production)
    deploy_production -->|Success| deploy_mfe(Deploy Micro Frontend)
  end

  subgraph Red-Green Deployment Model
    deploy_mfe -->|Green| deploy_mfe_green(Deploy MFE - Green)
    deploy_mfe -->|Red| deploy_mfe_red(Deploy MFE - Red)
  end

  subgraph CI/CD Details
    classDef buildClass fill:#3498db,stroke:#2980b9
    class build buildClass
    classDef testClass fill:#2ecc71,stroke:#27ae60
    class test testClass
    classDef deployStagingClass fill:#f39c12,stroke:#d35400
    class deploy_staging deployStagingClass
    classDef deployHelmClass fill:#9b59b6,stroke:#8e44ad
    class deploy_helm_repo deployHelmClass
    classDef deployProductionClass fill:#e74c3c,stroke:#c0392b
    class deploy_production deployProductionClass
    classDef deployMFClass fill:#27ae60,stroke:#2ecc71
    class deploy_mfe deployMFClass
  end

  subgraph MFE Details
    classDef deployMFEDetailsClass fill:#27ae60,stroke:#2ecc71
    class deploy_mfe_details deployMFEDetailsClass
    classDef deployMFEGreenDetailsClass fill:#27ae60,stroke:#2ecc71
    class deploy_mfe_green_details deployMFEGreenDetailsClass
    classDef deployMFERedDetailsClass fill:#e74c3c,stroke:#c0392b
    class deploy_mfe_red_details deployMFERedDetailsClass
  end

  build --> build_details("Compile source code, package artifacts")
  test --> test_details("Run automated tests on artifacts")
  deploy_staging --> deploy_staging_details("Deploy to a staging environment for further testing")
  deploy_helm_repo --> deploy_helm_repo_details("Package Helm charts and push to repository")
  deploy_production --> deploy_production_details("Final deployment to production environment")
  deploy_mfe --> deploy_mfe_details("Deploy the Micro Frontend")
  deploy_mfe_green --> deploy_mfe_green_details("Green deployment of the Micro Frontend")
  deploy_mfe_red --> deploy_mfe_red_details("Red deployment of the Micro Frontend")
