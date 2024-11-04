
# Kubernetes Python Development Environment

This project provides a deployable, containerized Python development environment for students, using Docker and Kubernetes. Each student receives an isolated Jupyter Lab instance to work with Python code without interfering with others. The project demonstrates Kubernetes and Docker expertise in setting up scalable, isolated, and persistent environments.

## Features

- **Isolated Environments**: Each instance runs separately for individual users.
- **Persistence**: Student work is saved using Kubernetes Persistent Volumes.
- **Scaling**: Kubernetes handles scaling if multiple environments are required.
- **Monitoring**: Optional setup for resource monitoring using tools like Prometheus and Grafana.

## Tech Stack

- **Docker**: Used for containerizing the Python development environment.
- **Kubernetes**: Manages deployment, scaling, and networking.
- **Helm**: Simplifies Kubernetes deployments with reusable configurations.

## Prerequisites

Make sure you have the following installed:
- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/) (or any Kubernetes cluster)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Helm](https://helm.sh/docs/intro/install/)

---

## Project Structure

```plaintext
my-k8s-python-env/
├── docker/
│   └── Dockerfile
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── pvc.yaml
└── helm/
    └── python-dev-env/
```

- **docker/Dockerfile**: Builds the custom Python development image with Jupyter Lab.
- **k8s/deployment.yaml**: Kubernetes Deployment manifest for the environment.
- **k8s/service.yaml**: Service manifest to expose the environment.
- **k8s/pvc.yaml**: Persistent Volume Claim for data persistence.
- **helm/python-dev-env**: Helm chart for easier deployments.

---

## Setup Instructions

### 1. Build and Push Docker Image

Build the Docker image with Jupyter Lab:

```bash
docker build -t <your_dockerhub_username>/python-dev-env:latest -f docker/Dockerfile .
docker push <your_dockerhub_username>/python-dev-env:latest
```

### 2. Deploy Using Kubernetes Manifests

1. **Apply Persistent Volume Claim**:

   ```bash
   kubectl apply -f k8s/pvc.yaml
   ```

2. **Deploy the Environment**:

   ```bash
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml
   ```

3. **Check Deployment**:

   ```bash
   kubectl get pods
   kubectl get services
   ```

4. **Access the Environment**:
   - Locate the Service’s `NodePort` to access Jupyter Lab at `http://<minikube_ip>:<NodePort>`.

### 3. Deploy Using Helm (Optional)

For reusable configurations and easier deployment management, use Helm:

1. **Install Helm Chart**:

   ```bash
   helm install my-python-dev-env helm/python-dev-env
   ```

2. **Customize Configurations**: Update `values.yaml` in the Helm chart for specific settings.

---

## Useful Commands

- **Scaling Pods**:
  ```bash
  kubectl scale deployment python-dev-env --replicas=<number_of_replicas>
  ```

- **View Logs**:
  ```bash
  kubectl logs <pod_name>
  ```

- **Delete Deployment and Service**:
  ```bash
  kubectl delete -f k8s/deployment.yaml
  kubectl delete -f k8s/service.yaml
  ```

## Contributing

Feel free to fork this repository and submit pull requests. Contributions are always welcome.

## License

This project is licensed under the MIT License.
