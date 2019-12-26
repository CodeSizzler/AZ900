<h1>Secure Network traffic using NSGs and ASGs.</h1>
<h2>Use Case</h2>
<p>In this walkthrough task we will create a virtual network and subnet, we will create two application security groups, one for management servers and one for web servers, then create a Network Security group (NSG) and associate that NSG to the subnet. We will then create two inbound network security rules, *allow-rdp-all* and *allow-web-all* traffic.</p>
<p>We will then create two virtual machines, one to represent a management server, and one to represent a web server, associate those virtual machines with their respective application security groups, and then with the network security group (NSG). We will then test the network security rules we have created and applied.</p>

<h2>Prerequisites</h2>
<p>You require need an Azure subscription to perform these steps. If you don't have one you can create one by following the steps outlined on the Create your Azure free account today webpage.</p>

<h2>Steps:</h2>
<h2>Create a virtual network:</h2>
<p>1. Sign into the Azure Portal.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/01.jpg"/>
<p>2. Select + Create a resource on the upper, left corner of the Azure portal, then select Networking, and then select Virtual network.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/02.jpg"/>
<p>3. Enter, or select, the following information, accept the defaults for the remaining settings, and then select Create:</p>
	<p>•Name: VNET1</p>
	<p>•Address space: 10.0.0.0/16</p>
	<p>•Subscription : < select your subscription ></p>
	<p>•Resource group: < Select *Create new* and enter netsecrg. ></p>
	<p>•Location: (US) East US (or a Datacenter location near you)</p>
	<p>•Subnet:</p>
	<p>•Name: subnet1</p>
	<p>•Address range: 10.0.0.0/24</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/03.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/04.jpg"/>

<h2>Create two application security groups:</h2>
<p>1. Select +Create a resource on the upper, left corner of the Azure portal.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/05.jpg"/>
<p>2. In the Search the Marketplace box, enter Application security group. When Application security group appears in the search results, select it, select Application security group again under everything and then select Create.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/06.jpg"/>
<p>3. Enter the following values then click Review and Create followed by Create.</p>
	<p>•Subscription : < select your subscription > </p>
	<p>•Resource group: < *Select existing...* and then select *netsecrg* which you created earlier. > </p>
	<p>•Name: asgwebservers </p>
	<p>•Region: (US) East US </p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/07.JPG"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/08.jpg"/>
<p>4. Complete steps 1 to 3 again to create another Application security group, specifying the following values:</p>
	<p>•Subscription : < select your subscription ></p>
	<p>•Resource group: < *Select existing...* and then select *netsecrg* which you created earlier. ></p>
	<p>•Name: asgmgmtservers</p>
	<p>•Region: (US) East US</p>
<p>5. Select +Create a resource on the upper, left corner of the Azure portal.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/09.jpg"/>
<p>6. In the Search the Marketplace box, enter Application security group. When Application security group appears in the search results, select it, select Application security group again under everything and then select Create.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/10.jpg"/>
<p>7. Enter the following values then click Review and Create followed by Create.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/11.jpg"/>
	<p>•Subscription : < select your subscription ></p>
	<p>•Resource group: < *Select existing...* and then select *netsecrg* which you created earlier. ></p>
	<p>•Name: asgmgmtservers</p>
	<p>•Region: (US) East US</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/12.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/13.jpg"/>

<h2>Create a network security group:</h2>
<p>1. Select + Create a resource on the upper, left corner of the Azure portal, then select Networking, and then select Network security group.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/14.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/15.JPG"/>
<p>2. Enter, or select, the following information, and then select Create:</p>
	<p>•Name: nsg1</p>
	<p>•Subscription : < select your subscription ></p>
	<p>•Resource group: < *Select existing...* and then select netsecrg which you created earlier. ></p>
	<p>•Location: (US) East US</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/16.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/17.jpg"/>

<h2>Associate the network security group to a subnet:</h2>
<p>1. Open the Network security group you just created, nsg1, Under SETTINGS, select Subnets and then select + Associate.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/18.jpg"/>
<p>2. Open the Network security group you just created, nsg1, Under SETTINGS, select Subnets and then select + Associate.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/19.jpg"/>

<h2>Create security rules:</h2>
<p>1. Still in the Network Security group, Under SETTINGS, select Inbound security rules and then select + Add.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/20.jpg"/>
<p>2. Create a security rule that allows ports 80 and 443 to the AsgWebServers application security group. Under Add inbound security rule, enter, or select the following values, accept the remaining defaults, and then select Add when finished.</p>
	<p>•	Source: Any</p>
	<p>•	Source port ranges: *</p>
	<p>•	Destination: Application security group</p>
	<p>•	Destination application security group: asgwebservers</p>
  	<p>•	Destination port ranges: 80,443</p>
	<p>•	Protocol: TCP</p>
	<p>•	Action: Allow</p>
	<p>•	Priority: default</p>
	<p>•	Name: Allow-Web-All</p>
<p>This allows us to connect to the web server from the internet over ports 80 and 443 only.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/21.jpg"/>
<p>3. Create another inbound security rule by repeating steps 1 and 2 again, using the following values:</p>
	<p>•	Source: Any</p>
	<p>•	Source port ranges: *</p>
	<p>•	Destination: Application security group</p>
	<p>•	Destination application security group: asgmgmtservers</p>
	<p>•	Destination port ranges: 3389</p>
	<p>•	Protocol: TCP</p>
	<p>•	Priotity: 110</p>
	<p>•	Name: Allow-RDP-All</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/22.jpg"/>
<p>Note:The port 3339, the rdp port, is exposed to the internet for the VM that is assigned to the asgmgmtservers application security group. For production environments, instead of exposing port 3389 to the internet, it's recommended that you connect to Azure resources that you want to manage using a VPN or private network connection. also, we designated the value Any for source to indicate access from the internet.</p>
<p>4. Review the rules you created. Your list should look like the list in the following picture:</p>

<h2>Create virtual machines:</h2>
<p>1. In the Azure Portal, click on the Cloud Shell icon in the top right hand corner.</p>
<p>2. The Cloud Shell is launched in the bottom of the browser window.</p>
<p>3. Run the below Azure CLI command to create the first virtual machine, this command will run fine in either powershell *or* bash console. You can copy and paste the command from below directly into the Cloud Shell console and press Enter to run it.</p>
	<p>```cli</p>
	<p>az vm create `</p>
	<p>--name vmmgmt1 `</p>
	<p>--resource-group netsecrg `</p>
	<p>--image Win2019Datacenter `</p>
	<p>--location eastus `</p>
	<p>--vnet-name VNET1 `</p>
	<p>--subnet subnet1 `</p>
	<p>--nsg nsg1 `</p>
	<p>--asg asgmgmtservers ` --admin-username</p>
	<p>azureuser `</p>
	<p>--admin-password Password0134!</p>
	<p>```</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/23.jpg"/>
<p>Note: The command will take two to three minutes to complete and should run successfully. Do not continue to the next step until the VM is deployed.</p>
<p>4. Create the second virtual machine by running the following command in the same cloud shell console in the browser window.</p>
	<p>```cli</p>
	<p>az vm create `</p>
	<p>--name vmweb1 `</p>
	<p>--resource-group netsecrg `</p>
	<p>--image Win2019Datacenter `</p>
	<p>--location eastus `</p>
	<p>--vnet-name VNET1 `</p>
	<p>--subnet subnet1 `</p>
	<p>--nsg nsg1 `</p>
	<p>--asg asgwebservers ` --admin-username</p>
	<p>azureuser `</p>
	<p>--admin-password Password0134!</p>
	<p>```</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/24.jpg"/>
<p>Note:• Items to note from the deployment.</p>
		<p>• We created a network interface for each VM, and attached the network interface to the VM.</p>
		<p>• Both network interfaces are in Virtual network VNET1 and its subnet subnet1.</p>
		<p>• subnet1 is part of the Network Security Group, nsg1, so as such the nsg1 security rules are applied to the two virtual machines.</p>
		<p>• vmmgmt1 has been associated with the application security group asgmgmtservers</p>
		<p>• - vmweb1 has been associated with the application security group asgwebservers*</p>

<h2>Test traffic filters:</h2>
<p>1. In the Azure Portal, go to your resource group, i.e. netsecrg, open the vmmgmt1 virtual machine and connect to it by clicking on the Connect button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/25.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/26.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/27.jpg"/>
<p>2. In the Connect to virtual machine blade select Download RDP File and click to open the rdp file when prompted to do so.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/28.jpg"/>
<p>3. In the Remote Desktop Connection dialogue select Connect.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/29.jpg"/>
<p>4. In the Windows Security > Enter your credentials dialogue select More Choices.</p>
<p>5. Select use a different account and enter the user name and password you specified when creating the VM, as below, then click OK.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/30.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/31.jpg"/>
<p>Note:•You may receive a certificate warning during the sign-in process. If you receive the warning, select Yes or Continue, to proceed with the connection.The connection succeeds, because port 3389 is allowed inbound connections from the internet to the asgmgmtservers application security group, i.e. the vmmgmt1 virtual machine is in the VNET1 virtual network and the subnet subnet1 which has those security rules associated with it as defined by the Network Security group nsg1.</p>
<p>6. From within the vmmgmt1 virtual machine we will now connect via rdp to the vmweb1 virtual machine. Still within the remote desktop connection to vmmgmt1, go to the start menu, type PowerShell, then locate and launch Powershell, by right clicking it and choosing Run as Administrator.</p>
<p>7. We will now install Internet Information Service (IIS) on the vmweb1 to allow it function as a webserver. Return to the remote desktop connection to vmweb1 virtual machine and open a Powershell prompt by clicking on the start button, typing Powershell, the right clicking it and choosing Run as administrator 12. In the resultant Powershell console prompt, install Microsoft Internet.</p>
<p>Note:•Information Service (IIS) on the vmweb1 virtual machine, by running the following command within the PowerShell session.</p>
	<p>```</p>
	<p>Install-WindowsFeature -name Web-Server -IncludeManagementTools</p>
	<p>```</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/32.jpg"/>
<p>8. The installation should complete successfully</p>
<p>9. Disconnect from the vmweb1 virtual machine, which leaves you in the vmmgmt1 remote desktop connection, then also disconnect from the vmmgmt1 virtual machine.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/33.jpg"/>
<p>10. In the Azure portal open the vmweb1 , go to Overview and note the Public IP address for the virtual machine. The address shown in the following picture is 13.90.244.107, but your address will be different:</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/34.jpg"/>
<p>11. From your local machine access the vmweb1 web server from the internet by opening an internet browser on your computer. You see the IIS welcome screen.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-006/35.jpg"/>
