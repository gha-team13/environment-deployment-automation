spinup-destroy.yml

When a developer creates a pull request to merge their changes, the continuous delivery pipeline  automatically sets up an isolated Azure environment. This environment hosts a fully functional version of the application, allowing team members, stakeholders, or QA engineers to test the changes without affecting the production environment. Once the testing is complete or the pull request is closed, the workflow tears down the environment, saving costs.

Instead of manually provisioning and deprovisioning environments, we use labels like 'spin up environment' and 'destroy environment' on pull requests. These labels trigger workflows that handle the entire lifecycle of the Azure resources. This approach not only reduces the time and effort required to manage resources but also ensures that no unnecessary infrastructure is left running, optimizing costs and simplifying operations.

deploy-staging.yml

Each time the developers push new code, the system automatically compiles and packages the application. This ensures every build is consistent and adheres to predefined quality standards, eliminating manual errors.
The platform than packages its application as Docker images. Each image is tagged with a unique identifier, such as the commit SHA from GitHub, making it easy to trace specific deployments to the exact version of the codebase.
After building the application, the pipeline stores the build artifacts separately. 
Before pushing updates to production, the application is deployed to a staging environment. This environment replicates production, enabling thorough testing and ensuring new changes don’t disrupt end-users.
The entire process is powered by GitHub Actions, which automates the workflow. From building to deploying, this integration reduces manual effort, speeds up delivery, and minimizes errors, allowing ius to deliver updates rapidly and with confidence.

deploy-prod.yml
When the developers push their changes to the main branch, signaling the start of the deployment process. The workflow compiles and prepares the application for the next steps, firstly a  is built from the compiled application and uploaded to the GHCR. The containerized application is than deployed to Azure App Service, thus updating the production environment. The CD pipeline is thus fully automated, ensuring smooth, consistent, and reliable deployments without manual intervention.
