(AZ-104 | Tim Warner | Pluralsight)

# <ins>***Implement and Manage Virtual Networking***</ins>
---

## <ins>**Implement Virtual Networks**</ins>
---

### <ins>*Azure Wire Server*</ins>

- Virtual IP
  - 168.63.129.16
- Responsible for DHCP to VMs
- Default Gateway for VMs
- Does DNS
- VM Agent Communication


### <ins>*Public and Private IP Addresses*</ins>

- All Azure services are available on public IP addresses
  - Service Tags
- Consider public IP addresses for ingress traffic only
- VM Management
  - Azure Bastion (Port 443)
  - Azure Load Balancer (NAT)
  - App Gateway (NAT)
  - Azure Firewall (NAT)
  - JIT VM Access


### <ins>*Name Resolution Options*</ins>

- Azure-provided Name resolution
  - Single name resolution
  - Within single VNet only
  - No custom DNS names
- Use your own DNS Server(s)
  - Full control over name resolution and forwarding
  - More expensive to deploy and manage
- Azure DNS
  - Public Zones
  - Private Zones


### <ins>*VNet Deployment Methods*</ins>

- Portal
- PowerShell
- Azure CLI
- JSON Template (ARM)
- ARM REST API



### <ins>*Simple VNet Deployment - PowerShell:*</ins>

```PowerShell

$virtualNetwork = New-AzVirtualNetwork `
    -ResourceGroupName myResourceGroup `
    -Location EastUS `
    -Name myVirtualNetwork `
    -AddressPrefix 10.0.0.0/16

$subnetConfig = Add-AzVirtualNetworkSubnetConfig `
    -Name default `
    -AddressPrefix 10.0.0.0/24 `
    -VirtualNetwork $virtualNetwork

$virtualNetwork | Set-AzVirtualNetwork

```

### <ins>*Simple VNet Deployment - Azure CLI:*</ins>

```Bash

az network vnet create \
    --name MyVnet \
    --resource-group $RgName \
    --location $Location \
    --address-prefix 10.0.0.0/16 \
    --subnet-name MySubnet-FrontEnd \
    --subnet-prefix 10.0.1.0/24

az network vnet subnet create \
    --address-prefix 10.0.2.0/24 \
    --name MySubnet-BackEnd \
    --resource-group $RgName \
    --vnet-name MyVnet

```

Virtual Network planning is crucial
- Avoid IP Address overlap
- VM Placement
 
Think about governance
- Azure Blueprints


---

## <ins>*Manage Azure Virtual Networks**</ins>

### *Subnet Delegation*

- Injected Services
- Reserved Subnet Label
- Security Policies
- Route Policies


### *Service Endpoints*

- 

