# Kube-news

## Objective
The Kube-news project is a NodeJS application designed to serve as an example application for working with container usage. It served me to study docker and kubernetes, which are crucial to today's web development. I've also created an dockerhub image, on which you can find [here](https://hub.docker.com/repository/docker/lucaspa123/docker-and-k8s-study/general).

## Configuration
To configure the application, it is necessary to have a Postgre database. To set up access to the database, configure the following environment variables:

- `DB_DATABASE`: Name of the database to be used.
- `DB_USERNAME`: Database user.
- `DB_PASSWORD`: Password for the database user.
- `DB_HOST`: Database address.

## Installation Guide

### Prerequisites
Make sure you have the following tools installed:

1. **kubectl:** You can install it by following the instructions [here](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).

2. **k3d:** K3d is a lightweight wrapper to run k3s (a lightweight Kubernetes distribution) inside Docker. Install it by following the steps outlined [here](https://k3d.io/v5.6.0/#installation).

3. **Database Client:** You will need a database client to access the PostgreSQL database. We recommend using [DataGrip](https://www.jetbrains.com/datagrip/), but you can choose any other client of your preference.

### Setup Local Kubernetes Environment

1. Create a local Kubernetes cluster using k3d:

   ```bash
   k3d cluster create meucluster --server 3 --agents 3 -p "8080:31000@loadbalancer"
   ```
2. Apply the Kubernetes deployment configuration:
    ```bash
    kubectl apply -f k8s/deployment.yaml
    ```
3. Verify the deployment:
    ```bash
    kubectl get all
    ```

### Accessing the Database

To access the PostgreSQL database, follow these steps:

1. Forward the database port to your local machine:
    ```bash
    kubectl port-forward pod/pod-id 5432:5432
    ```
    Replace pod-id with the actual ID or name of the PostgreSQL pod.

2. Use your database client (e.g., DataGrip) to connect to the PostgreSQL database:

- Host: localhost
- Port: 5432
- Database: Use the value set in DB_DATABASE
- Username: Use the value set in DB_USERNAME
- Password: Use the value set in DB_PASSWORD

Now, you should be able to interact with the Kube-news application and its PostgreSQL database in your local Kubernetes environment.