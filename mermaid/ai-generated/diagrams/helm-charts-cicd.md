``` mermaid
graph TD
  subgraph CI/CD Pipeline
    build(Build) -->|Artifacts| test(Test)
    test -->|Pass| deploy_staging(Deploy to Staging)
    deploy_staging -->|Success| deploy_helm_repo(Package and Push Helm Charts)
    deploy_helm_repo -->|Success| deploy_production(Deploy to Production)
  end

```