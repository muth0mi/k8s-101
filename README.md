# A soft introduction to kubernetes deployment
This guide presumes you are comfortable with docker containerization and explains how to get your images spinning on a k8s environment.


## Prerequisites
1. Kubectl
1. Minikube
1. Virtualbox - This will supply the hypervisor to minikube to create vm on. [Alternatives](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)


## Installation
[Kubectl](https://kubernetes.io/docs/reference/kubectl/kubectl "Kubectl detailed guide") is a Kubernetes command-line tool that allows running commands against Kubernetes clusters.
You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs. 

[Minikube](https://kubernetes.io/docs/setup/learning-environment/minikube) is a tool that makes it easy to run Kubernetes locally. 
Minikube runs a single-node Kubernetes cluster inside a Virtual Machine (VM) on a PC for users looking to try out Kubernetes or develop with it day-to-day.
For more demanding usage, [consinder running kubernetes on bare metal](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/).

### Steps
1. `# pacman -S kubectl`
1. `# pacman -S minikube`
1. `# pacman -S virtualbox`


## Launch minikube
* To launch a minikube [cluster](https://kubernetes.io/docs/reference/glossary/?all=true#term-cluster) execute `$ minicube start`
* To launch with custom hypervisor `$ minikube start --driver=docker`
* To set default hypervisor `$ minikube config set driver docker`. Virtualbox is the default in a fresh setup  
* To delete cluster `$ minikube delete`
* To open the k8s dashboard, run `$ minikube dashboard`


## Basics
Pods are the building blocks of a k8s system. Sort of like images to docker, well, or atoms to an element. 
A pod hosts and manages one or multiple containers.

Replication controllers manage behaviour of pods in terms of creating, deleting, healing, etc

A deployment is a special ( on steroids ) replication controller that allows updates and rollbacks of deployed pods more systematically.

A service exposes a pod, Replication controllers or deploymenent to the external world or to a different node within the cluster. Services have a static IP and communicate to pods using [Labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels). 


## Deploy an application
1. Apply the deployment to your cluster
   `kubectl apply -f /path/to/deployment.yml`
1. Create a service for the deployment
   `kubectl create -f /path/to/service.yml`
1. Run the application by visiting `http://<cluster-ip>:<nodePort>`


#### This guide works only for monolithic application and is not production certified. This is for the most part educational and doesn't consinder the nitty gritties of deployment.
