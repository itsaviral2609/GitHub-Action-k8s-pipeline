# GitHub-Action-k8s-pipeline

# CI/CD Pipeline with Docker and Kubernetes (kind)

This repository contains a GitHub Actions workflow that automates the process of setting up a Node.js application, building a Docker container, and deploying it to a local Kubernetes cluster using `kind`.

## Workflow Steps

The CI/CD pipeline performs the following steps on every push to the `main` branch:

1. **Checkout Repository**: Clone the `wizdesk` repository to the GitHub Actions runner.

2. **Set up Node.js**: Configure the runner to use Node.js version 18.

3. **Install Dependencies**: Run `npm install` to install the necessary dependencies for the project.

4. **Start the Application**: Execute `npm start` to start the application. This step is generally for verification purposes in this context, as the application will be containerized.

5. **Build Docker Image**: Build a Docker image named `aviralsingh2609/wizdesk:latest`. Replace `aviralsingh2609` with your Docker Hub username.

6. **Log in to Docker Hub**: Use the provided secrets to authenticate against Docker Hub for image push capabilities.

7. **Push Docker Image to Docker Hub**: Push the newly built Docker image to the Docker Hub repository.

8. **Install `kind`**: Download and install the `kind` tool, which is used to create a local Kubernetes cluster.

9. **Create a Kubernetes cluster with `kind`**: Initialize a new Kubernetes cluster using `kind`.

10. **Load Docker Image to `kind` Cluster**: Load the built Docker image into the `kind` cluster's container registry.

11. **Apply Kubernetes Manifests**: Apply the Kubernetes manifests located in the `k8s/` directory. These manifests should define the Kubernetes resources such as Deployments, Services, etc.

12. **Check Deployment Status**: Check the rollout status of the deployment to ensure it completes successfully.

## Prerequisites

- You must have a Docker Hub account with a repository where the Docker image will be pushed.
- The `DOCKER_HUB_USERNAME` and `DOCKER_HUB_ACCESS_TOKEN` secrets must be set in your GitHub repository to allow the workflow to authenticate with Docker Hub.
- The Kubernetes manifest files must be present in the `k8s/` directory at the root of the repository.

## Usage

To use this workflow:

1. Fork the `wizdesk` repository into your GitHub account.
2. Ensure you have the `DOCKER_HUB_USERNAME` and `DOCKER_HUB_ACCESS_TOKEN` secrets set in your repository settings.
3. Create or ensure the Kubernetes manifest files are properly set up in the `k8s/` directory.
4. Push your changes to the `main` branch to trigger the workflow.

## Note

The workflow is currently set up to run on a single Docker image and `latest` tag. You may want to modify the workflow to handle versioned releases using Git tags.
