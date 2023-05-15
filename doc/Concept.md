# Comparison of three products: Minikube, Kind, K3d
---
# Introduction: Description of tools and their purpose
---
# Minikube
---
Minikube implements a local Kubernetes cluster on macOS, Linux, and Windows. Minikube's primary goals are to be the best tool for local Kubernetes application development and to support all Kubernetes features that fit.

## Features

minikube runs the latest stable release of Kubernetes, with support for standard Kubernetes features like:

- [LoadBalancer](https://minikube.sigs.k8s.io/docs/handbook/accessing/#loadbalancer-access) - using `minikube tunnel`
- Multi-cluster - using `minikube start -p <name>`
- [NodePorts](https://minikube.sigs.k8s.io/docs/handbook/accessing/#nodeport-access) - using `minikube service`
- [Persistent Volumes](https://minikube.sigs.k8s.io/docs/handbook/persistent_volumes/)
- [Ingress](https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/)
- [Dashboard](https://minikube.sigs.k8s.io/docs/handbook/dashboard/) - `minikube dashboard`
- [Container runtimes](https://minikube.sigs.k8s.io/docs/handbook/config/#runtime-configuration) - `minikube start --container-runtime`
- [Configure apiserver and kubelet options](https://minikube.sigs.k8s.io/docs/handbook/config/#modifying-kubernetes-defaults) via command-line flags
- Supports common [CI environments](https://github.com/minikube-ci/examples)

As well as developer-friendly features:

- [Addons](https://minikube.sigs.k8s.io/docs/handbook/deploying/#addons) - a marketplace for developers to share configurations for running services on minikube
- [NVIDIA GPU support](https://minikube.sigs.k8s.io/docs/tutorials/nvidia_gpu/) - for machine learning
- [Filesystem mounts](https://minikube.sigs.k8s.io/docs/handbook/mount/)

For more information, see the [official minikube website](https://minikube.sigs.k8s.io/)

# Kind
---
[kind](https://sigs.k8s.io/kind) is a tool for running local Kubernetes clusters using Docker container “nodes”.
kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

If you have [go](https://sigs.k8s.io/kind) ([1.17+](https://golang.org/doc/devel/release.html#policy)) and [docker](https://www.docker.com/) installed `go install sigs.k8s.io/kind@v0.18.0 && kind create cluster` is all you need!

For older versions use `GO111MODULE="on" go get sigs.k8s.io/kind@v0.18.0`.

kind consists of:

- Go [packages](packages) implementing [cluster creation](https://github.com/kubernetes-sigs/kind/tree/main/pkg/cluster), [image build](https://github.com/kubernetes-sigs/kind/tree/main/pkg/build), etc.
- A command line interface ( [kind](https://github.com/kubernetes-sigs/kind/tree/main/main.go) ) built on these packages.
- Docker [image(s)](https://github.com/kubernetes-sigs/kind/tree/main/images) written to run systemd, Kubernetes, etc.
- [kubetest](https://github.com/kubernetes/test-infra/tree/master/kubetest) integration also built on these packages (WIP)
  
kind bootstraps each “node” with [kubeadm](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/). For more details see the [design documentation](https://kind.sigs.k8s.io/docs/design/initial).

**NOTE**: kind is still a work in progress, see the [1.0 roadmap](https://kind.sigs.k8s.io/docs/contributing/1.0-roadmap).

# K3d
---
k3d is a lightweight wrapper to run [k3s](https://github.com/rancher/k3s) (Rancher Lab’s minimal Kubernetes distribution) in docker.

k3d makes it very easy to create single- and multi-node [k3s](https://github.com/rancher/k3s) clusters in docker, e.g. for local development on Kubernetes.

**Note**: k3d is a community-driven project but it’s not an official Rancher (SUSE) product. 

---
# Characteristics
---
## Supported Operating Systems
---
| Service 	| Supported OS 	| ARC support 	| Automation Capability 	| Additional functions 	|
|---	|---	|---	|---	|---	|
| Minikube 	| Linux, macOS, Windows 	| x86, x86_64, ARM 	| yes, configurable via CLI or configuration file 	| monitoring using the Kubernetes Dashboard, the ability to work with containers from Docker or CRI-O 	|
| Kind 	| Linux, macOS, Windows 	| x86, x86_64, ARM 	| yes, configurable via CLI or configuration filev 	| the possibility of working with containers from Docker, the possibility of automated generation of the Kubernetes configuration 	|
| K3d 	| Linux, macOS, Windows 	| x86, x86_64, ARM 	| yes, configurable via CLI or configuration file 	| the ability to work with containers from Docker, the ability to automatically generate the Kubernetes configuration, the ability to launch many Kubernetes clusters. 	|

# Advantages and disadvantages
---
## Minikube

**Advantages**:
- Easy to set up and use.
- Supports multiple hypervisors (VirtualBox, KVM, Hyper-V, etc.).
- Can be used for local development and testing.
- Provides built-in support for addons like dashboard, ingress, and heapster.
- Has a large community and active development.
**Disadvantages**:
- Limited scalability (it is designed for single-node clusters).
- Does not support advanced features like cluster autoscaling and federation.
- Limited support for network plugins.

## Kind

**Advantages**:
- Lightweight and easy to install.
- Supports multi-node clusters.
- Can be used for local development and testing.
- Provides better support for network plugins.
- Can be easily integrated into CI/CD pipelines.
**Disadvantages**:
- Requires Docker to be installed on the host machine.
- Limited support for addons and plugins.
- Limited support for cluster upgrades and rollbacks.

## K3d

**Advantages**:
- Lightweight and easy to install.
- Supports multi-node clusters.
- Provides better support for network plugins.
- Can be easily integrated into CI/CD pipelines.
- Can be run inside a Docker container.
**Disadvantages**:
- Limited support for addons and plugins.
- Limited documentation and community support.
- Some features are still in development.

# Conclusions
---
**Minikube** is a tool that is easy to use and supports a variety of operating systems. It has automation capabilities and a wide range of additional features, such as monitoring and managing a Kubernetes cluster. However, Minikube is suitable for testing microservices on a local machine, but not suitable for more extensive projects.

**Kind** is a more extensive tool compared to Minikube. Kind has the possibility of automation, ease of use and stability of operation. In addition, it provides convenient Kubernetes cluster management. However, Kind can be limited in that it does not support some features that may be necessary for certain projects.

**K3d** is a fast and lightweight tool that can be used to quickly create and test Kubernetes clusters. It has the possibility of automation, ease of use and a low level of resource consumption. However, K3d may be less stable compared to Minikube or Kind.

In general, it is recommended to use **Kind** for more extensive projects and solving more complex problems, and **Minikube** and **K3d** - for quick testing and prototyping.

# Conclusion
---
For this task I strongly recomend K3d solution. Because it provides much more advantages than other two.

# Demo
---
Install current latest release <br />
&emsp;&emsp;wget: &emsp;`wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash` <br />
&emsp;&emsp;curl: &emsp;`curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash` <br />
For creation cluster need to run command: <br />
&emsp;&emsp;`k3d cluster create <your_cluster_name>` <br />
After sucessfull claster creation, check cluster info: <br />
&emsp;&emsp;`kubectl cluster-info` <br />
Check cluster nodes: <br />
&emsp;&emsp;`kubectl get nodes` <br />
Run our test image on Kubernetes cluster <br />
&emsp;&emsp;`kubectl run <deployment_name> --image=<your_image>` 
Check created pod <br />
&emsp;&emsp;`kubectl get pods` <br />
Output the log from our container "Hello" <br />
&emsp;&emsp;`kubectl logs <deployment_name>` <br />
You can delete cluster <br />
&emsp;&emsp;`k3d cluster delete <your_cluster_name>`  <br />  
    
https://asciinema.org/a/584839          
