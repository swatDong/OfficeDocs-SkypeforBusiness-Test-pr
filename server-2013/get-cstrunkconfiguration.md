﻿---
title: Get-CsTrunkConfiguration
TOCTitle: Get-CsTrunkConfiguration
ms:assetid: 15951113-5f96-4f44-8cad-9ff97fb5dfd6
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg398224(v=OCS.15)
ms:contentKeyID: 48183496
ms.date: 07/23/2014
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Get-CsTrunkConfiguration

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2012-08-13_

Retrieves one or more trunk configurations, which describe the settings for a trunking peer entity such as a public switched telephone network (PSTN) gateway, IP-private branch exchange (PBX), or Session Border Controller (SBC) at the service provider. This cmdlet was introduced in Lync Server 2010.

<div>

## Syntax

    Get-CsTrunkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Get-CsTrunkConfiguration [-Filter <String>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-LocalStore <SwitchParameter>]

</div>

<div>

## Examples

<div>

## EXAMPLE 1

This example retrieves all trunk configurations for the Lync Server deployment.

    Get-CsTrunkConfiguration

</div>

<div>

## EXAMPLE 2

This example retrieves the trunk configuration with the Identity site:Redmond. Because identities are unique, this command will return at most one object.

    Get-CsTrunkConfiguration -Identity site:Redmond

</div>

<div>

## EXAMPLE 3

Example 3 retrieves all trunk configurations defined at the site level. The **Get-CsTrunkConfiguration** cmdlet uses the Filter parameter to retrieve all trunk configurations with an Identity beginning with site:, meaning all trunk configurations defined at the site level.

    Get-CsTrunkConfiguration -Filter site:*

</div>

</div>

<div>

## Detailed Description

Use this cmdlet to retrieve one or more trunking configurations applicable to PSTN gateway entities. Each configuration contains specific settings for a trunking peer entity such as a PSTN gateway, IP-PBX, or SBC at the service provider. These settings configure such things as whether media bypass is enabled on this trunk, whether real-time transport control protocol (RTCP) packets are sent under certain conditions, and whether to require secure real-time protocol (SRTP) encryption.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Get-CsTrunkConfiguration** cmdlet locally: RTCUniversalUserAdmins, RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTrunkConfiguration"}

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
<td><p><em>Filter</em></p></td>
<td><p>Optional</p></td>
<td><p>System.String</p></td>
<td><p>This parameter accepts a wildcard string and returns all trunk configurations with identities matching that string. For example, a Filter value of site:* will return all trunk configurations defined at the site level.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>The unique identifier of the trunk configuration you want to retrieve. Trunk configurations can be defined at the Global scope, the Site scope, or at the Service scope for a PSTN Gateway service. For example, site:Redmond (for site) or PstnGateway:Redmond.litwareinc.com (for service).</p></td>
</tr>
<tr class="odd">
<td><p><em>LocalStore</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Retrieves the trunk configuration from the local replica of the Central Management store, rather than the Central Management store itself.</p></td>
</tr>
</tbody>
</table>


</div>

<div>

## Input Types

None.

</div>

<div>

## Return Types

This cmdlet returns an object of type Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration.

</div>

<div>

## See Also


[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Set-CsTrunkConfiguration](set-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
  

</div>

</div>

<span> </span>

</div>

</div>

</div>

