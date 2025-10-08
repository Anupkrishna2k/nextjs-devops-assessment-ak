# Overview

This repository contains a simple Next.js application which is containerized with Docker, automated with GitHub Actions, and deployed on Kubernetes using minikube.

**Here my objectives are**

1.containerize the application using docker.

2.Automate the docker build and push to ghcr.

3.Deploy the containerized app to Minikube using Kubernetes manifests.

_______________________________________________________________________________________________________________________________________________________________________



## Setup Instructions to run locally

**1. Clone the repository using**
  ```
  git clone https://github.com/Anupkrishna2k/nextjs-devops-assessment-ak.git
  ```

**2. Install Dependencies**

  go into the folder using
  ```
  cd nextjs-devops-assessment-ak
```
  run the followingcommand
  ```
  npm install
```

**3. Run Locally**

  run the followingcommand 
  ```
  npm run dev
```
  The application should be visible at URL:
  ```
  http://localhost:3000
```
____________________________________________________________________________________________________________________________________________________________________________________________________________



## Docker Instructions

Once the app runs fine locally , now you can containerise the application using dockerfile available in the repo.Use the below commands to build the image and run the container locally.

**1. Build Docker Image**
```
docker build -t nextjs-app .
```
**2. Run Docker Container Locally**
```
docker run -p 3000:3000 nextjs-app
```

**Open the below URL in the browser**
```
http://localhost:3000
```

____________________________________________________________________________________________________________________________________________________________________________________



## GitHub Container Registry (GHCR)

The Docker image is pushed automatically through GitHub Actions workflow (.github/workflows/ci.yml) on every push to main branch.

**GHCR Image URL:**
```
ghcr.io/anupkrishna2k/nextjs-app:latest
```

**Workflow steps:**

As you can see in the ci.yaml file , the workflow is in the following way

1.Log in to GHCR

2.Build Docker image

3.Push to GHCR

________________________________________________________________________________________________________________________________________________________________________________________




## Kubernetes Deployment on Minikube

### 1. Start Minikube
```
minikube start --driver=docker
```
**2. Apply Manifests**
```
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
```
**3. Check Pods and Service**
```
kubectl get pods

kubectl get svc
```
**4. Access the Application**
```
minikube service nextjs-app-service --url
```
Open the URL output given by the above command in your browser Next.js app should load.



## Notes

1. .gitignore includes node_modules, .next, .env, .DS_Store to avoid pushing unnecessary files as they are above 100 mb which github does not allow it.

2. Docker image and workflow are configured for public GHCR access.


## References 

1. [Docker docs](https://docs.docker.com/)

2. [github actions docs](https://docs.github.com/en/actions)

3. [minikube docs](https://minikube.sigs.k8s.io/docs/)




