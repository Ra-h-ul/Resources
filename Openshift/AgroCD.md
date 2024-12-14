
# What is Argo CD

Argo CD (Continuous Delivery) is a declarative, GitOps-based continuous delivery tool for Kubernetes. It is used to automate the deployment of applications on Kubernetes by maintaining the desired state of applications in a Git repository and syncing it with the actual state in the Kubernetes cluster.

# Alternatives to Argo CD:

- Flux CD: Another GitOps tool that automates the deployment of applications in Kubernetes.

- Jenkins X: A CI/CD platform built for Kubernetes and designed around GitOps principles.

- Spinnaker: A multi-cloud continuous delivery platform.

- GitLab CI/CD: A CI/CD tool with native GitOps support.

- Helm: Although not strictly a GitOps tool, Helm is commonly used in conjunction with Argo CD and other GitOps tools for managing Kubernetes applications.

# Before Argo CD:

Before Argo CD and similar GitOps tools, Kubernetes deployments were typically managed by manually applying Kubernetes manifests (kubectl apply), using Helm charts, or employing other CI/CD tools such as Jenkins and CircleCI that integrate with Kubernetes via scripts or custom plugins. This approach required a lot of manual intervention, leading to inconsistent deployments and challenges in maintaining the desired state of the cluster.

---

# How Argo CD Works:

Argo CD follows the GitOps model, which means the desired state of applications and their configurations is stored in a Git repository. Argo CD continuously monitors the repository for any changes and automatically applies them to the Kubernetes cluster. It compares the current state of the application in the cluster to the desired state stored in Git and ensures they are synchronized.

---
# Advantages of Argo CD:

- Declarative Configuration: The entire configuration is stored in Git, making it easy to manage and review.

- Automated Sync: Argo CD automatically synchronizes the desired state with the actual state in the cluster, reducing manual intervention.

- Multi-cluster Support: Argo CD can manage multiple Kubernetes clusters from a single instance.

- Visibility: Provides a UI and CLI to monitor and manage application deployments, making it easy to visualize the state of your applications.

- Rollback Support: You can easily roll back to previous versions of an application by simply reverting the Git commit.

- Security: By using Git as the source of truth, it provides version control and auditability for Kubernetes deployments.

# Disadvantages of Argo CD:

- Learning Curve: For teams not familiar with GitOps or Kubernetes, it can take time to learn and set up Argo CD.

- Complexity: Although Argo CD automates many processes, it can add complexity to the Kubernetes management lifecycle.

- Limited Integration: While Argo CD integrates well with Kubernetes, it might require additional tools or custom setups for specific integrations or non-Kubernetes workloads.
---
# Architecture of Argo CD:

## Argo CD consists of several key components:

- API Server: The main entry point for users to interact with Argo CD. It provides a REST API and user interface for managing applications.

- Repo Server: Responsible for interacting with Git repositories and fetching the configuration files.
Application Controller: Monitors the desired state of applications and reconciles them with the actual state in the Kubernetes cluster.

- Database (optional): Stores the application state and user session data.

- Notification System: Sends notifications related to the state of applications, such as when an application is out of sync or when a sync operation is completed.

# Main Components of Argo CD

- Git Repository: Holds the Kubernetes manifests or Helm charts, which define the desired state of the application.
Argo CD Server: Provides the API and UI to interact with the system.

- Controller: Syncs the state between the Git repository and the Kubernetes cluster.
Application: The logical entity in Argo CD that defines an application and its associated resources.

---

#  Configuring ArgoCD to Deploy an Application to a Kubernetes Cluster

To configure ArgoCD to deploy an application to a Kubernetes cluster, follow these steps:

### Step 1: Install ArgoCD on Your Kubernetes Cluster

- Create a namespace for ArgoCD:

        kubectl create namespace argocd

- Install ArgoCD using the Kubernetes manifests:

        kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

- Expose ArgoCD API server to access the Web UI:

        kubectl expose svc/argocd-server -n argocd --type=LoadBalancer --name=argocd-server

Obtain the initial admin password:

    kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath='{.data.password}' | base64 -d; echo

### Step 2: Access the ArgoCD Web UI

-    Get the URL of the ArgoCD server:

    kubectl get route -n argocd

This will give you the URL, which you can access through a web browser.

- Login using the username admin and the password obtained in the previous step.

### Step 3: Create an Application in ArgoCD

-    Add your Git repository containing Kubernetes manifests or Helm charts to ArgoCD:

        Go to Settings > Repositories and add your repository.
        Provide necessary authentication (if required).

- Create a new application:

    1. Go to Applications and click New App.
    2. Fill in the application details:
            
        1. Name: Application name
        2.    Git Repo URL: URL to the Git repository
        3.    Branch/Tag/Commit: The specific version of your code to deploy.
        4.    Path: The folder path where the Kubernetes manifests or Helm charts are stored.
        4.    Cluster: The target cluster (ArgoCD can deploy to multiple clusters).
        6.    Namespace: The Kubernetes namespace where the app will be deployed.

    Sync the application: Once the application is created, ArgoCD will pull the repository and deploy the app to the Kubernetes cluster based on the specified Git configuration.
---
# How ArgoCD Manages Rollbacks

ArgoCD keeps track of every deployment in its history, making it easy to roll back to a previous state if needed.
Rollback Process:

- Viewing Application History:
        In the ArgoCD Web UI, you can view the history of an application’s deployment.
        ArgoCD stores the commit hashes or version numbers of the deployed application.

- Rollback to a Previous Version:
        Go to the Applications section in ArgoCD UI.
        Select your application and view the History tab.
        You can choose a specific revision and click Sync to roll back to that version.

- Automatic Rollbacks:
        ArgoCD does not automatically rollback, but you can configure a health check to monitor and alert you in case a deployment fails, enabling you to perform manual rollbacks.
---
# How ArgoCD Handles Secrets

### ArgoCD doesn’t store secrets directly in the Git repository; instead, it integrates with external secret management systems to handle sensitive information.
Handling Secrets with ArgoCD:

- External Secret Management Tools:
  
    1. Vault: You can integrate HashiCorp Vault with ArgoCD to manage secrets.
        
    2.    Sealed Secrets: Bitnami’s Sealed Secrets can be used to encrypt Kubernetes secrets, which are then safely stored in Git.
        
    3.    Helm Secrets: You can use Helm charts with encrypted secrets and decrypt them during deployment.

- Creating Sealed Secrets:
        The Bitnami Sealed Secrets controller can be used to encrypt secrets, which are then safe to store in Git repositories. Only authorized controllers can decrypt them at runtime.

- Referencing Secrets:
        In your Kubernetes manifests, you would reference the secrets that are managed by the secret management tool, ensuring they are decrypted only at the time of deployment.
---
# Multicluster Deployment with ArgoCD

ArgoCD supports deploying to multiple Kubernetes clusters, enabling you to manage deployments across multiple environments (e.g., staging, production) from a single ArgoCD instance.
Steps for Multicluster Deployment:

- Add Multiple Clusters to ArgoCD:ArgoCD can manage multiple clusters. To add a new cluster to ArgoCD, use the following command:

        argocd cluster add <kube-context>

This allows ArgoCD to interact with different clusters using different kube contexts.

- Deploy to a Specific Cluster:When creating an application in ArgoCD, select the cluster to which you want to deploy your application.You can manage multiple applications, each targeting different clusters.

- Sync Across Clusters: ArgoCD will keep your application in sync across clusters, meaning any changes made in Git are automatically deployed to the selected clusters.
---
# How ArgoCD Works with Jenkins and Helm Charts

### ArgoCD and Jenkins Integration: ArgoCD and Jenkins can work together as part of a CI/CD pipeline. Jenkins can be used to build and test the application, while ArgoCD handles the deployment.

- Jenkins for CI:
        Jenkins can be used to trigger builds, run tests, and package the application into Docker containers or Helm charts.
        Jenkins can push the application code to a Git repository that ArgoCD watches.

- ArgoCD for CD:
        Once Jenkins pushes the updated code or Helm chart to Git, ArgoCD will automatically detect changes and deploy the new version of the application to the Kubernetes cluster.

- Triggering ArgoCD Sync from Jenkins:
        Jenkins can trigger ArgoCD’s sync process by making a REST API call to ArgoCD’s API endpoint. For example:

        curl -X POST -k -u <username>:<password> \
        -d '{"revision": "<commit hash>"}' \
        https://argocd.example.com/api/v1/applications/<app-name>/sync
---
# Using Helm Charts with ArgoCD:

### ArgoCD supports Helm charts, and you can use it to deploy applications that are defined using Helm.

- Helm Chart Deployment:
        In the ArgoCD UI, you can specify Helm charts as the application source. When creating a new application, choose Helm as the source type and provide the Helm chart repository URL.
        You can use specific versions or tags of the Helm chart stored in Git.

- Helm Values:
        You can specify custom values for the Helm chart deployment through the values.yaml file in your Git repository or as overrides in the ArgoCD Web UI or CLI.

- Syncing Helm Charts:
        ArgoCD will handle Helm chart deployments in the same way as Kubernetes manifests, applying any changes to the cluster when changes are detected in the Git repository.


---
# How Argo CD Works with OpenShift:

### Argo CD can be used with OpenShift, a Kubernetes distribution, in the same way it is used with regular Kubernetes clusters. Here's how it works:

- Git Repository: The desired state of your application (e.g., YAML files or Helm charts) is stored in a Git repository.
    
- Argo CD Installation: Argo CD is installed in the OpenShift cluster, typically through an Operator or by using kubectl.
    
- Argo CD Sync: Once Argo CD is set up, it continuously monitors the Git repository for changes. When a change is detected, it automatically syncs the changes to the OpenShift cluster.
    
- OpenShift Integration: Argo CD works with OpenShift resources like Deployments, StatefulSets, Services, etc., and can also leverage OpenShift’s integrated tools like OpenShift Templates, Routes, and BuildConfigs.

- Access Control: Argo CD can be used in OpenShift to manage deployments with RBAC (Role-Based Access Control) policies and integrate with OpenShift’s built-in authentication.


---
# Deploy an application using AgroCD and openshift 

## 1. Set up OpenShift Cluster

You need an OpenShift cluster to deploy your application. You can either set it up on a cloud provider (AWS, GCP, Azure) or locally using Minishift (a tool to run OpenShift on a local machine). Make sure you have access to your cluster and that it’s running properly.

## 2. Install ArgoCD

ArgoCD is a GitOps tool used to manage Kubernetes (and OpenShift) applications. It automates the deployment process by syncing the desired state of your application from Git to your cluster.

### Steps:

- Create a Namespace: Create a dedicated namespace for ArgoCD to isolate it from other services on your cluster:

        oc create namespace argocd

- Install ArgoCD: You’ll use the Kubernetes manifests provided by ArgoCD to install the necessary components. By running the command:

        kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

This command deploys all ArgoCD components like the API server, controller, repo server, etc.

Expose the ArgoCD API Server: OpenShift runs services within the cluster by default, and ArgoCD's API server needs to be exposed to access the Web UI. The command below creates a LoadBalancer to expose the service:

oc expose svc/argocd-server -n argocd --type=LoadBalancer --name=argocd-server

Get the Initial Admin Password: By default, ArgoCD uses the admin user. The initial password is stored in a secret, and you can retrieve it using the following command:

    oc get secret argocd-initial-admin-secret -n argocd -o jsonpath='{.data.password}' | base64 -d; echo

    This will give you the password for the admin account.

## 3. Access ArgoCD Web UI

Now that ArgoCD is installed, you can access the Web UI:

- Use the OpenShift CLI to get the route for the ArgoCD server:

        oc get route -n argocd

- Open the browser and go to the URL for the ArgoCD API server. Log in using the username admin and the password you retrieved earlier.

## 4. Configure Git Repository in ArgoCD

ArgoCD works on the GitOps model, where the desired state of the application is stored in Git repositories. For ArgoCD to deploy your application, you must configure it with access to your Git repository (GitHub, GitLab, Bitbucket, etc.).

### Steps:

- In the ArgoCD Web UI, go to Settings > Repositories.
    Add your Git repository by providing the URL. 
    
- You’ll also need to authenticate if your repository is private.This allows ArgoCD to pull your application's Kubernetes manifests or Helm charts from the Git repository.


## 5. Create an Application in ArgoCD

### In ArgoCD, applications are defined as a combination of a repository, a target cluster, and a namespace where the resources will be deployed. You configure ArgoCD to monitor the Git repository and continuously deploy any changes. 

## Steps:

-  In the ArgoCD Web UI, go to Applications and click New App.
    Fill in the application details:
  
- Application Name: A unique name for your application.

- Project: If you use ArgoCD projects, you can select or create a project here. Projects help group and organize applications.

- Sync Policy: Choose whether to manually trigger deployments or automatically sync with changes in the Git repository.

- Git Repo URL: Enter the URL of your Git repository where the Kubernetes manifests or Helm charts are stored.

- Revision: Specify the Git branch, tag, or commit to use for the application.

- Path: Define the folder within the Git repository where your Kubernetes manifests or Helm charts reside.

- Cluster: Specify the OpenShift cluster where the application should be deployed.

- Namespace: Choose the namespace in the cluster where your application will run.

- ArgoCD will use this information to pull the desired state (Kubernetes resources) from the Git repository and deploy it on OpenShift.

## 6. Deploy the Application

Once the application is created, ArgoCD automatically syncs the application with the Git repository. It compares the desired state in the repository with the actual state in the OpenShift cluster and applies the changes accordingly.
Steps:

-    If you selected automatic sync, ArgoCD will immediately start deploying the application and keep it updated with any changes made to the Git repository.

-    If you chose manual sync, you need to trigger a sync in the ArgoCD UI, which will start the deployment process.

## 7. Monitor and Manage Application

ArgoCD provides a Web UI to monitor and manage your applications. You can view the deployment status, logs, and sync status:

- If there are discrepancies between the desired state and the actual state, ArgoCD will show it and can automatically reconcile it.

-    You can trigger a manual sync or view detailed logs for troubleshooting.

## 8. Automate Updates

### ArgoCD makes continuous delivery seamless:

- Whenever you push updates to your Git repository (e.g., new versions of Kubernetes manifests), ArgoCD will automatically detect these changes and deploy them to your OpenShift cluster (if auto-sync is enabled).
    
- This allows for a continuous delivery pipeline where your application is always up to date with the state defined in your Git repository.