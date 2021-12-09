(AZ-104 | Michael Teske | Pluralsight)

# <ins>***Create and Configure Containers***</ins>

## <ins>*What are Azure Container Instances?*<ins>

### *What is a container?*
- Bundles apps code together with related configuration files and libraries
- Runs on a virtualized version of the Host OS
- Because the differences in underlying OS and infrastructure are abstracted, as long as the base image is consistent, the container can be deployed and run anywhere.



### *Benefits of Container Instances:*

- Faster startup
- Per second billing
- Security through isolation
- Custom sizes
- Persistent storage
- Linux and Windows


### *Core Concepts:*

- Azure Container Instances allows you to run multiple containers without managing servers
- Image source is the source from which the image is pulled.
- Can create and upload custom images to your registry.
- Registries are the location of images, can be Azure Container Registry, Docker Hub, or other container registry.
- Restart policies include 'always', 'on failure' and 'never'.

### <ins>*Creating an Azure Container Instance*

**Azure CLI:**

```PowerShell
# create a resource group

az group create --name ps-course-rg --location eastus

# create and deploy a continaer

az container create --resource-group ps-course-rg --name mycontianer \
--image mcr.microsoft.com/azuredocs/aci-helloworld --dns-name-label az104-demo \
--ports 80 --restart-policy Always

```


### <ins>*Azure Container Groups*

- Collection of containers on the same host
- Currently supports only Linux container instances
- Deployment Options:
  - Resource Manager template (ARM)
  - YAML file
- Update containers in a group by redeploying the group with at least one modified property
- Modified properties that requires container deletion:
- *Container groups are fully destroyed and recreated (not redeployed)*
  - OS type
  - CPU, memory, GPU
  - Restart policy
  - Network profile


### <ins>*Deploying Container Group with ARM Template*</ins>
**Azure cli:**

```powershell

# Create a resource group

az group create --name container-rg --location eastus

# Create and deploy Azure Container group from template

az deployment group create --resource-group container-rg --template-file azuredeploy.json

# View deployment state

az container show --resource-group container-rg --name demo-container-group --output table

# View container logs

az container logs --resource-group container-rg --name demo-container-group --container-name aci-tutorial-app

# View side-car logs

az container logs --resource-group container-rg --name demo-container-group --container-name aci-tutorial-app

```

---

## <ins>*Create and Configure Azure Kubernetes Service*</ins>


### *What is Azure Kubernetes Service?*

- Open-source system for automating deployment, scaling and management of containerized apps
- It's a management platform using declarative configuration to orchestrate containers in different compute environments.
- A Kubernetes deployment is configured as a cluster consisting of at least one 'master' machine and one or more 'worker' machines.
- Azure Kubernetes Service (AKS) manages hosted Kubernetes clusters
  - Environment is enabled with:
    - Automatic Updates
    - Self-Healing
    - Easy Scale
- AKS cluster is managed by Azure and is free
  - Only pay for VMs on which the nodes run
- Can register with Azure ARC

### *Create an Azure Kubernetes Cluster*

- Nodes of the same configuration are grouped in node pools.
- When you create your cluster, you create a system node pool
- The AKS cluster must use VM Scale Sets for the nodes for autoscaling and multiple node pools
- All node pools must reside in the same virtual network
- AKS cluster must use the *'Standard SKU'* load balancer to use multiple node pools
- Once deployed, you CANNOT change the node size


### *Create an AKS Single Node Cluster*

```bash

# Create a basic single-node AKS cluster

az aks create \
    --resource-group ps-course-rg \
    --name PSAKSCluster \
    --vm-set-type VirtualMachineScaleSets \
    --node-count 2 \
    --generate-ssh-keys \
    --load-balancer-sku standard


```

### *Adding an AKS Node Pool*

```bash

# Adding an AKS Node Pool

az aks nodepool add \
    --resource-group ps-course-rg \
    --cluster-name PSAKSCluster \
    --name mynodepool \
    --node-count 3

```

### *Configure Storage for AKS*

- Volumes
  - Disks
  - Files
- Persistent Volumes
  - Only exist until the volume is deleted
- Storage Classes
- Persistent Volume Claims
  - Request disk or file storage of a particular storage class like access mode and size


| Use Case                                  | Volume Plugin | Read/Write Once | Read-Only Many | Read/Write Many | Windows Server Container Support |
|-------------------------------------------|---------------|-----------------|----------------|-----------------|----------------------------------|
| Shared Configuration                      | Azure Files   | Yes             | Yes            | Yes             | Yes                              |
| Structured App Data                       | Azure Disks   | Yes             | No             | Yes             | Yes                              |
| Unstructured Data, File System Operations | BlobFuse      | Yes             | Yes            | Yes             | No                               |


### *Configuring Scaling for AKS*

- Manual scale pods or nodes
  - Portal or AZ CLI
- Horizontal pod auto-scaler (HPA)
  - Setup guardrails with min and max metrics (i.e cpu usage)
  - Can scale up and down
  - Cool down period ensures auto-scalers before another event can be triggered
- Cluster auto-scaler
  - Auto-scales nodes of the cluster based on requested ocmpute demand
  - Run in conjunction with HPA
  - Can scale up an down


### *Configuring Scaling with AZ CLI:*

```bash

# Manual scale pods

kubectl scale --replicas=5 deployment/azure-vote-front

# Manual scale nodes

az aks scale --resource-group ps-course-rg --name myAKSCluster --node-count 3

# Autoscale

kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10

```

### *Configuring Networking for AKS*

<ins>*Kubenet vs. Azure CNI*</ins>

| Capabilities                                                                        | Kubenet                         | Azure CNI       |
|-------------------------------------------------------------------------------------|---------------------------------|-----------------|
| Deploy cluster in existing or new VNet                                              | Supported-UDRs manually applied | Supported       |
| Pod to Pod Connectivity                                                             | Supported                       | Supported       |
| Pod to VM, VM in same VNet                                                          | Works when initiated by pod     | Works both ways |
| Pod to VM, VM in peered VNet                                                        | Works when initiated by pod     | Works both ways |
| On-premises access using VPN                                                        | Works when initiated by pod     | Works both ways |
| Access to resources secured by service endpoints                                    | Supported                       | Supported       |
| Expose Kubernetes service using a load balancer, App Gateway, or ingress controller | Supported                       | Supported       |


*IP Addresses for Pods*

- If it is a Kubenet *ONLY* the worker nodes will get an IP form the subnet they reside in
- If it is a CNI *ALL* nodes will get an IP from the subnet they reside in 
  - Must understand this due to limited IP Addresses in large clusters


### <ins>*Upgrading a Cluster:*</ins>

***YOU CAN ONLY UPGRADE ONE MINOR VERSION AT A TIME***

- You *can* upgrade from 1.1.4.x to 1.15.x
- You *cannot* upgrade from 1.14.x to 1.16.x


```bash

# Show current version of AKS

az aks show --resource-group ps-course-rg --name myAKSCluster --output table

# Get available upgrades for the cluster 

az aks get-upgrades --resource-group ps-course-rg --name myAKSCluster

# Upgrade Cluster

az aks upgrade --resource-group ps-course-rg --name myAKSCluster --kubernetes-version <KUBERNETES_VERSION>

```