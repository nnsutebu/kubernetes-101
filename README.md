## 1. Why do companies adopt Kubernetes?
- Companies adopt kubernetes for various reasons:
- Container Orchestration: simplifies the management, deployment, scaling of your containerized applications
- Service Discovery, autoscaling and Load Balancing: where applications can be automatically discovered by other services, scaled up or down based on demand, and distributed
- Simplifies deployments: supports different deployments strategies, Rolling Update & Rollbacks,  release new versions of applications and to revert to previous versions if needed
- Storage Orchestration, Self-Healing, Secrets and Configuration Management: inbuilt mechanism for healing, managing storage and securing sensitive information
- Multi-Cloud and Hybrid Cloud Support: supports deployment across omprem and multicloud environments
- Role-Based Access Control (RBAC): Pods and Multi-Container SupportMonitoring and Logging** intergrates various monitoring tools to perform health checks
- Highly available and has self healing capabilities**: scale up and down based on workloads and helps your application beacome resilient. If a container fails it is restarted over and over
## 2. Difference between configmap and secret and how, when would you use them?
- Secrets: is used to store sensitive data, such as passwords, API keys, or SSL certificates. stored in Base64-encoded format
- Config: map is Used to store non-sensitive configuration data, such as application settings, environment variables, or configuration files.
- ConfigMap data is stored as plain text and can be easily accessed by the pods.
Useful for storing application-specific configuration that needs to be shared across multiple pods.
## 3. Difference between stateful and daemonset and how, when would you use them?
- Daemonsets: are objects running on all nodes and are responsible for monitoring and logging, network plugins 
- statefulsets: are objects used for applications that require persistance storage and a stable network identity.
## 4. Difference between replicaset and deployments, how, when would you use them?
- Replica set: Ensures that a specified number of pod replicas are running at all times. Used fo scaling pods
- Deployment: Manages the lifecycle of pods, including rolling updates, rollbacks, and scaling.
## 5. Difference between affinity, taints and tolorations, how, when would you use them?
- Affinity: specifies how  pods are scheduled on specific nodes based on the properties of the nodes, such as labels or node attributes.
- Taints:  mark or prevent certain pods from being scheduled on certain nodes based on properties
- Tolorations: allows certain pods to be scheduled on nodes with specific taints
## 6. Difference between init container and sidecar, how, when would you use them?
- Init containers: used for task like downloading files, running database migrations, setting up configuration before the application starts
- sidecars: used for logging, monitoring and proxying network traffic
## 7. Difference between iliveness and readiness, how, when would you use them?
- Liveness probe: checks if the container is running and healthy. Useful for dettecting and recovering apps crashes or dreadlocks
- Readiness probe: checks if the container is ready to start accepting traffic
8 ## What is a namespace and how, when would you use them?
Provides a way to divide your cluster in between multiple users and teams
## 8.Have you worked with storage and what type of storage have you provisioned?
- Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) for provisioning static and dynamic storage volumes.
- Local storage for applications that require fast, low-latency access to data.
Network-attached storage (NAS) or Storage Area Network (SAN) volumes for larger, shared storage needs.
- Cloud-provider-specific storage solutions, such as Amazon EBS, Google Persistent Disk, or Azure Disks.
## 9.What policies are present in persistent volume claims?
- Access Modes: Defines how the volume can be accessed, such as ReadWriteOnce, ReadOnlyMany, or ReadWriteMany.
- Storage Class: Specifies the type of storage to be provisioned, such as SSD or HDD.
Volume Modes: Defines whether the volume should be formatted as a filesystem or used as a raw block device.
- Reclaim Policy: Specifies what should happen to the underlying Persistent Volume when the PVC is deleted, such as Retain, Recycle, or Delete.
- Volume Binding Mode: Specifies when volume binding and dynamic provisioning should occur.
## 10. what volume access modes with volumes?
- ReadWriteOnce (RWO): The volume can be mounted as read-write by a single node.
- ReadOnlyMany (ROX): The volume can be mounted as read-only by multiple nodes.
- ReadWriteMany (RWX): The volume can be mounted as read-write by multiple nodes.

2 TYPES OF RETAIN POLICIES: 
Retain:
Release:
Status:
Bound: means volume has been attached or attributed to a pvc
Release: means volume has been release from that pvc
Restart Policy:
Maxsure:
maxUnavailable:

## 11. Where is the location of the config? 
etc/kubernetes/manifest
## 12. What are kubernetes objects or resourceses? kubectl api-resources
- Cluster: A set of nodes (machines) that run containerized applications managed by Kubernetes.
- Node: A single machine (virtual or physical) in a cluster that runs Pods
- Pods: The basic unit of deployment in Kubernetes, containing one or more containers.
- Services: Provide a stable network endpoint for a set of Pods.
- Service Accounts: Provide an identity for processes running in Pods.
- Liveness:  checks if a container is still running; if it fails, the container is restarted.
- Readiness: checks if a container is ready to serve traffic; if it fails, the Pod is removed from the Service endpoints.
- Replicaset: Ensures a specified number of Pod replicas are running at all times.
- Daemonset: Ensures a copy of a Pod runs on every node (or a subset).
- Deployment: Manages the lifecycle of pods, including rolling updates, rollbacks, and scaling.
- request: The minimum amount of CPU or memory guaranteed to a container.
- limit: The maximum amount of CPU or memory a container is allowed to use.
- Affinity: specifies how  pods are scheduled on specific nodes based on the properties of the nodes, such as labels or node attributes.
- Taints:  mark or prevent certain pods from being scheduled on certain nodes based on properties
- Tolorations: allows certain pods to be scheduled on nodes with specific taints,
- Resource Quotas: Limit the total resources consumed by all Pods in a namespace.
- Persistent Volumes (PVs): Provide storage to Pods, independent of the Pod's lifecycle.
- Persistent Volume Claims (PVCs): Requests storage resources, which are then bound to PVs.
- Endpoints: Provide the IP addresses and ports for a Service.
- ConfigMaps: Provide configuration data to Pods.
- Secrets: Store sensitive data such as passwords, tokens, or keys.

## 13. How does admission controller worker?
- The Kubernetes API server is the central control plane component that exposes the Kubernetes API. When a user or controller submits a request to the API server, it goes through a series of admission controllers, which are pluggable components that can modify or validate the request before it 
is processed. Admission controllers are used to enforce various policies and validations, such as resource quotas, security constraints, and more.
## 14. How does the Api server validates users: 
Api server validates identity of users using different authentification and authorization mechanisms. 
For authentification: the API validates user identity and incoming request using via Json web token, x509.certificates, oidc processes, username & password
For authorization: the api applies the authorization mechanism which is admission control which are your plugable modules, RBAC roels, Node authorizers
## 15. How would you install Kubernetes on prem in air gap environment?
Air gab environments are isolated environments with no network or internet access similar to the private subnets with isolated environments. 
Prepare the infrastructure: identifying the machines to host cluster making sure they meet theb requirement and that the network is isolated
- Download the Kubernetes binaries (e.g., kubectl, kubeadm, kubelet)from a trusted source and transfer them to the air-gapped environment using removable media.
- store them in a private container registry within the air-gapped environment.
- Deploy and configurea private container registry, such as Docker Registry or Harbor, within the air-gapped environment.
- Load the required Kubernetes component images into the private registry.
- Use the kubeadm tool to initialize the Kubernetes control plane on one of the prepared nodes.
- Ensure that the kubeadm command references the local container registry for the Kubernetes component images.
- Use the kubeadm tool to join additional nodes to the Kubernetes cluster.
- Establish secure procedures for updating Kubernetes components and container images within the air-gapped environment.
- Regularly backup the Kubernetes configuration and store the backups in a secure, offline location.
- Implement strict access controls and auditing for the Kubernetes cluster within the air-gapped environment.
## 16. what is your process of setting up a kubernetes cluster?
- created federated access token for the repo
- created a bucket, dbtable to store and lock state
- created a terraform module with add-ons
- create a workflow that automates the deployment 
## 17. How do you install Kubernetes in an environment without internet?
## 18. How do you configure your images to get into that environment?
- Transfer the container images to the air-gapped environment using a secure, offline method, such as copying them to a removable storage device (e.g., external hard drive, USB drive).
- Deploy a private container registry within the air-gapped environment, such as Docker Registry or Harbor.
- Load the Kubernetes container images into the private registry.
- Configure the private registry to use appropriate network settings
## 19. What type of node groups did you use to provision clusters? 
- Ec2instances, Fargate, EKS
## 20. What type of experience do you have with open shift?
## 21. What are cgroups in Linux?
-cgroups (short for control groups) are a Linux kernel feature that allows you to limit, isolate, and monitor the resource usage (like CPU, memory, disk I/O, and network) of a group of processes.
They are essential for container runtimes (like Docker and Kubernetes) to enforce resource constraints and ensure that no single container or process hogs the system.
## 22. How do you enable logs in a cluster?
- setting up namespace-level logging, which can help with troubleshooting and auditing.
## 22. What are the steps you take before upgrading a cluster?
- Backup the Cluster: Perform a full backup of the Kubernetes cluster, including the API server, etcd, and any persistent volumes.
- Test the Upgrade: Perform the upgrade in a non-production environment first to ensure it works as expected.
- Review Deployment Manifests: Ensure that all Kubernetes object manifests (Deployments, StatefulSets, etc.) are up-to-date and compatible with the new Kubernetes version.
- Coordinate with Stakeholders: Communicate the upgrade plan and timeline with all stakeholders to ensure minimal disruption.
- Perform the Upgrade: Follow the appropriate upgrade process for the Kubernetes distribution (e.g., kubeadm, kops, EKS) to upgrade the cluster.
-Monitor the Upgrade: Closely monitor the cluster during and after the upgrade to ensure everything is functioning as expected.
# Kubernetes Version Rollback:
- Kubernetes does support version rollbacks, but the process can be complex and may involve downtime. The general approach would be:
- Backup the Cluster: Perform a full backup of the Kubernetes cluster before attempting the rollback.
Identify the Target Version: Determine the specific Kubernetes version to which you want to roll back.
- Prepare the Rollback: Ensure that all Kubernetes object manifests are compatible with the target Kubernetes version.
- Perform the Rollback: Follow the appropriate rollback process for the Kubernetes distribution, which may involve manually downgrading components or using a tool like kubeadm.
- Verify the Rollback: Thoroughly test the cluster after the rollback to ensure everything is functioning correctly.
## 23. Can you roll back a Kubernetes version?
 that rolling back Kubernetes can be a complex and risky process, and it's generally recommended to avoid it if possible by carefully planning and executing upgrades.
## 24.What are the authentication and authorization mechanism in kubernetes?
**Authentication:** Api server validates identity of users using different methods: bearer tokens, x509.certificates, oidc processes, https
The API server supports several authentication methods, including:
- X.509 Client Certificates: The API server can verify the identity of users or client applications using X.509 client certificates.
- Bearer Tokens: The API server can authenticate users or client applications that present a valid bearer token, such as a JSON Web Token (JWT).
- HTTP Basic Authentication: The API server can authenticate users using a username and password.
- OIDC (OpenID Connect): The API server can integrate with an external OIDC-compliant identity provider to authenticate users.
The API server is configured to accept one or more of these authentication methods, and it will use the configured method(s) to verify the identity of the incoming request.
**Authorization:** authorization is done using rbac, node authorizer, webhook, 
After a user or client application is authenticated, the API server will authorize their access to resources based on the user's or application's permissions.
-Kubernetes uses several built-in authorization modules, including:
-RBAC (Role-Based Access Control): The RBAC system allows cluster administrators to define roles with specific permissions, and then assign those roles to users, groups, or service accounts.
-Node Authorizer: The Node Authorizer is responsible for authorizing node-related operations, such as allowing nodes to retrieve their configuration or report their status.
-Webhook Authorizer: The Webhook Authorizer delegates authorization decisions to an external service, allowing for custom authorization policies.
The API server will apply the appropriate authorization module(s) to determine whether the authenticated user or client application has the necessary permissions to perform the requested operation.
**Attribute-Based Access Control (ABAC):**
In addition to the built-in authorization modules, Kubernetes also supports Attribute-Based Access Control (ABAC), which allows administrators to define access policies based on the attributes of the user, resource, or environment.
ABAC policies can be used to implement more fine-grained access control, such as restricting access based on the user's role, the namespace of the resource, or the time of day.
**Admission Control:**
The API server also employs admission control, which is a set of pluggable modules that can intercept and modify requests before they are processed by the API server.
Admission controllers can be used to implement additional validation, mutation, or policy enforcement rules, such as requiring certain labels or annotations on resources.
**Audit Logging:**
The API server generates audit logs for all incoming requests, which can be used for security monitoring, compliance, and troubleshooting.
The audit logs record information about the request, including the user, resource, and action performed, as well as the outcome of the request.
## Are you familiar with the concept of boast trapping?
- refers to the initial setup of control plane and worker nodes, and configuring cluster components securely and reliably.
## What are the concepts, prequiste for rke2 cluster or clusters in kubernetes?
## How do you set and configure the config yaml file in the boost strapping process?
- The config.yaml file is placed at /etc/rancher/rke2/config.yaml. It defines key cluster parameters.
## How would you enable auditing within the rke2 cluster? 
## you have 3 directorys a, b, c and you are in directory a, how do you move files from directory a to b to c with out changing directpries
     mv file.txt ../b/ && mv ../b/file.txt ../c/
# How do you set up an inventory in ansible? Say you have a playbook you want to run
# Have you worked with endpoints? How are endpoints used in kubernetes?
- Endpoints are created by Services. They list Pod IPs the Service routes to. For example, if a Service selects 3 Pods, it creates an endpoint list pointing to their IPs and ports.
Endpoints enable:
- Internal load balancing
- DNS-based resolution (my-service.namespace.svc.cluster.local)

Service discovery in microservices
# Do you have experience setting prewebhook and validating webhook?
- These are admission controllers used to:
Mutate: Add default labels or annotations before saving the object.
Validate: Enforce policies (e.g., deny Pods without resource limits).

Used commonly with tools like Kyverno or Open Policy Agent (OPA) Gatekeeper.
# what is one thing you were working on that you couldn't resolve?
# Do you have experience with network policies? How would you 
- implemented Kubernetes Network Policies to control Pod traffic.
# How would you configure your readiness, liveness, security scanning, LDAP for MAF, PSA, PDI should be enforced, ensureing containers should run as root probes?
Use external OIDC provider (e.g., Keycloak or Dex) integrated with LDAP for user auth. Set RBAC via Kubernetes RoleBindings.
Resource Types
🚨 Note: You should follow this ordering (and this is the order they are covered in the video course) <<<<<<< HEAD -Certificate Authority: trusted root of all certificates in the cluster allows components to validat each ordeer

Controller, scheduler manager and Kubelet all have a client certificate and communicate with Apiserver who has the server certificate ======= static pods When making a kubectl how does the kubectl authenticates who you are? it speaks to the kubecongif when making a a kubectl what happens in the background your kubeconfig file has certificates,
14aca8cb0b282e30dceb7b1d970bb9e82a4b5c89

# Namespace: Provides a way to divide cluster resources between multiple users.
# Pod: The smallest and simplest Kubernetes object. Represents a set of running containers on your cluster.
# ReplicaSet: Ensures that a specified number of pod replicas are running at any given time.
# Deployment: Manages lifecycle of pods, providing features such as replicasets, rolling updates and rollbacks.
# Service: Defines a logical set of pods and a policy by which to access them.
# Job: Creates one or more pods that run to completion.
# CronJob: Schedules jobs to run at specified times or intervals.
# DaemonSet: Ensures that a copy of a pod runs on all (or some) nodes in the cluster.
# StatefulSet: Manages stateful applications, providing guarantees about the ordering and uniqueness of pods.
# ConfigMap: Store configuration data that can be consumed by pods.
# Secret: Manages sensitive information, such as passwords, OAuth tokens, and ssh keys.
# Ingress: Manages external access to the services in a cluster, typically HTTP.
# GatewayAPI: Manages traffic routing within the cluster, providing advanced routing capabilities.
# PersistentVolume and PersistentVolumeClaim: Manages persistent storage for pods.
# RBAC (Role-Based Access Control): Manages permissions within the cluster.
Out of Scope Resource Types
- LimitRange: Specifies resource constraints for resources within a namespace.
- NetworkPolicy: Controls the network traffic flow at the IP address or port level within the Kubernetes cluster.
- MutatingWebhookConfiguration: Defines webhooks that can mutate incoming requests to the Kubernetes API server.
- ValidatingWebhookConfiguration: Defines webhooks that can validate incoming requests to the Kubernetes API server.
- HorizontalPodAutoscaler: Automatically scales the number of pods in a deployment or replica set based on observed CPU utilization or other custom metrics.
- CustomResourceDefinition: Allows users to define their own resource types and make the Kubernetes API server handle them (covered in a later section!).

## MONOLITHIC ARCHITECTURE:are monolithic stacks
design approach where application stacks that are developed, tightly coupled and deployed as a single unit or codebase. What does that mean? All components are part of a single application Frontend, logic and backend. <<<<<<< HEAD The Applications shares the same memory space Examples of monolith stacks ======= The Applications share the same memory space

## Examples of monolith stacks
14aca8cb0b282e30dceb7b1d970bb9e82a4b5c89 LAMP: Linux, web server, Mysql MEAN: nosql, expressjs, Angular, Nodejs JEE: Java, Spring, Tomcat/Jboss/Wblogic, Mysql Django Stack: Python, Django, PostgreSQL

## Benefits:
Easy for small teams to develop and test Doesn't require complex networking and has a lower overhead Has only only a few points of entry

## Cons
Require the whole application to be deployed Doesn't scale well if parts of the application breaks Diffcult to update all application dependecies and libraries

## MICROSERVICE ARCHITECTURE;
is a design approach where different parts of an application stack are developed seperately, decoupled, deployed as a microservices, operates independently. Applications communicate with each other using well-defined APIs and services and each microservice

## Benefits
can deploy without impacting other services Easie to update software versions of dependencies Increased fault tolerance

## KUBERNETES
is an open-source container orchestration platform designed for automating the deployment, scaling, and management of containerized applications.

Alternatives to KUBERNETES: Apache Mesos, Openshift, Nomad, Juju, Tanzu, IBM, AKS, EKS, GCP, Suse rancher,
- Cluster orchestration: gcloud, ekctl, kubectl, aksctl
- Container platform: Podmad, docker

Pod: smallest deployable unit in kubernetes, represents a collection of one or more containers running in your cluster

Node: smallest fundamental unit of computing hadware, represent single machines in cluster and status of a node staust contains adderss, condition, capacity and info <<<<<<< 

HEAD Containers: Light weight isolated environments that comprises an application and it dependencies
Container runtime: software responsible for managing and running containers on a host system 
-Cluster: group of nodes that work together to run containerized apps and manages the underlying infrastructure
- Container orchestration: process of managing containers in a distributed environment Cluster: group of nodes that work together to run containerized apps and manages the underlying infrastructure 
- Heapster: performance monitoring and metrics collection system for data collected by kublet. - 

## Master Nodes
Master nodes: manages, plans, schedules, monitors all activities within the cluster, communicates with worker nodes to ensure all applications in the cluster are running smoothly. comprised of
- Etcd: Keyvalue database that stores cluster information mostly in Json, Yaml format. 
- Scheduler: Assigns pods to new Nodes based on resource availability. 
- Api-server: gateway/entry-point in to the Kubernetes cluster, processes, handles API request from users, applications and other components to interact with the cluster. authenticates, authorizes and validates request handling CRUD create read update and delete operations.
- Controller manager: Ensures the desired state of the cluster by making sure a specific number of pods are running. Runs various controllers like the 
   >>Node controller: monitors and manages the health of nodes, 
   >>Replication controller: ensures specific number of pods are running at all times 
   >>Namespace controller: creates and manages namespaces in cluster 
   >>Job controller: Manages batch or on-time jobs that run to completion 
   >>Deployment controller: manages deployment and scaling of applications 
   >>Endpoint controller: manages endpints withservices Api-server: gateway/entry-point in to the Kubernetes cluster, processes, handles API request from users, applications and other components to interact with the cluster. authenticates, authorizes and validates request handling CRUD create read update and delete operations.

- Containers: Light weight isolated environments that comprises an application and it dependencies
- Container runtime: software responsible for managing and running containers on a host system
- Container orchestration: process of managing containers in a distributed environment

## Worker Nodes
Worker nodes: runs the containers and executes the workloads- comprised of
- Kubelet: Agent, monitors and manages the pods state, replaces failed pods
- Containerd engine: runtime environment for our container, responsible 4 creating and managing containers
- Kubeproxy: Manages communication between Pods and the external world. Maintains network rules for load balancing and routing.

KUBERNETES STABDARD INTERFACE
- Container interface: used to execute and run container processes within the kube system. examples containerd, cri-o

- Container network interface: defines how container network is setup and defined in the kubernetes ecosystem such calico, Flannel, cilium, AWSVPC plugin, Azure CNI, GPC CNU

- Container storage interfaces: standard interface to provide durable persistent storage to containers. Examples EBS CSI-driver, Secrets store CSI-driver, Azure Disk SCI-driver

- Kubeconfig: stored in ~/.kube/config contains information about cluster, user credentials, certfificates and context

- Service files: contains information about networking such as clusterIP, NodePort, Loadbalancer, Selectors

- Deployment files: defines the desired state of deployment, pod replicas, container images and resource limits

- Config maps- stores application config files in plain format kubectl create configmap myconfigmao --from literal=env=dev

Use cases: create env variables

Secrets: stores sensitive data like Password, API keys, in an encrypted format echno -n 'name you want to encode' | base64 echo -n 'admin' | basecode 64 echno -n 'snap' ./ password.txt kubectl create secret generic mysecret --from=file=./username.txt --from=./password.txt

<<<<<<< HEAD

>>>Deployment: manages lifecycle of aplications including deployment, scaling, rollingout(gradually updaing the application), rollback reverting back to a preious version) 
>>>Replica set: ensures a specific number of pods are running and it's used for scaling
>>>Daemon set: objects that are ran on every node in a cluster and are used for logging, monitoring . 
>>>Stateful set: objects that manages stateful applications requiring persistent storage, network identities such as database, message queries =======

>>> Headless service: manage network access to a set of Pods without using the standard load-balancing features. a headless service provides DNS records that map to the individual Pods. Enables direct communication between Pods, such as with StatefulSets
Sidecar: specialized containers that run to completion before the main application containers in a Pod start.
>>> Init container:
Useful: when we want to perform data migration or pre-processing tasks before the application starts. Labels: used to identify and group resources

>>> Selectors: are used to query and select resources based on their labels Pod selector: selecting a group of pods based 
- Equity based selector: select resources based on certain criteria that are equitable or balanced. 
- Equality based selector: feature for selecting resources based on exact label values or simple logical conditions. Node selectors: Service account: used to grant access permission to pods and apps in your cluster enabling apps to interract with th API server usecases: grant specific permissions, run applications with different roles

## 4 resources under RBAC role based acess control authorization mechanism
- Cluster binding: granting persmission and access right with in cluster
- Role binding: granting permission and access right with in namespace
- Roles: set of rules that define permissions and access rights to specificed resources within namespace
- Cluster role: used to grant permission to users to manage resources inthe cluster
- Service: provides stable identity and endpoint that other apps can use to intereact
- Liveness probe: checks the health of the container and restarts the container
- Readiness probe: determines when to start accepting traffic


## DEPLOYMENT TYPES:
- Rollbacks: reverting to previous stable state after an update has introduced issues or failures

- Rolling updates; default deployment replaces old pods with new ones ensuring a number of pods are available and healthty at all times

- Blue-green deployment: traffic is redirected from the prod to new green env and can be switched back

- Canary deployment: allows you to test a subset

VOLUMES: used to provide persistent staorage for containers

- ReadWriteOnce (RWO) – The volume is mounted with read-write access for a single Node in your cluster. Any of the Pods running on that Node can read and write the volume’s contents.

- ReadOnlyMany (ROX) – The volume can be concurrently mounted to any of the Nodes in your cluster, with read-only access for any Pod.

- ReadWriteMany (RWX) – Similar to ReadOnlyMany, but with read-write access.

- ReadWriteOncePod (RWOP) – This new variant, introduced as a beta feature in Kubernetes v1.27, enforces that read-write access is provided to a single Pod. No other Pods in the cluster will be able to use the volume simultaneously.

## TYPES OF VOLUMES:
- local – Data is stored on devices mounted locally to your cluster’s Nodes.

- hostPath – Stores data within a named directory on a Node (this is designed for testing purposes and doesn’t work with multi-Node clusters).

- nfs – Used to access Network File System (NFS) mounts.

- iscsi– iSCSI (SCSI over IP) storage attachments.

- csi – Allows integration with storage providers that support the Container Storage Interface (CSI) specification, such as the block storage services provided by cloud platforms.

- cephfs – Allow the use of CephFS volumes.

- fc – Fibre Channel (FC) storage attachments.

- rbd – Rados Block Device (RBD) volumes.

- PV are cluster wide storage resources/objects that allow pods to access storage from defined device

- PVC. request for storage resources used to mount persistent volume into a Pod. such as Elasticblock, Azure Disk, Vsphere volume and CSI driver

- Network policies: define rules that specify how pods communicates and other endpoints

- Ingress: manages external access to services provides LB, HTTP routes, SSL terminations

- ingress rules: defines how traffic is allowed into selected pods

- Egress rules: deifnes how traffic is allowed to flow out of the selected pods

- TLS referes to transport Layer security

- NGINX INGRESS CONTROLLER managing and routing incoming HTTP and HTTPS traffic to services within the cluster. NGINX Ingress Controller uses NGINX as the underlying reverse proxy and load balancer, providing features like host-based routing, path-based routing, TLS termination,

- EGRESS controlled and filtered to restrict access to external resources or enforce security policies.

- SET MANAGER: assigns certificates to applications

VERTICAL POD AUTOSCALER: adjusts the CPU and memory resource requests of pods based on their resource usage patterns. VPA helps optimize resource allocation by dynamically scaling the resource requests of pods to match their actual resource utilization.

HORIZONTAL POD AUTOSCALER: number of pod replicas based on observed CPU or custom metrics. HPA helps scale applications horizontally by increasing or decreasing the number of pod replicas in response to changes in resource utilization HPA

## SERVICES IN KUBERNETES
- SERVICES: abstraction that defines a logical set of pods and policy by which to access them.
- ClusterIP: Exposes the service within the cluster, makes it reachable only within cluster
- NodeIP: Exposes the service through a static port on each node
- Loadbalancer: Exposes the service using a loadbalancer to evenly distrbute traffic
- External name: Services will be mapped to a DNS name.
- Ingress

HEADLESS SERVICE: enables you to reach ports without accessing via proxy.
NETWORKING IN KUBERNETES
Networking: CNI stands for container network interface, manages the way pods and containers connect to the network. Different flavours of CNI's such as Calico, Flannel, Weavenet, Antrea, Tigera Seucure, Mellanox VDPA, kube router
Calico: open-source
Flannel: CNI plugin that uses layer 3 networking
Weave: CNI plugin that provides scalable, networking policies
Cilium: best CNI plugin, provides best security, observability and good for complex clusters
Kube-router: lightweight CNI plugin Loadbalancer with loadbalancing features and network policiess
<<<<<<< HEAD

 ## WHY USE CALICO? Provides
-Advanced networking policies: define fine-frained networking policies and rules over containers based on labels, ports Scalability: Handles large clusters with ease Cross-Cluster networking: has the capacity to connect multiple clusters together Border Gateway Protocol routing: supports BGP routing good for onprem Security: encrypts network traffic so only authoriszed pods can communicate with respective pods
## WHY use CALICO? Provides
Advanced networking policies: define fine-frained networking policies and rules over containers based on labels, ports
Scalability: Handles large clusters with ease
Cross-Cluster networking: has the capacity to connect multiple clusters together
Border Gateway Protocol routing: supports BGP routing good for onprem
Security: encrypts network traffic so only authoriszed pods can communicate with respective pods
14aca8cb0b282e30dceb7b1d970bb9e82a4b5c89

## VOLUMES KUBERNETES
- Ephemeral means if containers are restarted they would loose their data and it requires persistance

- EmptyDir: used to share volumes between multiple containers within a pods Data is stored in volumes that reside inside the Pods only

- hostPath: helps access data of the pods or container volumes from the host machine Replicates data of the volumes on the host machine, if changes on the host are made, it is refelcted on the pods volumes

- Persistent volume: process of storing data in the Cloud such as EBS, Azure disk To get a Persistent volume, you need to claim the volume via the help of of a Persistent Volume Claim

## Liveness Probe in KUBERNETES
- LivenessProbe: used to check the health of your application by specifying that in the manifest file. A 0 output of livenessProbe means the application is running perfectly LivenessProbe repeats the process after seconds or minutes Liveness Probe also recreates pods when it detects the application health checks are unevenly yoked
ConfigMaps and Secrets in KUBERNETES

-ConfigMap: used to store configuration data which is non-confidential in key-value pairs by decoupling the application to get rid of the hard-corded values

- Secrets: stores sensitive info such as password, API keys, TLS certificate. Provides extra layer of security encodes and decodes using base64-encoded format Can be mounted in volumes in pods is a feature that encrypts data stores sensitve data up to 1MB

- KUBERNETES JOBS
Jobs are used to run workloads, log rotation, batch processes, backup scripts. Key features of the Jobs: ● One-time Execution: If you have a task that needs to be executed one time whether it’s succeed or fail then the job will be finished. ● Parallelism: If you want to run multiple pods at the same time. ● Scheduling: If you want to schedule a specific number of pods after a specific time. ● Restart Policy: You can specify whether the Job should restart if fails

- SECURITY IN KUBERNETES
Apply security updates Restrict access to ETCD implement network segmentation and define policy rukes implement vulnerability scanning Define resource quota and limits use images from authorized repos only

- KUBERNETES POD LIFECYCLE There are multiple types of states for the Pod lifecycle that we will discuss here:

Pending: When a pod is created it has to go through the pending status in which Master nodes allocate the nodes to where to create the pod. The pods will remain in the pending state until all the necessary resources are allocated such as CPU, memory, and storage.
Running: Once the pod has been scheduled to a node, it comes into the Running Status. Once the pod comes into a running state, the containers within the pods will be creating and doing the tasks that have been provided in the manifest file.
Succeeded: Once the pods have completed their task then, the pods come in the succeeded state and then terminates.
Failed: Once the pods intend to create but due to some issues the pods are not creating and showing the Failed state leads to issues with the configurations which need to be addressed by the creator of the file.
CrashLoopBackOff: This is the advanced state of a Failed state where the container is crashing and restarts. To fix this issue, the creator of the file needs to check the manifest file.
Unknown: In some cases, the Kubernetes may lose the connection with the nodes to create the pods that show the unknown status of the particular pod.
Termination: When a pod is no longer available it comes in the termination process. Once the pod is deleted, it can not restart again the same pods and is removed from the entire Kubernetes cluster.
There are some conditions that come under while creating Pods:

● Initialized: This condition shows whether all the init containers have started successfully or not. If the status is false it means the init containers have not started. ● Ready: This condition shows the pod is ready to use. ● ContainersReady: As the name suggests, if the containers are ready within a pod it will show True in the status. ● PodScheduled: This condition shows that the pod has been scheduled on the node.

KUBERNETES REQUEST QUOTAS

ResourceQuota: helps manage and distribute resources accoirding to the requirements

● Limit: Limit specifies that the container, pod, or namespace will have the limit resources where if the objects will exceed the limit then, the object won’t create.

● Request: The request specifies that the container, pod, or namespace needs a particular amount of resources such as CPU and memory. But if the request is greater than the limit then, Kubernetes won’t allow the creation of pods or containers.

Now, there are some conditions or principles for requests and limit which needs to be understood. Let’s understand with hands-on and theoretical.

If the requests and limits are given in the manifest file, it works accordingly.
If the requests are given but the limit is not provided then, the default limit will be used.
If the request
Service Account: A service account provides an identity for processes that run in a Pod. This is how Kubernetes authorizes API requests.

RBAC (Role-Based Access Control): RBAC is a method of regulating access to computer or network resources based on roles assigned to individual users within an enterprise.

Cluster Role: Cluster-wide roles define permissions on cluster-scoped resources.

Role: Roles define permissions within a namespace. Not tied to namespaces

Role Binding: Role bindings bind roles to subjects. A subject can be a user, group, or service account. permission with in cluster

DaemonSet: A DaemonSet ensures that all (or some) nodes run a copy of a Pod.

StatefulSet: A StatefulSet manages the deployment and scaling of a set of Pods, and provides guarantees about the ordering and uniqueness of these Pods. Label: Labels are key/value pairs that are attached to objects like Pods, Services, and Deployments to organize and select subsets of objects.

Namespaces: Namespaces provide a way to divide cluster resources between multiple users or teams.

Cluster: A cluster consists of at least one worker node and at least one master node.

Pods: Pods are the smallest and simplest Kubernetes objects. A Pod represents a single instance of a running process in your cluster.

Deployment: A Deployment provides declarative updates for Pods and ReplicaSets.

ReplicaSet: A ReplicaSet ensures that a specified number of pod replicas are running at any given time and works on eaulity controller-only.

Replication Controller: ensures a specified number of pods are running

Replicaset and replication are both repsonsible for vailability and autoscaling of pods, both ensures specified number of pods are running.

Labels: defined in keyvalue-pairs, similar to tags, used to organise k8s objects suchs as pods, nodes
Equality based selectors: select/filter objects by label key and values
Set-based selectors: select objects with a particular key with specified values
Kubernetes webhook authentification:
is an HTTPS service that recieved a request in defined format manages webhook authentification via valid certficate, static token file, openID connect tokens and service accounts Process: user generates a token to call for the Kube Api The token is receieved by the kubernetes api passes through an auth webhook in predefined format Webhook validates token and returns status in predefined format

Kubernetes validation webhook:

Autoscaler: daemon set: replicates pods across your nodes in the cluster, used for running node monitoring, collecting logs from nodes, backing up node data stateful set: ensures pods are created in a specific order replication controller : replicaset:

kubectl get role -A kubectl get --all-namespaces ~/.ssh ~/.kube/config

create a server volume

hcloud server create --image ubuntu-20.04 --name kelson-ubuntu --type cpx21 --location ash --user-data-from-file user_data.sh --volume kelson-vol1

How to get the cpu of a pod kubectl get pod podame-o=jsonpath='{.spec.containers[0].resources.requests.cpu}'

Mastering Kubernetes
Master nodes: manages the clusters manages, plans, schedules and monitors nodes
Worker nodes: Host applications
Master nodes components
-ETCD: database that stores cluster information on nodes, configs, secrets, accounts, roles, bindings, roles, Pods in the keyvalue format. -distrubuted reliable keyvalue store that is simple and fast -Keyvalue database that stores information in any format mostly Json, Yaml Access etcd using ./etcdctl (list all the commands that it supports) ./etcdctl set key1 value1 ./etcd get key1 what version is etcd= ./etcdctl --version to change the the etcd version from version 2 to 3 sets version 2 to 3 etcdclt_API3 ./etcdctl version export etcdctl_API=3 ./etcdctlversion sets a value ./etcdctl set key1 value1 gets a value ./etcdctl get key1 set up cluster using kubeadmin Kube admin deploys the etcd as a pod in the kube system name space kubectl get pods -n kube-system kubectl get serviceaccount -n kube-system kubectl get clusterrolebinding
API Server: -Authentificates users, validates request, retrieves data , updates data -Acts as the gateway to the Kubernetes cluster. -Accepts commands and communicates with other components. Kube admin deploys the API-server as a pod in the kube system name space To access the API-server kubectl get pods -n kube-system located on th master node as cat etc/kubernetes/manifests/kube-apiserver.yaml cat /etc/systemd/system/kube-apiserver.service ps -aux | grep kube-api-server
Controller Manager: -Ensures the desired state of the cluster. -Monitors, manages and controls various controllers, which manage different aspects of the system.responsible for availability and scalability -Node controller: monitors and checks the status of the nodes. Checks the status every 5 seconds and waits for 40 seconds to mark the nodes unreachable and gives it 5 minutes to come back -Replication controller: makes sure the desired number of pods are running at all times in a replication group Kube admin deploys the API-server as a pod in the kube system name space kubectl get pods -n kube-system located on the master note at cat etc/kubernetes/manifests/kube-controller-manager.yaml cat /etc/systemd/system/kube-controller-manager.service ps -aux | grep kube-controller-manager
Scheduler: Assigns (containers) to individual pods to Nodes based on resource availability. Distributes workload evenly across the cluster. Node (Minion/Worker Node): Kube admin deploys the Scheduler as a pod in the kube system name space on the master node kubectl get pods -n kube-system

located on the master note at
cat etc/kubernetes/manifests/kube-scheduler.yaml cat /etc/systemd/system/kube-scheduler.service ps -aux | grep kube-scheduler
Worker Nodes components
