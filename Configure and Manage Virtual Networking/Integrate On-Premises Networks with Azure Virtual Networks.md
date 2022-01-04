(AZ-104 | Tim Warner | Pluralsight)

# <ins>***Integrate On-Premises Networks with Azure Virtual Networks***</ins>
---

## <ins>**Configure an Azure Virtual Private Network**</ins>

- Virtual Private Network (VPN):
  - A secure, encrypted connection over an unsecure communications medium (typically the public internet).

### <ins>*Azure VPN Value Proposition*</ins>

- Extending local network in to Azure
- Fully embrace hybrid cloud deployments
- Manage local systems from Azure
- Compliance
- Manage Azure systems from local network
- High Availability


### *Site-to-Site VPN (S2S)*

- "Always on" VPN using IPSec and IKE protocols
- Supports Policy Based (Static) or Route Based (Dynamic) routing methods
- Active-Active or Active-Passive Highly Available scenarios
- Number of tunnels and max bandwidth depends on SKUs

![S2S VPN](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/images/hub-spoke.png)

### *VNet-to-VNet VPN*

- Before global VNet peering, this was once the only way to link VNets in different regions.
- Same IPSec/IKE secure tunnel used in S2s VPN
- Local network gateways are automatically created and populated.
- Benefit:
  - Isolation
  - Security
  - Administrative Boundary

![VNet-to-VNet VPN](https://docs.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-howto-vnet-vnet-resource-manager-portal/connections-diagram.png)

### *Point-to-Site VPN (P2S VPN)*

- Individual VPN tunnels to the Virtual Network
- Standards-based Protocols:
  - OpenVPN (TLS)
  - SSTP (TLS).
  - IKEv2 (IPSec) VPN
- Proof of concept deployments, more traditionally for remote workers
- Certificate, Azure AD, and RADIUS (local AD) authentication options

![P2S VPN](https://docs.microsoft.com/en-us/azure/vpn-gateway/media/vpn-gateway-about-point-to-site-routing/isolated.jpg#lightbox)