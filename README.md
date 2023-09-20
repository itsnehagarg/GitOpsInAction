# What is GitOps?

GitOps is a mechanism to automate infrastructure for the DevOps and other specialized engineers.
GitOps is mainly defined as "GitOps uses Git repositories as a single source of truth to deliver infrastructure as code."

# GitOps Tools
~ ArgoCD
~ FluxCD
~ Code Fresh
~ Jenkins X

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

7. kubectl get svc
![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/85b0657a-482d-49c3-8923-283303a7e469)

8. kubetcl get svc -n argocd

![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/937cab19-c120-4c61-a259-03491f585fbc)

9. argocd server interacts with the CLI. We are going to edit the file by using the below command. We are editing the service because by default it comes with the service type as ClusterIP mode and we want this to be NodePort mode so that we can access this service over the web browser.

`` kubectl edit svc argocd-server -n argocd
``

10. We need port forwarding to access:

`` minikube service list -n argocd
``



11. Minikube creates a tunnel and provides the Ip address as shown below using the cmd:
    
``
minikube service argocd-server -n argocd
``

13. We can access the ArgoCD on our browser using the IPs given by above command.


14. ArgoCD UI is up! Yay!

![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/b14b77de-d7f6-4e3d-adbb-156bceafa6cf)

14. Let's try to login now.

Now use the command to check the password prseent in the ArgoCD secret file.
`` kubectl get secret -n argocd

``
![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/c0072c05-b329-4ec7-9c37-cc16d6b67220)



`` kubectl edit secret argocd-initial-admin-secret -n argocd
``

Now get the password and then decrypt the secrets.

``
echo secret_password  | base64 --decode
``
Now paste the password in the browser and we can login!

![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/cafdf71e-b8fd-4ecf-a3e5-b2029f56ea22)

Lets try out some projects:

1. Click on Create Application button on your ArrgoCD UI:
![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/a282a0ff-a370-4cff-8343-be178065b8a7)

2. In Sync Policy, select Automatic so, ARgo CD automatically deploys the app.

3. Provide the URL of the repository and the path:
![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/a0a67944-2906-45fb-86d2-307fbfc4ae90)

4. Provide the Cluster URL and the namespace
![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/2af2797b-b069-4a4b-8344-5a1c21feea80)

5. Click on Create button.
![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/6e93662b-838d-4c78-9d19-1769873474cc)

6. Now ArgoCD is getting the application from the GitHub link that we have provided earlier. It will start fetching the configurations mentioned in guestbook-ui-deployment.yaml & guestbook-ui-svc.yaml
7. It will deploy it on Kubernetes cluster.
![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/9cc04697-b922-42dd-b408-e6c9fc08567c)

8. Run the command
`` kubectl get deploy``

9.   Now we can also check the ArgoCD UI:
![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/5606b893-15fc-40b2-80fe-07e13991b099)

10.   We can delete the resources that got created by clicking on the "Delete" button.

11. If we are not able to access the ArgoCD UI then all the steps can be performed by using ArgoCD CLI.


# ArgoCD Architecture

ArgoCD Architecture comprises of below components:
~ API Server (exposes the API consumed by the Web UI, CLI, and CI/CD systems)
~ Repository Server (connects to Git and fetches the state)
~ Application Controller (connects to K8s and fetches the state)

![image](https://github.com/itsnehagarg/GitOpsInAction/assets/20385826/62baca87-9bcb-4a35-a3db-fb0f2562bb4a)




### References and Image Credits:
https://argo-cd.readthedocs.io/en/stable/















GitOps tools, ArgoCD, Architecture, Implementation
