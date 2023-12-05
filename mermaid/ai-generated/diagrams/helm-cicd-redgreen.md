``` mermaid
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
    build_details(Build Details)<br>Compile source code, package artifacts
    test_details(Test Details)<br>Run automated tests on artifacts
    deploy_staging_details(Deploy to Staging Details)<br>Deploy to a staging environment for further testing
    deploy_helm_repo_details(Helm Packaging Details)<br>Package Helm charts and push to repository
    deploy_production_details(Deploy to Production Details)<br>Final deployment to production environment
  end

  subgraph MFE Details
    deploy_mfe_details(Deploy Micro Frontend Details)<br>Deploy the Micro Frontend
    deploy_mfe_green_details(Deploy MFE - Green Details)<br>Green deployment of the Micro Frontend
    deploy_mfe_red_details(Deploy MFE - Red Details)<br>Red deployment of the Micro Frontend
  end

  build --> build_details
  test --> test_details
  deploy_staging --> deploy_staging_details
  deploy_helm_repo --> deploy_helm_repo_details
  deploy_production --> deploy_production_details
  deploy_mfe --> deploy_mfe_details
  deploy_mfe_green --> deploy_mfe_green_details
  deploy_mfe_red --> deploy_mfe_red_details

```