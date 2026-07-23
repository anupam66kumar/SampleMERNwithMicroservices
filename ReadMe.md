# **`MERN Microservices Application with CI/CD & Kubernetes Deployment`** 

```
A full-stack MERN microservices application containerized with Docker, automated
via Jenkins CI, stored in AWS ECR, deployed onto an Amazon EKS cluster, and
integrated with MongoDB Atlas.
```

### **`GitHub Repo: https://github.com/anupam66kumar/SampleMERNwithMicroservices.git`** 

```
---
```

```
Architecture Overview
* **Frontend:** React.js served via Nginx (Port 80)
* **Backend Services:** Node.js microservices (`helloservice` on port 3001,
`profileservice` on port 3002)
* **Database:** MongoDB Atlas (Cloud-hosted database cluster)
* **CI/CD Pipeline:** Jenkins declarative pipeline script (`Jenkinsfile`)
* **Orchestration:** Kubernetes (Amazon EKS) managed via `kubectl` and custom
manifests
```

```
---
```

```
## Project Directory Structure
```

```
SampleMERNwithMicroservices/
├── backend/
│   ├── helloservice/
│   │   ├── Dockerfile
│   │   ├── index.js
│   │   └── package.json
│   └── profileservice/
│       ├── Dockerfile
│       ├── index.js
│       └── package.json
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   └── src/
├── k8s/
│   └── all-services.yaml
└── Jenkinsfile
```

Step-by-Step Implementation
---------------------------

### 1\. CI/CD Pipeline Automation(Jenkins & ECR)

The application uses a Jenkinsfileat the root directory to automate checking out code, logging into AWSECR, building images, and pushing them securely.

*   **Jenkins Pipeline Execution:**_(screenshot of successful Jenkins build ):_
    <img width="1037" height="895" alt="image" src="https://github.com/user-attachments/assets/e8f340b5-c01d-4700-8948-13b4d0a1b6cd" />
    <img width="1655" height="895" alt="image" src="https://github.com/user-attachments/assets/0c179553-1576-4308-8f00-a03910826681" />
    

*   **AWS ECR Repositories:**_(screenshot of ECR repositories containing frontend,helloservice, and profileservice)_
    <img width="1655" height="895" alt="image" src="https://github.com/user-attachments/assets/8eb1530a-48ec-4c34-9fa6-97e16ffa395e" />


### 2\. Kubernetes Cluster Provisioning(Amazon EKS)

Created an EKS managed cluster withtwo worker nodes using eksctl:

Bash
eksctl create cluster --name streaming-cluster --region ap-southeast-2 --node-type t3.medium --nodes 2   `

*   **Cluster Nodes Verification(kubectl get nodes):**_(Insert screenshot of active nodes here)_
    <img width="813" height="181" alt="image" src="https://github.com/user-attachments/assets/2f9759ff-4218-4d01-a61a-699b4c0bcc2a" />
    

### 3\. Deploying Microservices &MongoDB Atlas

All Kubernetes deployments, ClusterIPservices, and the frontend LoadBalancer service are defined withink8s/all-services.yaml. The profileservice connects to MongoDB Atlas using a secure connection stringenvironment variable.

Apply the configurations to thecluster:

Bash

kubectl apply -f k8s/all-services.yaml   `

*   **Running Pods Verification(kubectl get pods):**_(Insert screenshot showing 1/1 Running state for all pods here:screenshots/kubectl-pods.png)_
    <img width="817" height="141" alt="image" src="https://github.com/user-attachments/assets/b456712b-5e89-4008-a9ae-678cc2942a6c" />


Verification & Local Access
---------------------------

To verify application health andbrowse the user interface:

Bash

   kubectl port-forward svc/frontend-service 8080:80  
   kubectl port-forward svc/profileservice-service 3002:3002  
   kubectl port-forward svc/helloservice-service 3001:3001  
   
OUTPUT   `
-------
<img width="817" height="159" alt="image" src="https://github.com/user-attachments/assets/233abc68-70bf-4757-a17e-8569b2aa2135" />
<img width="1657" height="367" alt="image" src="https://github.com/user-attachments/assets/17363816-7def-4557-883e-e34b3e70529c" />
<img width="1657" height="367" alt="image" src="https://github.com/user-attachments/assets/f557df57-3890-456c-842a-b6c80b88d3e6" />

