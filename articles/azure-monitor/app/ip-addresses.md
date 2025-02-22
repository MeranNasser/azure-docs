---
title: IP addresses used by Azure Monitor
description: Server firewall exceptions required by Application Insights
ms.topic: conceptual
ms.date: 01/27/2020

---

# IP addresses used by Azure Monitor

[Azure Monitor](../overview.md) uses a number of IP addresses. Azure Monitor is made up of core platform metrics and log in addition to Log Analytics and Application Insights. You might need to know these addresses if the app or infrastructure that you are monitoring is hosted behind a firewall.

> [!NOTE]
> Although these addresses are static, it's possible that we will need to change them from time to time. All Application Insights traffic represents outbound traffic with the exception of availability monitoring and webhooks which require inbound firewall rules.

> [!TIP]
> You can use Azure [network service tags](../../virtual-network/service-tags-overview.md) to manage access if you are using Azure Network Security Groups. If you are managing access for hybrid/on premises resources you can download the equivalent IP address lists as [JSON files](../../virtual-network/service-tags-overview.md#discover-service-tags-by-using-downloadable-json-files) which are updated each week. To cover all the exceptions in this article you would need to use the service tags: `ActionGroup`, `ApplicationInsightsAvailability`, and `AzureMonitor`.

Alternatively, you can subscribe to this page as a RSS feed by adding https://github.com/MicrosoftDocs/azure-docs/blob/main/articles/azure-monitor/app/ip-addresses.md to your favorite RSS/ATOM reader to get notified of the latest changes.


## Outgoing ports

You need to open some outgoing ports in your server's firewall to allow the Application Insights SDK and/or Status Monitor to send data to the portal:

| Purpose | URL | IP | Ports |
| --- | --- | --- | --- |
| Telemetry |dc.applicationinsights.azure.com<br/>dc.applicationinsights.microsoft.com<br/>dc.services.visualstudio.com<br/>*.in.applicationinsights.azure.com | | 443 |
| Live Metrics Stream | live.applicationinsights.azure.com<br/>rt.applicationinsights.microsoft.com<br/>rt.services.visualstudio.com|23.96.28.38<br/>13.92.40.198<br/>40.112.49.101<br/>40.117.80.207<br/>157.55.177.6<br/>104.44.140.84<br/>104.215.81.124<br/>23.100.122.113| 443 |

## Status Monitor

Status Monitor Configuration - needed only when making changes.

| Purpose | URL | IP | Ports |
| --- | --- | --- | --- |
| Configuration |`management.core.windows.net` | |`443` |
| Configuration |`management.azure.com` | |`443` |
| Configuration |`login.windows.net` | |`443` |
| Configuration |`login.microsoftonline.com` | |`443` |
| Configuration |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| Configuration |`auth.gfx.ms` | |`443` |
| Configuration |`login.live.com` | |`443` |
| Installation | `globalcdn.nuget.org`, `packages.nuget.org` ,`api.nuget.org/v3/index.json` `nuget.org`, `api.nuget.org`, `dc.services.vsallin.net` | |`443` |

## Availability tests

This is the list of addresses from which [availability web tests](./monitor-web-app-availability.md) are run. If you want to run web tests on your app, but your web server is restricted to serving specific clients, then you will have to permit incoming traffic from our availability test servers.


> [!NOTE]
> For resources located inside private virtual networks that cannot allow direct inbound communication with the availability test agents in public Azure, the only option is to [create and host your own custom availability tests](availability-azure-functions.md).

### Service tag

If you are using Azure Network Security Groups, simply add an **inbound port rule** to allow traffic from Application Insights availability tests by selecting **Service Tag** as the **Source** and **ApplicationInsightsAvailability** as the **Source service tag**.

>[!div class="mx-imgBorder"]
>![Under settings select Inbound security rules and then select add at the top of the tab ](./media/ip-addresses/add-inbound-security-rule.png)

>[!div class="mx-imgBorder"]
>![Add inbound security rule tab](./media/ip-addresses/add-inbound-security-rule2.png)

Open ports 80 (http) and 443 (https) for incoming traffic from these addresses (IP addresses are grouped by location):

### IP Addresses

If you're looking for the actual IP addresses so you can add them to the list of allowed IP's in your firewall, please download the JSON file describing Azure IP Ranges. These files contain the most up-to-date information. For Azure public cloud, you may also look up the IP address ranges by location using the table below.

After downloading the appropriate file, open it using your favorite text editor and search for "ApplicationInsightsAvailability" to go straight to the section of the file describing the service tag for availability tests.

> [!NOTE]
> These addresses are listed using Classless Inter-Domain Routing (CIDR) notation. This means that an entry like `51.144.56.112/28` is equivalent to 16 IPs starting at `51.144.56.112` and ending at `51.144.56.127`.

#### Azure Public Cloud
Download [Public Cloud IP addresses](https://www.microsoft.com/download/details.aspx?id=56519).

#### Azure US Government Cloud
Download [Government Cloud IP addresses](https://www.microsoft.com/download/details.aspx?id=57063).

#### Azure China Cloud
Download [China Cloud IP addresses](https://www.microsoft.com/download/details.aspx?id=57062).

#### Addresses grouped by location (Azure Public Cloud)

```
Australia East
20.40.124.176/28


Brazil South
191.233.26.176/28


France Central (Formerly France South)
20.40.129.96/28


France Central
20.40.129.32/28


East Asia
52.229.216.48/28


North Europe
52.158.28.64/28


Japan East
52.140.232.160/28


West Europe
51.144.56.96/28


UK South
51.105.9.128/28


UK West
20.40.104.96/28


Southeast Asia
52.139.250.96/28


West US
40.91.82.48/28


Central US
13.86.97.224/28


North Central US
23.100.224.16/28


South Central US
20.45.5.160/28

East US
20.42.35.32/28


```

### Discovery API
You may also want to [programmatically retrieve](../../virtual-network/service-tags-overview.md#use-the-service-tag-discovery-api) the current list of service tags together with IP address range details.

## Application Insights & Log Analytics APIs

| Purpose | URI |  IP | Ports |
| --- | --- | --- | --- |
| API |`api.applicationinsights.io`<br/>`api1.applicationinsights.io`<br/>`api2.applicationinsights.io`<br/>`api3.applicationinsights.io`<br/>`api4.applicationinsights.io`<br/>`api5.applicationinsights.io`<br/>`dev.applicationinsights.io`<br/>`dev.applicationinsights.microsoft.com`<br/>`dev.aisvc.visualstudio.com`<br/>`www.applicationinsights.io`<br/>`www.applicationinsights.microsoft.com`<br/>`www.aisvc.visualstudio.com`<br/>`api.loganalytics.io`<br/>`*.api.loganalytics.io`<br/>`dev.loganalytics.io`<br>`docs.loganalytics.io`<br/>`www.loganalytics.io` |20.37.52.188 <br/> 20.37.53.231 <br/> 20.36.47.130 <br/> 20.40.124.0 <br/> 20.43.99.158 <br/> 20.43.98.234 <br/> 13.70.127.61 <br/> 40.81.58.225 <br/> 20.40.160.120 <br/> 23.101.225.155 <br/> 52.139.8.32 <br/> 13.88.230.43 <br/> 52.230.224.237 <br/> 52.242.230.209 <br/> 52.173.249.138 <br/> 52.229.218.221 <br/> 52.229.225.6 <br/> 23.100.94.221 <br/> 52.188.179.229 <br/> 52.226.151.250 <br/> 52.150.36.187 <br/> 40.121.135.131 <br/> 20.44.73.196 <br/> 20.41.49.208 <br/> 40.70.23.205 <br/> 20.40.137.91 <br/> 20.40.140.212 <br/> 40.89.189.61 <br/> 52.155.118.97 <br/> 52.156.40.142 <br/> 23.102.66.132 <br/> 52.231.111.52 <br/> 52.231.108.46 <br/> 52.231.64.72 <br/> 52.162.87.50 <br/> 23.100.228.32 <br/> 40.127.144.141 <br/> 52.155.162.238 <br/> 137.116.226.81 <br/> 52.185.215.171 <br/> 40.119.4.128 <br/> 52.171.56.178 <br/> 20.43.152.45 <br/> 20.44.192.217 <br/> 13.67.77.233 <br/> 51.104.255.249 <br/> 51.104.252.13 <br/> 51.143.165.22 <br/> 13.78.151.158 <br/> 51.105.248.23 <br/> 40.74.36.208 <br/> 40.74.59.40 <br/> 13.93.233.49 <br/> 52.247.202.90 |80,443 |
| Azure Pipeline annotations extension | aigs1.aisvc.visualstudio.com |dynamic|443 | 

## Application Insights Analytics

| Purpose | URI | IP | Ports |
| --- | --- | --- | --- |
| Analytics Portal | analytics.applicationinsights.io | dynamic | 80,443 |
| CDN | applicationanalytics.azureedge.net | dynamic | 80,443 |
| Media CDN | applicationanalyticsmedia.azureedge.net | dynamic | 80,443 |

Note: *.applicationinsights.io domain is owned by Application Insights team.

## Log Analytics Portal

| Purpose | URI | IP | Ports |
| --- | --- | --- | --- |
| Portal | portal.loganalytics.io | dynamic | 80,443 |
| CDN | applicationanalytics.azureedge.net | dynamic | 80,443 |

Note: *.loganalytics.io domain is owned by the Log Analytics team.

## Application Insights Azure portal Extension

| Purpose | URI | IP | Ports |
| --- | --- | --- | --- |
| Application Insights Extension | stamp2.app.insightsportal.visualstudio.com | dynamic | 80,443 |
| Application Insights Extension CDN | insightsportal-prod2-cdn.aisvc.visualstudio.com<br/>insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com<br/>insightsportal-cdn-aimon.applicationinsights.io | dynamic | 80,443 |

## Application Insights SDKs

| Purpose | URI | IP | Ports |
| --- | --- | --- | --- |
| Application Insights JS SDK CDN | az416426.vo.msecnd.net<br/>js.monitor.azure.com | dynamic | 80,443 |

## Action Group webhooks

You can query the list of IP addresses used by Action Groups using the [Get-AzNetworkServiceTag PowerShell command](/powershell/module/az.network/Get-AzNetworkServiceTag).

### Action Groups Service Tag
Managing changes to Source IP addresses can be quite time consuming. Using **Service Tags** eliminates the need to update your configuration. A service tag represents a group of IP address prefixes from a given Azure service. Microsoft manages the IP addresses and automatically updates the service tag as addresses change, eliminating the need to update network security rules for an Action Group.

1. In the Azure portal under Azure Services search for *Network Security Group*.
2. Click on **Add** and create a Network Security Group.

   1. Add the Resource Group Name and then enter *Instance Details*.
   1. Click on **Review + Create** and then click *Create*.
   
   :::image type="content" source="../alerts/media/action-groups/action-group-create-security-group.png" alt-text="Example on how to create a Network Security Group."border="true":::

3. Go to Resource Group and then click on *Network Security Group* you have created.

    1. Select *Inbound Security Rules*.
    1. Click on **Add**.
    
    :::image type="content" source="../alerts/media/action-groups/action-group-add-service-tag.png" alt-text="Example on how to add a service tag." border="true":::

4. A new window will open in right pane.
    1.  Select Source: **Service Tag**
    1.  Source Service Tag: **ActionGroup**
    1.  Click **Add**.
    
    :::image type="content" source="../alerts/media/action-groups/action-group-service-tag.png" alt-text="Example on how to add service tag." border="true":::


## Profiler

| Purpose | URI | IP | Ports |
| --- | --- | --- | --- |
| Agent | agent.azureserviceprofiler.net<br/>*.agent.azureserviceprofiler.net | 20.190.60.38<br/>20.190.60.32<br/>52.173.196.230<br/>52.173.196.209<br/>23.102.44.211<br/>23.102.45.216<br/>13.69.51.218<br/>13.69.51.175<br/>138.91.32.98<br/>138.91.37.93<br/>40.121.61.208<br/>40.121.57.2<br/>51.140.60.235<br/>51.140.180.52<br/>52.138.31.112<br/>52.138.31.127<br/>104.211.90.234<br/>104.211.91.254<br/>13.70.124.27<br/>13.75.195.15<br/>52.185.132.101<br/>52.185.132.170<br/>20.188.36.28<br/>40.89.153.171<br/>52.141.22.239<br/>52.141.22.149<br/>102.133.162.233<br/>102.133.161.73<br/>191.232.214.6<br/>191.232.213.239 | 443
| Portal | gateway.azureserviceprofiler.net | dynamic | 443
| Storage | *.core.windows.net | dynamic | 443

## Snapshot Debugger

> [!NOTE]
> Profiler and Snapshot Debugger share the same set of IP addresses.

| Purpose | URI | IP | Ports |
| --- | --- | --- | --- |
| Agent | agent.azureserviceprofiler.net<br/>*.agent.azureserviceprofiler.net | 20.190.60.38<br/>20.190.60.32<br/>52.173.196.230<br/>52.173.196.209<br/>23.102.44.211<br/>23.102.45.216<br/>13.69.51.218<br/>13.69.51.175<br/>138.91.32.98<br/>138.91.37.93<br/>40.121.61.208<br/>40.121.57.2<br/>51.140.60.235<br/>51.140.180.52<br/>52.138.31.112<br/>52.138.31.127<br/>104.211.90.234<br/>104.211.91.254<br/>13.70.124.27<br/>13.75.195.15<br/>52.185.132.101<br/>52.185.132.170<br/>20.188.36.28<br/>40.89.153.171<br/>52.141.22.239<br/>52.141.22.149<br/>102.133.162.233<br/>102.133.161.73<br/>191.232.214.6<br/>191.232.213.239 | 443
| Portal | gateway.azureserviceprofiler.net | dynamic | 443
| Storage | *.core.windows.net | dynamic | 443
