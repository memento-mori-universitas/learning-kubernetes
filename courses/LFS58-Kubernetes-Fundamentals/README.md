Kubernetes exposes an API using a local client called kubectl. The kube-schedule sees the request for running containers coming to the API and finds a suitable node to run that container in. 

Each node in the cluster runs two processes: a kubectl and a kube-proxy.

The kubectl manages any resources and watches over them on the local node while the kube-proxy creates and manages networking rules to expose to the container on the network.

Containers are not managed individually; they are part of a larger object called a Pod. A Pod consists of one or more containers which a share IP address, access to storage and namespace.

Orchestration is managed through a series of watch-loops or controllers. Each controller is in charge of keeping the desired state of the node.

A Deployment ensures resources are available, such as IP address and storage and then deploys a Replica Set.

The Replica Set is a controller that restarts/deploys containers until the desired number is achieved.

To managed thousands of nodes we can use labels as identifies which avoids knowing the node IP address.

### Installing and Configuration

Once we have minikube and kubectl, we can use kubeadm to create our first cluster. Prior to initializing the Kubernetes cluster, we must choose a network to avoid IP conflicts.

- Calico 
  A flat Layer 3 network which communicates without IP encapsulation, used in production with software such as Kubernetes, OpenShift, Docker, Mesos and OpenStack. Viewed as a simple and flexible networking model, it scales well for large environments. Another network option, Canal, also part of this project, allows for integration with Flannel. Allows for implementation of network policies.
  
- Flannel
  A Layer 3 IPv4 network between the nodes of a cluster. Developed by CoreOS, it has a long history with Kubernetes. Focused on traffic between hosts, not how containers configure local networking, it can use one of several backend mechanisms, such as VXLAN. A flanneld agent on each node allocates subnet leases for the host. While it can be configured after deployment, it is much easier prior to any Pods being added.
  
- Kube-router
  Feature-filled single binary which claims to "do it all". The project is in the alpha stage, but promises to offer a distributed load balancer, firewall, and router purposely built for Kubernetes.
  
- Romana 
  Another project aimed at network and security automation for cloud native applications. Aimed at large clusters, IPAM-aware topology and integration with kops clusters.
  
- Weave Net 
  Typically used as an add-on for a CNI-enabled Kubernetes cluster.
  
### Main Deployment Configurations

Four main deployment configurations:
- Single-node
- Single head node, multiple workers
- Multiple head nodes with HA, multiple workers
- HA etcd, HA head nodes, multiple workers
