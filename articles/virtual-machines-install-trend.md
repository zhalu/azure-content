<properties 
	pageTitle="How to install and configure Trend Micro Deep Security as a Service on an Azure VM" 
	description="Describes installing and configuring Trend Micro security on a VM in Azure" 
	services="virtual-machines" 
	documentationCenter="" 
	authors="KBDAzure" 
	manager="timlt" 
	editor=""/>

<tags 
	ms.service="virtual-machines" 
	ms.workload="infrastructure-services" 
	ms.tgt_pltfrm="vm-multiple" 
	ms.devlang="na" 
	ms.topic="article" 
<<<<<<< HEAD
	ms.date="09/24/2014" 
=======
	ms.date="02/17/2015" 
>>>>>>> 440cd6ceb9ad667ae1c98784b7b3fe20f52a31f4
	ms.author="kathydav"/>


# How to install and configure Trend Micro Deep Security as a Service on an Azure VM

This article shows you how to install and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server. The protection that Deep Security as a Service provides includes anti-malware protection, firewall, intrusion prevention system, and integrity monitoring. 

The client is installed as a security extension by using the VM Agent. On a new virtual machine, you'll install the VM Agent along with the Deep Security Agent. On an existing virtual machine that doesn't have the VM Agent, you'll need to download and install it first. This article covers both situations.

If you have existing subscription from Trend Micro for an on-premises solution, you can use it to protect your Azure virtual machines. If you're not a customer yet, you can sign up for a trial subscription. For more information about this solution, see the Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## Install the Deep Security Agent on a new virtual machine

The [Azure Management Portal](http://manage.windowsazure.com) lets you install the VM Agent and the Trend Micro security extension when you use the **From Gallery** option to create the virtual machine. Using this approach is an easy way to add protection from Trend Micro if you're creating a single virtual machine.

This **From Gallery** option opens a wizard that helps you set up the virtual machine. You use the last page of the wizard to install the VM Agent and Trend Micro security extension. For general instructions, see [Create a Virtual Machine Running Windows Server](../virtual-machines-windows-tutorial/). When you get to the last page of the wizard, do the following:

1.	Under VM Agent, check **Install VM Agent**.

2.	Under Security Extensions, check **Trend Micro Deep Security Agent**.

	![Install the VM Agent and the Deep Security Agent](./media/virtual-machines-install-trend/InstallVMAgentandTrend.png)

3.	Click the check mark to create the virtual machine.

## Install the Deep Security Agent on an existing virtual machine

To do this, you'll need the following:

- The Azure PowerShell module, version 0.8.2 or newer installed on your local computer. You can check the version of Azure PowerShell that you have installed with the **Get-Module azure | format-table version** command. For instructions and a link to the latest version, see [How to Install and Configure Azure PowerShell](../install-configure-powershell/). 

- The VM Agent installed on the target virtual machine. 

First, verify that the VM Agent is already installed. Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt. Replace everything within the quotes, including the < and > characters.

<<<<<<< HEAD
1.	Get the cloud service name, virtual machine name, and VM and store each of those in variables so the next commands can use them:
	<p>`$servicename = MyServiceName`
	<p>`$name = MyVmName`
	<p>`$vm = Get-AzureVM -ServiceName $servicename -Name $name`

	> [AZURE.NOTE] If you don't know the cloud service and VM name, run Get-AzureVM to display that information for all VMs in the current subscription.

2.	Add the Deep Security Agent to the virtual machine:
<p> `Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA -VM $vm.VM`

	> [AZURE.NOTE] If you want to install a specific version, run the following command to get a list of available versions: `Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA`. Then, include the Version parameter when you run Set-AzureVMExtension.
=======
	$CSName = "<cloud service name>"
	$VMName = "<virtual machine name>"
	$vm = Get-AzureVM -ServiceName $CSName -Name $VMName 
	write-host $vm.VM.ProvisionGuestAgent

If you don't know the cloud service and virtual machine name, run **Get-AzureVM** to display that information for all the virtual machines in your current subscription.
>>>>>>> 440cd6ceb9ad667ae1c98784b7b3fe20f52a31f4

If the **write-host** command returns **True**, the VM Agent is installed. If it returns **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).

If the VM Agent is installed, run these commands.

	$Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA
	Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## Next steps

It takes a few minutes for the agent to start running when it is installed. After that, you'll need to activate Deep Security on the virtual machine so it can be managed by a Deep Security Manager. See the following for additional instructions:

- Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101).
- A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) to configure the virtual machine.
- [Instructions](http://go.microsoft.com/fwlink/?LinkId=404099)  for the sample.

## Additional Resources

[How to Log on to a Virtual Machine Running Windows Server]

[Azure VM Extensions and Features]


<!--Link references-->
[How to Log on to a Virtual Machine Running Windows Server]: ../virtual-machines-log-on-windows-server/
[Azure VM Extensions and Features]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409

