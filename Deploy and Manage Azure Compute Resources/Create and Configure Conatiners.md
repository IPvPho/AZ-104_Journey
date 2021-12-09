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

