---
title: 'Disable PTA when using Azure AD Connect "Do not configure" | Microsoft Docs'
description: This article describes how to disable PTA with the Azure AD Connect "do not configure" feature.
services: active-directory
author: billmath
manager: karenhoran
ms.service: active-directory
ms.topic: how-to
ms.workload: identity
ms.date: 01/21/2022
ms.subservice: hybrid
ms.author: billmath
ms.collection: M365-identity-device-management
---

# Disable PTA 

To disable PTA, complete the steps that are described in [Disable PTA when using Azure AD Connect](#disable-pta-when-using-azure-ad-connect) and [Disable PTA in PowerShell](#disable-pta-in-powershell) in this article.

## Disable PTA when using Azure AD Connect

If you are using Pass-through Authentication with Azure AD Connect and you have it set to **"Do not configure"**, you can disable it. 

>[!NOTE]
>If you have PHS already enabled then disabling PTA will result in the tenant fallback to PHS.

Disabling PTA can be done using the following cmdlets. 

## Prerequisites
The following prerequisites are required:
- Any Windows machine that has the PTA agent installed. 
- Agent must be at version 1.5.1742.0 or later. 
- An Azure global administrator account in order to run the PowerShell cmdlets to disable PTA.

>[!NOTE]
> If your agent is older then it may not have the cmdlets required to complete this operation. You can get a new agent from Azure Portal an install it on any Windows machine and provide admin credentials. (Installing the agent does not affect the PTA status in the cloud)

> [!IMPORTANT]
> If you are using the Azure Government cloud then you will have to pass in the ENVIRONMENTNAME parameter with the following value. 
>
>| Environment Name | Cloud |
>| - | - |
>| AzureUSGovernment | US Gov|


## Disable PTA in PowerShell

From within a PowerShell session, use the following to disable PTA:

1. PS C:\Program Files\Microsoft Azure AD Connect Authentication Agent> `Import-Module .\Modules\PassthroughAuthPSModule`
2. `Get-PassthroughAuthenticationEnablementStatus`
3. `Disable-PassthroughAuthentication`

## If you don't have access to an agent

If you do not have an agent machine you can use following command to install an agent.

1. Download the latest Auth Agent from portal.azure.com.
2. Install the feature: `.\AADConnectAuthAgentSetup.exe` or `.\AADConnectAuthAgentSetup.exe ENVIRONMENTNAME=<identifier>`


## Next steps

- [User sign-in with Azure Active Directory Pass-through Authentication](how-to-connect-pta.md)
