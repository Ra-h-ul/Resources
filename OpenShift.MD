# OpenShift Overview

OpenShift is a Kubernetes-based platform that provides a set of developer and operational tools to build, deploy, and manage containerized applications. It supports multiple programming languages and frameworks.

### Supported Languages
- C, C++, Java, Python, R, Ruby, .NET, Perl, Golang, Node.js

### Supported Frameworks
- Quarkus, SpringBoot, Jenkins, Podman, Knative, Gin

---

## Major Components of OpenShift

### 1. **Pod**
A Pod is the smallest unit in the Kubernetes object model. It can contain one or more containers (e.g., Docker containers) that share the same network namespace and storage. Pods are ephemeral and should be treated as disposable. Kubernetes will restart or recreate them when needed.

### 2. **Cluster**
A cluster is a collection of nodes (physical or virtual machines) that work together to run containerized applications. It forms the foundation of Kubernetes/OpenShift, providing the necessary infrastructure for orchestrating and managing containers.

### 3. **Node**
A Node is a worker machine that runs the workloads of containerized applications. Nodes can be physical or virtual machines and are managed by the Kubernetes control plane.

#### Node Types:
1. **Master Node (Control Plane Components)**: Manages the entire cluster.
    - **API Server**: The central component that exposes the OpenShift API for cluster interaction. All operations like creating pods, services, or deployments are handled through the API server.
    - **Controller Manager**: Ensures the desired state of the OpenShift cluster by managing various controllers (node, endpoint, replication).
    - **Scheduler**: Assigns workloads (pods) to nodes based on resource availability, affinity, taints, and tolerations.
    - **etcd (Data Store)**: Stores all cluster data and configuration, including pod locations and resource statuses.

2. **Worker Nodes**: Run the actual containerized workloads. 
    - **Kubelet**: Runs on each worker node, ensuring that containers are running in the pods as defined.
    - **Kube Proxy**: Manages network traffic and load balancing within the cluster, helping with service discovery.
    - **CRI-O**: Container runtime interface for managing containers, replacing Docker in OpenShift.

---

## OpenShift Terminology

### 1. **Perspective**
"Perspective" refers to a feature within the OpenShift web console that streamlines the user interface (UI) based on the user’s role or task. You can switch between Developer and Administrator perspectives to tailor your experience.

### 2. **Observe**
Observe is part of OpenShift's observability features, which are essential for monitoring, tracking, and diagnosing the performance and health of applications, services, and infrastructure running within the cluster.

### 3. **Search**
Search allows you to find resources in your project by typing or scrolling through a list of existing resources.

### 4. **Namespace**
A Namespace is a way to divide cluster resources between multiple users or teams. It enables resource isolation, encapsulation of objects under a unique name, and provides resource quotas.

#### Features:
- Provides resource isolation.
- Supports policies for resource quotas and access control.

### 5. **Project**
A Project in OpenShift is a namespace with additional metadata, providing isolation and access control for resources like pods, services, and routes.

### 6. **Operator**
An Operator is a software extension to Kubernetes that uses custom resources to manage applications and their components. It automates tasks like application deployment, scaling, and lifecycle management.

### 7. **Deployment**
A Deployment defines how to create or modify instances of pods that hold a containerized application. It is often used for stateless applications and helps manage scaling, updates, and rollbacks.

### 8. **DeploymentConfig**
DeploymentConfig is an OpenShift-specific extension of Kubernetes Deployment that emphasizes consistency over availability.

#### Features:
- Supports triggers for automatic updates (e.g., image changes, config changes).
- Allows rolling, recreate, and custom deployment strategies.
- Integrates with lifecycle hooks (e.g., pre/post deployment actions).

### 9. **Build**
A Build in OpenShift creates runnable container images from source code, binaries, or Dockerfiles.

#### Types of Builds:
- **Source-to-Image (S2I)**: Converts source code into a runnable image.
- **Docker Build**: Builds images using a Dockerfile.
- **Binary Build**: Uploads pre-built binaries to create an image.

### 10. **BuildConfig**
A BuildConfig defines how a build is executed, including the source code location, build strategy, and where to store the output.

#### Key Features:
- Specifies source code location, build strategy, and image output.
- Integrates with triggers (e.g., webhooks, changes in source code).
- Automatically links builds with DeploymentConfig.

### 11. **ReplicaSet**
ReplicaSet ensures that a specified number of pod replicas are running at any time.

#### Features:
- Monitors and maintains the desired number of pods.
- Replaces failed pods with new ones.

### 12. **Service Account**
A Service Account is an internal account used by cluster tools or pods to interact with Kubernetes resources.

#### Features:
- Provides an identity for processes running in pods to interact with the Kubernetes API.
- Supports Role-Based Access Control (RBAC).

### 13. **Storage Class**
A Storage Class defines the characteristics of storage (e.g., backup policies, quality, etc.) that a cluster administrator configures.

#### Features:
- Defines storage type and parameters for dynamic provisioning.
- Enables automatic volume provisioning without manual PV creation.
- Specifies reclaim policies (Retain, Delete).

### 14. **Persistent Volume (PV)**
A Persistent Volume (PV) is a storage resource independent of cluster nodes. It holds information about the storage size, type, and sharing capabilities.

### 15. **PersistentVolumeClaim (PVC)**
A PersistentVolumeClaim is a request for storage by a user, specifying size, access modes, and optionally the storage class. It binds to an available PV for persistent storage.

#### Features:
- Binds to an appropriate PV (either static or dynamically provisioned).
- Links the application to persistent storage.

#### **PV vs PVC**:
- **PV**: Represents actual storage in the cluster, managed by the administrator.
- **PVC**: A request for storage by the user, which binds to a suitable PV.

---

## OpenShift Services

### 1. **Service**
A Service provides a stable endpoint to access a group of pods over a network, abstracting the complexity of pod IP addresses and lifecycle.

#### Types of Services:
- **ClusterIP** (default): Internal communication within the cluster.
- **NodePort**: Exposes the service on each node’s port.
- **LoadBalancer**: Integrates with external cloud load balancers.
- **ExternalName**: Maps a service to an external DNS name.

### 2. **Ingress**
Ingress exposes services inside the cluster to external clients using HTTP or HTTPS. It can provide load balancing, SSL/TLS termination, and routing based on hostnames or paths.

#### Features:
- Load balancing.
- SSL/TLS termination.
- Path-based and hostname-based routing.

### 3. **Routes**
Routes expose OpenShift services to external clients using HTTP, HTTPS, or TLS.

#### Key Features:
- Hostname-based routing.
- SSL termination and passthrough.
- Custom routing policies.

### 4. **Internal DNS**
OpenShift automatically provides DNS resolution for cluster services and pods.

#### DNS Features:
- Pods can be accessed via `<pod-name>.<namespace>.svc.cluster.local`.
- Services are accessible at `<service-name>.<namespace>.svc.cluster.local`.

---

## Deployment Strategies

Deployment strategies define how application updates are rolled out, ensuring minimal disruption or downtime.

### 1. **Recreate Strategy**
Stops all existing pods before starting new ones. Suitable for applications where maintaining state isn’t critical, but causes downtime.

### 2. **Rolling Strategy**
Incrementally replaces old pods with new ones. Ideal for applications that can handle partial updates.

### 3. **Custom Strategy**
Defines a completely custom deployment process. Useful for advanced scenarios where other strategies are insufficient.

### 4. **A/B Deployment**
Deploys a new version alongside the current version and splits traffic between them for testing. Ideal for testing features with a subset of users before full rollout.

#### Implementation:
- Deploy two versions (A and B) as separate services.
- Use a Route to split traffic between the two services.

### 5. **Blue-Green Deployment**
Maintains two environments: the current version (Blue) and the new version (Green). After validation, traffic is switched from Blue to Green, ensuring zero downtime.

#### Implementation:
- Deploy the new version as a separate DeploymentConfig or service.
- Use Routes to switch traffic from Blue to Green.

---

## Troubleshooting in OpenShift
(Troubleshooting section can be added here with more details if needed.)
