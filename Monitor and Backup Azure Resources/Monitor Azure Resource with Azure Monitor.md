(AZ-104 | Tim Warner | Puralsight)

# <ins>**Monitor Resource with Azure Monitor**</ins>

---

## <ins>*Configuring Microsoft Azure Resource Monitoring*</ins>

### *Azure Monitor Data Sources*

![Azure Monitor Data Sources](https://docs.microsoft.com/en-us/azure/azure-monitor/media/overview/overview.png)

### *Diagnostic Settings for Logs & Metrics*

- For Azure Resources
- Log Analytics Workspace
  - PaaS
- Event Hub
  - PaaS
  - Telemetry
- Storage Account
  - Original repository option, last resort for compliance or long-term retention.

### *Enable Diagnostics - Azure PowerShell*

```PowerShell

Set-AzDiagnosticSetting - Name KeyVault-Diagnostics `
    -ResourceId /subscriptions/.../Microsoft.KeyVault/vaults/mykeyvault `
    -Category AuditEvent -MetricCategory AllMetrics -Enabled $true `
    -StorageAccountId /../Microsoft.Storage/storageAccounts/mystorageaccount `
    -WorkspaceId /.../workspaces/myworkspace `
    -EventHubAuthorizationRuleId /.../RootManageSharedAccessKey

```

### <ins>*Azure Virtual Machine Agents*</ins>

- VM Diagnostics Extension
- Log Analytics Agent
- Dependency Agent

### *Metrics Explorer*

- Plot live metrics data for any Azure resources
- Can Pin to Dashboard
- Can share a permalink URL with colleagues
- Can raise alerts based on metrics shows

### <ins>*Log Analytics (Azure Monitor Logs)*</ins>

- Data Sources sending log data in to centralized *workspaces*
- Workspace provides uniform data tables no matter the base data formatting
- Uses KQL (Kusto Query Language)

### <ins>*Application Insights*</ins>

- Application Performance Management (APM) service
  - PaaS
  - Visualize application performance
    - Host Telemetry
    - Dependencies
    - User Behavior
    - Performance Anomalies
  - Web test with synthetic transactions
  - Service Map

---

## <ins>**Monitoring and Reporting on Microsoft Azure Resources**</ins>

### <ins>*Log Search Workflow*</ins>

- Configure diagnostics properly
- Determine what information you are after
- Run the query
- Take relevant action

### <ins>*Application Insights Components*</ins>

- Smart Detection
  - Live anomaly detection
  - Integrates with IDE
- Application Map
  - Visualize Dependencies
- Profiles
  - Execution data for web requests
- Usage Analysis
  - User segmentation and retention
- Live Metrics
  - Stream to dashboards

### <ins>*Azure Monitor Alert Workflow*</ins>

- Alert Rule
  - Target Resource
    - Signal
      - Criterial/Logic Test
        - Action Group
          - Actions to-do
        - Monitor Condition
          - Alert State

> *It is best practice to create Action Groups prior to creating actions so they can be applied to the appropriate group as you go.*
