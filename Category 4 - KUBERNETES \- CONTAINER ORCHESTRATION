**════════════════════════════════════════════════════════════════════**  
**CATEGORY 4: KUBERNETES \- CONTAINER ORCHESTRATION**  
**════════════════════════════════════════════════════════════════════**

**Covering: 7-day Kubernetes series including installation, fundamentals, practical examples, and Helm**

**/\* COMMENT: Kubernetes (K8s) is the industry-standard container orchestration platform.**  
   **It automates deployment, scaling, and management of containerized applications.**  
   **Essential skill for modern DevOps and cloud-native architectures. \*/**

**4.1 KUBERNETES ARCHITECTURE:**

**CONTROL PLANE COMPONENTS:**  
**● API Server: Front-end for K8s control plane**  
**● etcd: Distributed key-value store for cluster data**  
**● Scheduler: Assigns pods to nodes**  
**● Controller Manager: Runs controller processes**  
**● Cloud Controller Manager: Integrates with cloud providers**

**NODE COMPONENTS:**  
**● Kubelet: Agent running on each node**  
**● Container Runtime: Docker, containerd, or CRI-O**  
**● Kube-proxy: Network proxy on each node**

**KEY CONCEPTS:**

**● Pod: Smallest deployable unit (1+ containers)**  
**● Deployment: Manages replica sets and rolling updates**  
**● Service: Exposes pods as network service**  
**● Namespace: Virtual clusters within physical cluster**  
**● ConfigMap: Configuration data**  
**● Secret: Sensitive data (passwords, tokens)**  
**● Volume: Persistent storage**  
**● Ingress: HTTP/HTTPS routing to services**

**ESSENTIAL KUBECTL COMMANDS:**

**/\* COMMENT: kubectl is the command-line tool for Kubernetes. These commands cover**  
   **everyday operations for managing K8s clusters. \*/**

**\# Cluster Information**  
**kubectl cluster-info**  
**kubectl get nodes**  
**kubectl get pods \-A               \# All pods in all namespaces**  
**kubectl get pods \-o wide          \# Detailed view**

**\# Deployments**  
**kubectl create deployment nginx \--image=nginx**  
**kubectl get deployments**  
**kubectl scale deployment nginx \--replicas=3**  
**kubectl set image deployment/nginx nginx=nginx:1.21**  
**kubectl rollout status deployment/nginx**  
**kubectl rollout undo deployment/nginx**  
**kubectl delete deployment nginx**

**\# Pods**  
**kubectl get pods**  
**kubectl describe pod pod\_name**  
**kubectl logs pod\_name**  
**kubectl logs \-f pod\_name          \# Follow logs**  
**kubectl exec \-it pod\_name \-- /bin/bash**  
**kubectl delete pod pod\_name**

**\# Services**  
**kubectl expose deployment nginx \--port=80 \--type=LoadBalancer**  
**kubectl get services**  
**kubectl describe service nginx**  
**kubectl delete service nginx**

**\# Namespaces**  
**kubectl get namespaces**  
**kubectl create namespace dev**  
**kubectl config set-context \--current \--namespace=dev**  
**kubectl delete namespace dev**

**\# Apply/Create from YAML**  
**kubectl apply \-f deployment.yaml**  
**kubectl delete \-f deployment.yaml**  
**kubectl get all \-n namespace**

**\# Troubleshooting**  
**kubectl describe pod pod\_name**  
**kubectl logs pod\_name \--previous  \# Previous container logs**  
**kubectl top nodes                 \# Resource usage**  
**kubectl top pods**

**4.2 KUBERNETES YAML EXAMPLES:**

**\# Deployment**  
**apiVersion: apps/v1**  
**kind: Deployment**  
**metadata:**  
  **name: nginx-deployment**  
**spec:**  
  **replicas: 3**  
  **selector:**  
    **matchLabels:**  
      **app: nginx**  
  **template:**  
    **metadata:**  
      **labels:**  
        **app: nginx**  
    **spec:**  
      **containers:**  
      **\- name: nginx**  
        **image: nginx:1.21**  
        **ports:**  
        **\- containerPort: 80**  
        **resources:**  
          **requests:**  
            **memory: "64Mi"**  
            **cpu: "250m"**  
          **limits:**  
            **memory: "128Mi"**  
            **cpu: "500m"**

**\# Service**  
**apiVersion: v1**  
**kind: Service**  
**metadata:**  
  **name: nginx-service**  
**spec:**  
  **selector:**  
    **app: nginx**  
  **ports:**  
  **\- protocol: TCP**  
    **port: 80**  
    **targetPort: 80**  
  **type: LoadBalancer**

**\# ConfigMap**  
**apiVersion: v1**  
**kind: ConfigMap**  
**metadata:**  
  **name: app-config**  
**data:**  
  **APP\_ENV: production**  
  **DB\_HOST: mysql-service**

**\# Secret**  
**apiVersion: v1**  
**kind: Secret**  
**metadata:**  
  **name: db-secret**  
**type: Opaque**  
**data:**  
  **password: cGFzc3dvcmQxMjM=  \# base64 encoded**
