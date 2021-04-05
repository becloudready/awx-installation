# AWX-Installation
> This repo provides the details how to install to AWX in Kubernetes.

# Prerequisites
* A Kubernetes Cluster.
* A Kubectl CLI Tool.

# Step: 1
## Clone the AWX GitHub repository
> git clone https://github.com/becloudready/awx.git
>
> cd awx
>
> git checkout -b branch-17

# Step: 2
* Now go inside the installer directory
> cd installer
* Edit the following values in the inventory file.
> kubernetes_context=Your context name #You can find this in kubeconfig file
>
> kubernetes_namespace=Your namespace # You can give any name for namespace
>
> kubernetes_web_svc_type=NodePort
