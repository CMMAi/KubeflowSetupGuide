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
  * Start Minikube
   ```
   minikube start --vm-driver=none --cpus 6 --memory 12288 --disk-size=120g --extra-config=apiserver.authorization-mode=RBAC --extra-config=kubelet.resolv-conf=/run/systemd/resolve/resolv.conf --extra-config kubeadm.ignore-preflight-errors=SystemVerification
   ```
#### Installation of Kubeflow
1. Download the kfctl [here](https://github.com/kubeflow/kfctl/releases)
2. Unpack the tar ball: ```tar -xvf kfctl_v1.0.2_<platform>.tar.gz```
3. Edit your .bashrc or .zshrc or any others shell confige file like this:
 ```
 export PATH=$PATH:<path to where kfctl was unpacked>
 export KF_NAME=<your choice of name for the Kubeflow deployment>
 export BASE_DIR=<path to a base directory>
 export KF_DIR=${BASE_DIR}/${KF_NAME}
 export CONFIG_URI="https://raw.githubusercontent.com/kubeflow/manifests/v1.0-branch/kfdef/kfctl_k8s_istio.v1.0.2.yaml"
 ```
 ```
 mkdir -p ${KF_DIR}
 cd ${KF_DIR}
 kfctl apply -V -f ${CONFIG_URI}
 ```
 #### Launch of Kubeflow central dashboard
 * Set the environment variables in your .bashrc or .zshrc or any others shell confige file like this:
  ```
  export INGRESS_HOST=$(minikube ip)
  export INGRESS_PORT=$(kubectl -n istio-system get service istio-ingressgateway -o jsonpath='{.spec.ports[?(@.name=="http2")].nodePort}')
  ```
 * then you could get the deployment url by ```echo http://$INGRESS_HOST:$INGRESS_PORT```
 
 #### For more detail, please checkout https://www.kubeflow.org/docs/started/workstation/minikube-linux/
