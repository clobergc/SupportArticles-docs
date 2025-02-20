---
title: Gather information by using TSSv2 for Active Directory replication issues
description: Introduces how to gather information by using the TroubleShootingScript Version 2 (TSSv2) toolset for Active Directory replication issues.
ms.date: 04/21/2023
author: v-lianna
ms.author: v-lianna
manager: dcscontentpm
audience: itpro
ms.topic: troubleshooting
ms.prod: windows-client
localization_priority: medium
ms.reviewer: kaushika, warrenw
ms.custom: sap:windows-troubleshooters, csstroubleshoot
ms.technology: windows-client-troubleshooter
---
# Gather information by using TSSv2 for Active Directory replication issues

This article introduces how to gather information by using the TroubleShootingScript Version 2 (TSSv2) toolset for Active Directory replication issues.

Before contacting Microsoft support, you can gather information about your issue.

## Prerequisites

Refer to [Introduction to TroubleShootingScript toolset (TSSv2)](introduction-to-troubleshootingscript-toolset-tssv2.md#prerequisites) for prerequisites for the toolset to run properly.

## Gather key information before contacting Microsoft support

1. Download [TSSv2](https://aka.ms/getTSSv2) and extract it in the *C:\\tss_tool* folder.
2. Open the *C:\\tss_tool* folder from an elevated PowerShell command prompt.  
    > [!NOTE]
    > Don't use the Windows PowerShell Integrated Scripting Environment (ISE).
3. Run the following cmdlets:

    ```powershell
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
    ```

    ```powershell
    .\TSSv2.ps1 -Start -Scenario ADS_General -noProcmon -noPSR -noVideo
    ```

4. Enter *A* for "Yes to All" for the execution policy change.

> [!NOTE]
>
> - The traces are stored in a compressed file in the *C:\\MSDATA* folder. After a support case is created, this file can be uploaded to the secure workspace for analysis.
> - If you've downloaded this tool previously, we recommend downloading the latest version. It doesn't automatically update when running `-Start -Scenario ADS_General -noProcmon -noPSR -noVideo`.
