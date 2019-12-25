<h1>Install IIS webserver on a VM with Azure Cloud Shell</h1>
<h2>Use Case</h2>
<p>Students can just read through the tasks and get a feel for how it works or actually step through it like a lab task.</p> 
<p>Another option could be to complete the walkthrough at the end of the module, and complete all or some of the walkthroughs in the module together at that stage, like an end of module or even end of course lab.</p> 

<h2>Prerequisites</h2>
<p>An active Azure subscription is required. If you do not have an Azure subscription, create a free Azure account before you begin.</p>

<h2>Steps:</h2>

<p>1. Access Azure Cloud Shell go to the location https://shell.azure.com and sign in with your Azure user login credentials. You can also run Azure Cloud Shell from within Azure Portal by using the Cloud Shell icon.</p> 
<p>2. If prompted, choose a Bash or PowerShell environment. This walkthrough uses PowerShell.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Install IIs/01.jpg"/>
<p>3. First time Azure Cloud Shell users must create and configure Cloud Drive storage, to allow Azure Cloud Shell files to persist. To create and configure storage, select Show advanced settings. If you have created and configured storage already, go to Step5.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Install IIs/02.jpg"/>
<p>4.Provide the following details to create and configure storage.</p> 
	<p>•Subscription: Choose your subscription.</p>   
	<p>•Cloud Shell region: Select the location closest to you. For example, North Europe.</p>  
	<p>•Resource group: Choose Create new, then provide a unique name for your new resource group.</p>
	<p>•Storage account: Select Create new, and provide a unique name for your storage account.</p>   
	<p>•File share: Choose Create new, then enter a unique file share name.</p> 
	<p>•Select the Create storage button. Select the Create storage button.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Install IIs/03.jpg"/>
<p>Wait for the storage setup to complete. When the storage setup is complete, the Welcome to Azure Cloud Shell message is shown in the terminal window.</p> 
<p>5. At the Azure Cloud Shell prompt, set a VM administrator username and password with the Get-Credential command. The credentials are assigned to the variable $cred. The variable is recalled when the new VM is created in the next Step 6.</p>
<p>$cred = Get-Credential When prompted, enter a username and password for the VM administrator. For example,</p>  
	<p>•User: myVMAdmin</p>   
	<p>•Password: pa$$W0rd101</p> 
<p>6. Create a VM with the New-AzVM command. The following example creates a VM named myVM in the North Europe location. If they do not exist, the resource group myResourceGroup and supporting network resources are created in Azure. To allow web traffic, the following command also opens port 80. Change these to more suitable settings, if you prefer.</p>	   
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Install IIs/04.jpg"/>
<p>Note: Ensure you are signed into your Azure subscription. If you have multiple subscriptions, you can get a list of your subscriptions using the command GetAzSubscription. Specify which subscription to use with the command SelectAzSubscription -Subscription "<Name of your subscription>". Substitute the actual name of the subscription you want to use for <Name of your subscription>.</p>  
	<p>New-AzVm `</p>    
	<p>-ResourceGroupName "myResourceGroup" `</p>   
	<p>-Name "myVM" `</p>  
	<p>-Location "North Europe" `</p>  
	<p>-VirtualNetworkName "myVnet" `</p>  
	<p>-SubnetName "mySubnet" `</p>  
	<p>-SecurityGroupName "myNetworkSecurityGroup" `</p>  
	<p>-PublicIpAddressName "myPublicIpAddress" `</p>  
	<p>-OpenPorts 80 `</p>  
	<p>-Credential $cred</p>
<p>When the newly created resources and VM are ready, details about the resources and VM will be displayed in the Azure Cloud Shell window. Wait for the resources and VM to be created.</p> 	
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Install IIs/05.jpg"/>
<p>Connect to the Virtual Machines under Virtual Machine and go to powershell.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Install IIs/06.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Install IIs/07.jpg"/>

<p>Give the below command to install IIS using Powershell.</p>
<p>Add-WindowsFeature –Name “Web-Server”</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Install IIs/08.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Install IIs/09.jpg"/>

	
	
	
 
