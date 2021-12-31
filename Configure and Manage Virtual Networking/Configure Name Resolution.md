(AZ-104 | Tim Warner | Pluralsight)

# <ins>*Configure Name Resolution*<ins>
---

## <ins>**Configure Azure-Provided Name Resolution**</ins>

- Hostname 
  - Single Label Name
  - Resolution within a single VNet
- Advantage: Ease of use/no configuration
- Advantage: No more globally unique VM host names
- *.internal.cloudapp.net (internet accessible DNS Zone)
  - Cannot modify suffix
- WINS and NetBIOS names are NOT supported
- Both A(forward lookup) & PTR(Reverse Lookup) lookups are supported


## <ins>*Azure Wire Server*</ins>

- IP Address: *168.63.129.16*
- Enables VM Agent to communicate with Azure platform
- Intra-VNet name resolution
- Azure-provided DHCP

### PowerShell to test connectivity:

```PowerShell

test-netconnection -ComputerName <name> -port <port>

```

- If TcpTestSucceedeed == True, ping is successful and we have connectivity.


## <ins>*Configure Custom DNS Settings*</ins>

### Custom DNS Use Cases:

- On-premises Active Directory
  - S2S VPN/ExpressRoute joining cloud and local AD
- IaaS Active Directory
- Inter-VNet name resolution
- FQDN name resolution

---

## <ins>*Configuring the Azure DNS Service*</ins>

- Cloud-based Domain Name System (DNS) hosting service
  - Public Zone
  - Private Zone
- Separate & Distinct from Azure Provided Name Resolution
- Enables name resolution between Azure VNets
- Can Do:
  - Host Public and Private Domains
  - Delegate a domain from another host
  - Integrates with ARM features (geo-availability (100% SLA), RBAC, tags locks, monitoring)
  - Creates an alias record for domain name apex with Traffic Manager
- Cannot Do:
  - Buy a Public Domain Name
    - Can buy an App Service Domain
  - Cannot enable DNSSEC 
  - Cannot support zone transfers


### <ins>*Public DNS Zones*</ins>

- 
