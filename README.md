# What is GitOps?

# GitOps Tools


## ArgoCD Installation
Go to: https://argo-cd.readthedocs.io/en/stable/operator-manual/installation/

1. Start the minikube which starts the local Minikube Kubernetes cluster.

   Use the below command:
   
   `` minikube start
   ``

   ![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/74b8d43c-05c2-4732-aaea-cf5444b6d9c8)

3. Use the below command to create the ArgoCD namespace:
`` kubectl create namespace argocd
``
5. Use the below command to install ArgoCD, a GitOps-based continuous delivery tool for Kubernetes, by applying the resource definitions provided in the specified YAML file to the argocd namespace in your Kubernetes cluster.
   
`` kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
``
 ![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/72998e21-57e6-4bc6-8526-edbd1254586d)

6. Let's check if the pods have come up using the below command:

`` kubectl get pods -n argocd -w

``
![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/7fc80557-1807-4195-8c3c-4b0ed5134ea0)


# ArgoCD Architecture


# ArgoCD Hands-On













GitOps tools, ArgoCD, Architecture, Implementation
