## Step 1: Create a Namespace for Jenkins. 

```sh
kubectl create namespace devops-tools
```

kubectl apply -f 1-serviceAccount.yaml
kubectl create -f 2-volume.yaml
kubectl apply -f 3-deployment.yaml
kubectl -n devops-tools get deploy
kubectl -n devops-tools get po
kubectl apply -f 4-service.yaml
kubectl -n devops-tools get svc
kubectl -n devops-tools edit svc

## Get password

kubectl exec -it jenkins-bf6b8d5fb-bdk5g cat /var/jenkins_home/secrets/initialAdminPassword -n devops-tools


## Setup Credentials in Jenkins to Access GKE

There are multiple ways to access your GKE cluster using Jenkins Pod, either you can keep your Kube config in Jenkins global credentials, or you can keep Kube config directly inside our pod so that the pod can it directly

# first go inside pod
kubectl exec -it pod_name -- /bin/bash 
# inside pod in /var/jenkins_home directory create a folder .kube
mkdir .kube
# Copy your config file inside the pod 
sudo kubectl cp -r ~/.kube/config pod_name:/var/jenkins_home/.kube/config
now you have proper connectivity with your cluster

Configure Kubernetes Cloud in Jenkins

Go to Manage Jenkins -> Manage Node and Cloud -> Configure Clouds -> Add a new cloud -> Kubernetes -> Kubernetes Cloud Details.