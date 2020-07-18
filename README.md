# [Kubeflow](https://www.kubeflow.org/) Setup Guide
> Try it on [Brandy Test Server](http://140.112.12.213:31380/)

## Single Node Deployment
### [Linux](https://www.kubeflow.org/docs/started/workstation/getting-started-linux/)
#### Prerequisites
* Ubuntu 18 machine with 
  * min 8 cores, 
  * 16GB RAM, 
  * 250GB storage
* Root privileges on a Ubuntu machine
#### Kubernetes
* Docker CE
  ```
  apt-get update
  apt-get install -y apt-transport-https ca-certificates curl software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
  add-apt-repository \
     "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
     $(lsb_release -cs) \
     stable"
  apt-get update
  apt-get install docker-ce docker-ce-cli containerd.io
  ```
* kubectl
  ```
  curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.0/bin/linux/amd64/kubectl
  chmod +x ./kubectl
  mv ./kubectl /usr/local/bin/kubectl
  ```
* Minikube
  ```
  curl -Lo minikube https://storage.googleapis.com/minikube/releases/v1.2.0/minikube-linux-amd64
  chmod +x minikube
  cp minikube /usr/local/bin/
  rm minikube
  ```
