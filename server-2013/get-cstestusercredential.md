﻿---
title: Get-CsTestUserCredential
TOCTitle: Get-CsTestUserCredential
ms:assetid: 2af8d526-005c-40fb-957c-5b2ee5bce432
ms:mtpsurl: https://technet.microsoft.com/en-us/library/JJ204759(v=OCS.15)
ms:contentKeyID: 48183692
ms.date: 07/23/2014
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Get-CsTestUserCredential

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2014-03-19_

Returns information that tells you whether or not a user has been configured as a watcher node test user. Watcher nodes are computers that periodically use Microsoft System Center Operations Manager and Lync Server 2013 synthetic transactions to verify that Lync Server components are working as expected. This cmdlet was introduced in Lync Server 2013.

<div>

## Syntax

    Get-CsTestUserCredential -SipAddress <String>

</div>

<span id="Examples"></span>

<div>

## Examples

<div>

## Example 1

The command shown in Example 1 returns information for the user sip:kenmyer@litwareinc.com provided that the user has been configured as a watcher node test user. If the user has not been configured as a test user then the **Get-CsTestUserCredential** cmdlet will return an error.

    Get-CsTestUserCredential -SipAddress "sip:kenmyer@litewareinc.com"

</div>

<div>

## Example 2

The commands shown in Example 2 return a list of all the users who have been configured as watcher node test users. To do this, the first command in the example sets the value of the Windows PowerShell command-line interface $ErrorActionPreference variable to "SilentlyContinue"; this suppresses the display of any error messages that would otherwise appear if the **Get-CsTestUserCredential** cmdlet tries to return test user information for a user who has not been configured as a watcher node test user.

With the error messages suppressed, the second command in the example uses the **Get-CsUser** cmdlet to return a collection of all the users who have been enabled for Lync Server 2013. This collection is then piped to the **ForEach-Object** cmdlet. The **ForEach-Object** cmdlet loops through each user account in the collection, running the **Get-CsTestUserCredential** cmdlet against each account to see if the user has been configured as a test user. If the user has been configured as a test user then information about that user will be displayed on screen. If the user has not been configured as a test user then nothing will be displayed on screen.

The final command in the example resets the value of $ErrorActionPreference to "Continue".

    $ErrorActionPreference = "SilentlyContinue"
    Get-CsUser | ForEach-Object {Get-CsTestUserCredential -SipAddress $_.SipAddress}
    $ErrorActionPreference = "Continue"

</div>

</div>

<span id="DetailedDescription"></span>

<div>

## Detailed Description

If you are using System Center Operations Manager in conjunction with Lync Server 2013, you have the option of configuring "watcher node" computers. Watcher nodes are computers that periodically (and automatically) run synthetic transactions. Synthetic transactions are cmdlets that test various features of Lync Server; for example, there are synthetic transactions that verify that users can register with Lync Server; that users can exchange instant messages and presence information using Lync Server; that users can conduct data collaboration and application sharing conferences; and that users can make phone calls across the public switched telephone network. As noted, these synthetic transactions run periodically and, if they fail, issue alerts notifying administrators that the system might be experiencing difficulties.

Many synthetic transactions require test users; for example, you cannot test the ability of two users to exchange instant messages unless you have a pair of user accounts and you attempt to exchange instant messages using those accounts. When you configure a watcher node you must assign at least two test users to that node. These test users can be any valid Active Directory user accounts that have been enabled for Lync Server 2013 and have been registered as test accounts. Accounts are registered as test accounts by using the [Set-CsTestUserCredential](set-cstestusercredential.md) cmdlet. If you later decide not to use an account as a test account you can unregister the by using the [Remove-CsTestUserCredential](remove-cstestusercredential.md) cmdlet. This cmdlet simply prevents the account from being used as a watcher node test account; it does not delete, disable, or otherwise modify the account.

To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Get-CsTestUserCredential"}

**Lync Server Control Panel:** The functions carried out by the **Get-CsTestUserCredential** cmdlet are not available in the Lync Server Control Panel.

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
<td><p><em>SipAddress</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>SIP address of the account being checked for test user credentials. For example:</p>
<p>-SipAddress &quot;sip:kenmyer@litwareinc.com&quot;</p>
<p>You must include the SipAddress parameter when calling the <strong>Get-CsTestUserCredential</strong> cmdlet. If you do not, you will be prompted to enter that address.</p></td>
</tr>
</tbody>
</table>


</div>

<span id="InputTypes"></span>

<div>

## Input Types

None. The **Get-CsTestUserCredential** cmdlet does not accept pipelined input.

</div>

<span id="ReturnTypes"></span>

<div>

## Return Types

The **Get-CsTestUserCredential** cmdlet returns instances of the System.Management.Automation.PSCredential object.

</div>

<div>

## See Also


[Remove-CsTestUserCredential](remove-cstestusercredential.md)  
[Set-CsTestUserCredential](set-cstestusercredential.md)  
  

</div>

</div>

<span> </span>

</div>

</div>

</div>

