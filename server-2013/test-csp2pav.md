﻿---
title: Test-CsP2PAV
TOCTitle: Test-CsP2PAV
ms:assetid: acb01fb7-4685-4f38-a724-8c2ae8e0219a
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg412821(v=OCS.15)
ms:contentKeyID: 48185120
ms.date: 07/23/2014
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Test-CsP2PAV

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2013-03-25_

Tests the ability of a pair of users to conduct a peer-to-peer audio/video (A/V) call. This cmdlet was introduced in Lync Server 2010.

<div>

## Syntax

    Test-CsP2PAV -ReceiverCredential <PSCredential> -ReceiverSipAddress <String> -SenderCredential <PSCredential> -SenderSipAddress <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-RegistrarPort <Int32>] [-TargetFqdn <String>] <COMMON PARAMETERS>

    Test-CsP2PAV -TargetFqdn <String> [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] [-ReceiverSipAddress <String>] [-RegistrarPort <Int32>] [-SenderSipAddress <String>] <COMMON PARAMETERS>

    Test-CsP2PAV [-Authentication <TrustedServer | Negotiate | ClientCertificate | LiveID>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Force <SwitchParameter>] [-OutLoggerVariable <String>] [-OutVerboseVariable <String>]

</div>

<div>

## Examples

<div>

## EXAMPLE 1

Example 1 checks to see if a pair of preconfigured test users can log on to the pool atl-cs-001.litwareinc.com and then conduct a peer-to-peer audio/video call. This command will work only if test users have been defined for the pool atl-cs-001.litwareinc.com. If they have, then the command will determine whether the two users can log on to the system and, if so, can converse using an audio/video call.

If test users have not been defined then the command will fail because it will not know which users to employ when doing the test. If you have not defined test users for a pool, then you must include the SenderSipAddress and ReceiverSipAddress parameters as well as the corresponding credentials for the users involved in the instant message exchange. The **Test-CsP2PAV** cmdlet will then conduct its checks using the two specified users.

    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com 

</div>

<div>

## EXAMPLE 2

The commands shown in Example 2 test the ability of a pair of users (litwareinc\\pilar and litwareinc\\kenmyer) to log on to Lync Server and then conduct a peer-to-peer audio/video call. To do this, the first command in the example uses the **Get-Credential** cmdlet to create a Windows PowerShell credential object containing the name and password of the user Pilar Ackerman. (Because the logon name, litwareinc\\pilar, has been included as a parameter, the Windows PowerShell Credential Request dialog box only requires the administrator to enter the password for the Pilar Ackerman account.) The resulting credentials object is then stored in a variable named $cred1. The second command does the same thing, this time returning a credential object for the Ken Myer account.

With the two credential objects in hand, the third command in the example determines whether or not the two users can log on to Lync Server and conduct a peer-to-peer audio/video call. To carry out this task, the **Test-CsP2PAV** cmdlet is called, along with the following parameters: TargetFqdn (the FQDN of the Registrar pool); SenderSipAddress (the SIP address for the first test user); SenderCredential (the Windows PowerShell object containing the credentials for this same user); ReceiverSipAddress (the SIP address for the other test user); and ReceiverCredential (the Windows PowerShell object containing the credentials for the other test user).

    $cred1 = Get-Credential "litwareinc\pilar"
    $cred2 = Get-Credential "litwareinc\kenmyer"
    
    Test-CsP2PAV -TargetFqdn atl-cs-001.litwareinc.com -SenderSipAddress "sip:pilar@litwareinc.com" -SenderCredential $cred1 -ReceiverSipAddress "sip:kenmyer@litwareinc.com" -ReceiverCredential $cred2

</div>

</div>

<div>

## Detailed Description

The **Test-CsP2PAV** cmdlet is an example of a Lync Server "synthetic transaction." Synthetic transactions are used in Lync Server to verify that users are able to successfully complete common tasks such as logging on to the system, exchanging instant messages, or making calls to a phone located on the public switched telephone network (PSTN). These tests can be conducted manually by an administrator, or they can be automatically run by an application such as Microsoft System Center Operations Manager (formerly Microsoft Operations Manager).

Synthetic transactions are typically conducted in two different ways. Many administrators will use the **CsHealthMonitoringConfiguration** cmdlets to set up test users for each of their Registrar pools. These test users are a pair of users who have been preconfigured for use with synthetic transactions. (Typically these are test accounts and not accounts that belong to actual users.) With test users configured for a pool, administrators can simply run a synthetic transaction against that pool without having to specify the identities of (and supply the credentials for) the user accounts involved in the test.

Alternatively, administrators can run a synthetic transaction using actual user accounts. For example, if two users are unable to exchange instant messages, an administrator could run a synthetic transaction using the two user accounts in question (as opposed to a pair of test accounts) and try to diagnose and resolve the problem. If you decide to conduct a synthetic transaction using actual user accounts you will need to supply the logon names and passwords for each user.

The **Test-CsP2PAV** cmdlet is used to determine whether two test users are able to participate in a peer-to-peer audio/video (A/V) conversation. To test this scenario, the cmdlet starts off by logging the two users on to Lync Server. Assuming that the two logons succeed, the first user then invites the second user to join an A/V call. The second user accepts the call, the connection between the two users is tested, and then the call is ended and the test users are logged off from the system.

The **Test-CsP2PAV** cmdlet does not actually conduct an A/V call; multimedia information is not exchanged between the test users. Instead, the cmdlet simply verifies that the appropriate connections can be made and that the two users are capable of conducting such a call.

Who can run this cmdlet: To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Test-CsP2PAV"}

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
<td><p><em>ReceiverCredential</em></p></td>
<td><p>Required</p></td>
<td><p>PSCredential</p></td>
<td><p>User credential object for the first of the two user accounts to be tested. The value passed to ReceiverCredential should be an object reference obtained by using the <strong>Get-Credential</strong> cmdlet. For example, this code returns a credentials object for the user litwareinc\pilar and stores that object in a variable named $y:</p>
<p>$y = Get-Credential &quot;litwareinc\pilar&quot;</p>
<p>You need to supply the user password when running this command.</p>
<p>The receiver credential is not required if you are running the test under the health monitoring configuration settings for the pool.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderCredential</em></p></td>
<td><p>Required</p></td>
<td><p>PSCredential</p></td>
<td><p>User credential object for the second of the two user accounts to be tested. The value passed to SenderCredential should be an object reference obtained by using the <strong>Get-Credential</strong> cmdlet. For example, this code returns a credentials object for the user litwareinc\kenmyer and stores that object in a variable named $x:</p>
<p>$x = Get-Credential &quot;litwareinc\kenmyer&quot;</p>
<p>You need to supply the user password when running this command.</p>
<p>The sender credential is not required if you are running the test under the health monitoring configuration settings for the pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>TargetFqdn</em></p></td>
<td><p>Required</p></td>
<td><p>String</p></td>
<td><p>Fully qualified domain name (FQDN) of the pool to be tested.</p></td>
</tr>
<tr class="even">
<td><p><em>Authentication</em></p></td>
<td><p>Optional</p></td>
<td><p>SipSyntheticTransaction AuthenticationMechanism</p></td>
<td><p>Type of authentication used in the test. Allowed values are:</p>
<p>* TrustedServer</p>
<p>* Negotiate</p>
<p>* ClientCertificate</p>
<p>* LiveID</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suppresses the display of any non-fatal error message that might occur when running the command.</p></td>
</tr>
<tr class="even">
<td><p><em>OutLoggerVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>When present, detailed output from running the cmdlet will be stored in the specified variable. This variable includes a pair of methods – ToHTML and ToXML – that can then be used to save that output to either an HTML or an XML file.</p>
<p>To store output in a logger variable named $TestOutput use the following syntax:</p>
<p>-OutLoggerVariable TestOutput</p>
<p>Note: Do not use prepend a $ character when specifying the variable name.To save the information stored in the logger variable to an HTML file, use a command similar to this:</p>
<p>$TestOutput.ToHTML() &gt; C:\Logs\TestOutput.html</p>
<p>To save the information stored in the logger variable to an XML file, use a command similar to this:</p>
<p>$TestOutput.ToXML() &gt; C:\Logs\TestOutput.xml</p></td>
</tr>
<tr class="odd">
<td><p><em>OutVerboseVariable</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>When present, detailed output from running the cmdlet will be stored in the specified variable. For example, to store output in a variable named $TestOutput use the following syntax:</p>
<p>-OutVerboseVariable TestOutput</p>
<p>Do not prepend a $ character when specifying the variable name.</p></td>
</tr>
<tr class="even">
<td><p><em>ReceiverSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>SIP address for the first of the two user accounts to be tested. For example: -ReceiverSipAddress &quot;sip:pilar@litwareinc.com&quot;. The ReceiverSipAddress parameter must reference the same user account as ReceiverCredential.</p>
<p>The SIP address is not required if you are running the test under the health monitoring configuration settings for the pool.</p></td>
</tr>
<tr class="odd">
<td><p><em>RegistrarPort</em></p></td>
<td><p>Optional</p></td>
<td><p>Int32</p></td>
<td><p>SIP port used by the Registrar service. This parameter is not required if the Registrar uses the default port 5061.</p></td>
</tr>
<tr class="even">
<td><p><em>SenderSipAddress</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>SIP address for the second of the two user accounts to be tested. For example: -SenderSipAddres &quot;sip:kenmyer@litwareinc.com&quot;. The SenderSipAddress parameter must reference the same user account as SenderCredential.</p>
<p>The SIP address is not required if you are running the test under the health monitoring configuration settings for the pool.</p></td>
</tr>
</tbody>
</table>


</div>

<div>

## Input Types

None. The **Test-CsP2PAV** cmdlet does not accept pipelined input.

</div>

<div>

## Return Types

The **Test-CsP2PAV** cmdlet returns an instance of the Microsoft.Rtc.SyntheticTransactions.TaskOutput object.

</div>

<div>

## See Also


[Test-CsAVConference](test-csavconference.md)  
  

</div>

</div>

<span> </span>

</div>

</div>

</div>

