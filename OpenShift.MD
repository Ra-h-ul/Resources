1. OpenShift : 

        OpenShift is a Kubernetes-based  platform that provides a set of developer and operational tools to build, deploy, and manage containerized applications. It supports multiple programming languages and frameworks.

        languages : c c++ java python R ruby .Net perl Golang node
        Frameworks : quarqus springBoot jenkins podman Knative Gin

2. Major components of openshift.

- Pod :
        
        A Pod is the smallest unit in the Kubernetes object model that you create or deploy. It can contain one or more containers (e.g., Docker containers) that share the same network namespace and storage. Each pod can hold tightly coupled containers that need to share storage or networking. Pods are ephemeral and should be treated as disposable; Kubernetes will restart or recreate them when needed.

- Cluster :
        
        a cluster is a collection of nodes (physical or virtual machines) that work together to run containerized applications. The cluster forms the foundation of a Kubernetes/openshift environment, providing the necessary infrastructure for orchestrating and managing containers.


- Node:

        Node is a worker machine that runs the workloads of containerized applications. It is an essential part of the Kubernetes/openshift architecture, providing the infrastructure that allows applications to run in a distributed manner. Nodes can be physical machines or virtual machines and are managed by the Kubernetes control plane.

        1.Master Node (Control Plane Components) :Manages the entire cluster

        API Server: The API server is the central component that exposes the OpenShift API for interaction with the cluster. All operations, such as creating pods, services, or deployments, are handled through the API server. The CLI, web console, and other services communicate with the API server.

        Controller Manager: The controller manager is responsible for maintaining the desired state of the OpenShift cluster by managing various controllers, such as node controllers, endpoint controllers, and replication controllers.

        Scheduler: The scheduler assigns workloads (pods) to nodes based on resource availability, affinity, taints, tolerations, and other scheduling policies. It ensures that containers are deployed on appropriate nodes to optimize resource usage.

        etcd (Data Store): OpenShift uses etcd to store all cluster data and configuration. It’s a distributed key-value store that contains information about the state of the cluster, such as pod locations, configuration settings, and resource statuses.

        2.Worker Nodes :Runs the actual containerized workloads

        Kubelet: Kubelet runs on each worker node, communicating with the control plane (master node) to manage container lifecycle. It ensures that the containers are running in the pods as defined in the deployment.

        Kube Proxy: Kube Proxy is responsible for managing network traffic and load balancing within the OpenShift cluster. It helps with service discovery and ensures that requests reach the appropriate pod across nodes.

        CRI-O: OpenShift uses CRI-O as the container runtime interface (instead of Docker),  the container runtime is the software responsible for running containers on each node. It manages container lifecycle operations like creating, starting, stopping, and deleting containers.


3. Openshift terminology

- Perspective :  

        Perspective" refers to a feature within the OpenShift web console that helps organize and streamline the user interface (UI) to suit the role or task of the user. we can switch between Developer and Administrator perspectives.

- observe: 
        
        Observe is part of the observability features, which are essential for monitoring, tracking, and diagnosing the performance and health of applications, services, and infrastructure running within the OpenShift cluster. 

- Search : 
        
        Search for resources in your Project by simply starting to type or scrolling through a list of existing resources.

- Namespace : 
        
        A Namespace  is a way to divide cluster resources between multiple users or teams and can enable you to isolate resources, encapsulating objects under a unique name, and providing resource quotas.

        features  
        1. Provides resource isolation.
        2. Supports policies for resource quotas and access control.

- Project : 
        
        
                
                A Project in OpenShift is a namespace with additional metadata, providing isolation and access control for resources. It Includes RBAC policies for user access ans Encapsulates resources like pods, services, and routes.
    
- Operator :
        
         An Operator is a software extensions to Kubernetes that uses custom resources to manage applications and their components. It takes high-level user configuration and acts to make the cluster match the desired state.

- Deployment :
        
         A Kubernetes/openshift Deployment tells Kubernetes how to create or modify instances of the pods that hold a containerized application. Kubernetes deployments are completed using kubect. It is commonly used for stateless applications.Deployments can help to efficiently scale the number of replica pods, enable the rollout of updated code in a controlled manner, or roll back to an earlier deployment version if necessary.

- DeploymentConfig :
        
         The DeploymentConfig object is a Red Hat OpenShift extension of the Kubernetes Deployment that favors consistency over availability.

        provides  
        1. Supports triggers for automatic updates (image changes, config changes).
        2. Allows rolling, recreate, and custom deployment strategies.
        3. Can integrate with lifecycle hooks (pre/post deployment actions).

- Build :
        
         A Build in OpenShift is a process that creates container/runnable images from source code, binaries, or Dockerfiles.

        Types of Builds:
        1. Source-to-Image (S2I): Converts source code into a runnable image.
        2. Docker Build: Builds images using a Dockerfile.
        3. Binary Build: Uploads prebuilt binaries to create an image.



- BuildConfig :
        
         A BuildConfig defines how a build is executed and its parameters.A build object requires, at least, the source input of the build, the build strategy that defines how to build the input, and where to store the output of the process.

        Key Features:
        1. Specifies source code location, build strategy, and image output.
        2. Integrates with triggers (e.g., webhooks, changes in source code).
        3. Automatically links builds with DeploymentConfig.


- ReplicaSet :
        
         ReplicaSet is a part of deployment , ReplicaSet object indicates the number of pods that are available to attend a request or it ensures that a specified number of pod replicas are running at a time . This object also ties all the pods replicas together so you can operate on them at the same time. 

        features  
        1. monitors and maintains the desired number of pods
        2. replace failed pods with new one



- Service Account :
        
         A Service Account is a special kind of account that does not correspond to an actual user but it is used internally by cluster tools. It is useful for pods to connect to objects in the cluster such as CI/CD pipelines, secrets, or external (to the namespace or to the cluster) resources.

        features  
        1. provides an identity for processes running in pods to interact with the Kubernetes API.
        2. Automatically mounted into pods and supports RBAC (Role-Based Access Control).

- Storage Class : A Storage Class is a name that identifies a particular kind of storage defined by the cluster administrator. A storage class also defines its own characteristics, be it backup policies or service level quality, or any other specification the admin might choose.

        features  
        1. StorageClass defines the storage type and parameters for dynamically provisioning persistent storage.
        2. Defines storage backend and provisioning parameters (e.g., type, size, replication).
        3. Enables dynamic volume provisioning without needing to manually create PVs and allows specifying reclaim policies (Retain, Delete).

- Persistent Volume (PV) :
        
         A Persistent Volume (PV), is a persistence storage unit offered by the cluster, independent of cluster nodes. This object holds the information regarding the size, the type, or the ability to share the storage.

- PersistentVolumeClaim (PVC) :
        
         A PersistentVolumeClaim is a request for storage by a user, specifying size, access modes, and optionally the storage class. A PVC is a request to access a specific kind of storage of the required size. After acquiring the PVC, the storage is attached to the pods claiming it.

        features:
        1.Binds to an appropriate PV (static or dynamically provisioned).
        2.Acts as the link between an application and the persistent storage.

- PV vs PVC :

        PV: PV represents the actual storage resource in the cluster and is managed by the cluster administrator. It can be manually or dynamically provisioned and 	Waits to be claimed by a PVC.
        
        PVC:  PVC is a request for storage made by an application and is created by application developers or users. Dynamically provisions storage if StorageClass is specified and automatically binds to a suitable PV.

- Service : 

        A Service provides a stable endpoint to access a group of pods. It exposes a set of pods over a network. This abstraction allows internal or external clients of the application running on said pods to connect to them regardless of the actual state of the replicas or varying network IPs.

        Types of Services:
        1. ClusterIP (default): Internal communication within the cluster.
        2. NodePort: Exposes the service on a specific port of each node.
        3. LoadBalancer: Integrates with external cloud load balancers.
        4. ExternalName: Maps a service to an external DNS name

- Ingress :
        
        An Ingress exposes services inside the cluster to outside clients by using HTTP or HTTPS. A service ingress can also provide external URLs, load balancing, name-based virtual hosting, or SSL/TLS termination.
       
        Key Features:
        1. Provides load balancing.
        2. Manages SSL/TLS termination.
        3. Supports path-based and hostname-based routing.

- Routes :
        
        A Route serves a similar purpose to the Kubernetes ingress but provides additional features: TLS passthrough and re-encryption, wildcard domains, pattern-based domains, and splitting traffic. A Route exposes OpenShift services to external clients using HTTP, HTTPS, or TLS.

        Key Features:
        1. Manages hostname-based routing.
        2. Supports SSL termination and passthrough.
        3. Enables custom routing policies.

- Internal DNS
        
        OpenShift automatically provides DNS resolution for cluster services and pods.

        DNS Features:
        1.Pods can be accessed via <pod-name>.<namespace>.svc.cluster.local.
        2. Services are accessible at <service-name>.<namespace>.svc.cluster.local.



4. Deployment Strategies : Deployment strategies define how application updates are rolled out, ensuring minimal disruption or downtime. 

-  Recreate Strategy:
        
        Stops all existing pods before starting new ones. Suitable when maintaining application state is not required, or running two versions simultaneously could cause conflicts.Simple, ensures only one version runs at a time.Causes downtime during deployment.


- Rolling Strategy :
        Incrementally replaces old pods with new ones. Default strategy in OpenShift ideal for applications that can handle partial updates.Zero downtime if the application supports concurrent versions.Requires careful management of backward compatibility between old and new versions.


- Custom Strategy : 
        
        Allows defining a completely custom deployment process.Useful for advanced deployment scenarios where other strategies are insufficient. Complete control over deployment.Complexity in scripting and managing the process.


-  A/B Deployment: 
        
        Deploys a new version alongside the current version and splits traffic between them for testing.Ideal for testing new features with a subset of users before full rollout.
        Allows real-time testing with a subset of users and disadvantage is that it requires monitoring and rollback mechanisms for errors.

        implementation: Deploy two versions (A and B) as separate services.Use a Route to direct traffic percentages between the two services.

- Blue-Green Deployment:
        
        Maintains two environments: the current version (Blue) and the new version (Green). Traffic switches from Blue to Green after deployment validation. Ensures zero downtime and easy rollback but it is resource-intensive as both environments run simultaneously.

        implementation : Deploy the new version as a separate DeploymentConfig or service. Use Routes to switch traffic from Blue to Green.

5. Trouble shooting in Openshift :  

