﻿---
title: Remove-CsBandwidthPolicyServiceConfiguration
TOCTitle: Remove-CsBandwidthPolicyServiceConfiguration
ms:assetid: cf920168-3f65-4747-86cd-d3e287c84349
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg398877(v=OCS.15)
ms:contentKeyID: 48185516
ms.date: 07/23/2014
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Remove-CsBandwidthPolicyServiceConfiguration

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2013-02-21_

Removes an existing bandwidth policy service configuration. This cmdlet was introduced in Lync Server 2010.

<div>

## Syntax

    Remove-CsBandwidthPolicyServiceConfiguration -Identity <XdsIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

</div>

<div>

## Examples

<div>

## EXAMPLE 1

This example removes the bandwidth policy service configuration defined for the Redmond site (-Identity site:Redmond).

    Remove-CsBandwidthPolicyServiceConfiguration -Identity site:Redmond

</div>

<div>

## EXAMPLE 2

Example 2 removes all bandwidth policy service configurations where logging is disabled. To accomplish this, the example begins with a call to the **Get-CsBandwidthPolicyServiceConfiguration** cmdlet. This will return a collection of all bandwidth policy service configurations in the Lync Server deployment. This collection is then piped to the **Where-Object** cmdlet, which narrows the collection down to only those configurations where the EnableLogging property is equal to (-eq) False ($False). This leaves a collection of configurations that have logging disabled. This collection is then piped to the **Remove-CsBandwidthPolicyServiceConfiguration** cmdlet, which removes every item in the collection.

    Get-CsBandwidthPolicyServiceConfiguration | Where-Object {$_.EnableLogging -eq $False} | Remove-CsBandwidthPolicyServiceConfiguration

</div>

</div>

<div>

## Detailed Description

Call admission control (CAC) is a way of determining whether to allow real-time communications sessions, such as voice or video calls, to be established based on bandwidth constraints. Within the Lync Server implementation of CAC, regions, sites, and subnets are defined within a network along with the relationships and links between those entities in order to place bandwidth constraints between them. Bandwidth Policy service is the component that performs CAC functionality in the Lync Server deployment, enabling the decision as to whether sufficient bandwidth exists for a call to be established. This cmdlet removes a bandwidth policy service configuration defined at the site level. You can also use the cmdlet to “remove” the global bandwidth policy service; however, the global service will not actually be removed, it will simply be reset to its default values.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Remove-CsBandwidthPolicyServiceConfiguration** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsBandwidthPolicyServiceConfiguration"}

</div>

<div>

## Parameters


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Required</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>Required</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>The unique identifier of the configuration you want to remove. This identifier will consist of the scope (for the global configuration) or the scope and name (for a site-level configuration, such as site:Redmond).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Prompts you for confirmation before executing the command.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describes what would happen if you executed the command without actually executing the command.</p></td>
</tr>
</tbody>
</table>


</div>

<div>

## Input Types

Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration object. Accepts pipelined input of bandwidth policy service configuration objects.

</div>

<div>

## Return Types

This cmdlet does not return a value. It removes an object of type Microsoft.Rtc.Management.WritableConfig.Settings.BandwidthPolicyServiceConfiguration.BandwidthPolicyServiceConfiguration.

</div>

<div>

## See Also


[New-CsBandwidthPolicyServiceConfiguration](new-csbandwidthpolicyserviceconfiguration.md)  
[Set-CsBandwidthPolicyServiceConfiguration](set-csbandwidthpolicyserviceconfiguration.md)  
[Get-CsBandwidthPolicyServiceConfiguration](get-csbandwidthpolicyserviceconfiguration.md)  
  

</div>

</div>

<span> </span>

</div>

</div>

</div>

