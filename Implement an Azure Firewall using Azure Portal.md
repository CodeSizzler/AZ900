<h1>Implement an Azure Firewall using Azure Portal</h1>
<h2>Use Case</h2>
<p>From a network architecture perspective, we will create a single Virtual Network (VNET) which will contain three subnets. The three subnets will be.</p>
<p>•AzureFirewallSubnet: Contains Azure Firewall and all workload server traffic will be routed through Azure Firewall.</p> 
<p>•Workload-SN: Contains the Workload server i.e. a server where a production application would run. We create a default route so that this subnet's network traffic is configured to go through the firewall. The workload server will not have a publicly accessible connection available to it and will only be accessible via a Jump server(Jump box). We will configure Azure Firewall to allow the workload server to access DNS servers over port 53 to allow it access web sites on the internet.</p>  
<p>•Jump-SN: Contains a Jump server which has a public IP address that you can connect to using Remote Desktop. From there, you can then connect to (using another Remote Desktop) the workload server.</p> 	

<h2>Prerequisites</h2>
<p>You require need an Azure subscription to perform these steps. If you don't have one you can create one by following the steps outlined on the Create your Azure free account today webpage.</p>

<h2>Steps:</h2>

<h2>Create Resource group:</h2>
<p>1. Sign in to the Azure portal at https://portal.azure.com</p> 
<p>2. On Azure portal home page, click Resource groups > Add and use the following details and click Review and Create and then Create.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/01.png"/>
<p>•Subscription: < select your own subscription > </p>
<p>•Resource group: az900-rg </p>
<p>•Region: < select a Datacenter location nearest to you. Note: All subsequent resources that you create must be in the same location. ></p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/02.jpg"/>
<p>Click on create button.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/03.jpg"/>

<h2>Create a VNET:</h2>
<p>1. From the Azure portal home page, click All services > Networking > Virtual networks.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/04.jpg"/>
<p>2. Click Add and use the following details, leaving any other values as their default a click Create when finished.</p>
<p>•Name: Test-FW-VN</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/05.jpg"/>
<p>•Address space: 10.0.0.0/16</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/06.jpg"/>
<p>•Subscription : < select your subscription ></p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/07.jpg"/>
<p>•Resource group: < select resource group created earlier az900-rg ></p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/08.jpg"/>
<p>•Location: < select the same location that you used previously ></p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/09.jpg"/>
<p>•Subnet></p> 
<p>•Name: AzureFirewallSubnet (The firewall will be in this subnet, and the subnet name must be AzureFirewallSubnet)</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/10.jpg"/>

<h2>Create additional subnets:</h2>
<p>Next we will create some additional subnets, into which we will subsequently place two virtual machines.</p>
<p>1. On the Azure portal home page, click Resource groups > az900-rg.</p> 
<p>2. Click the Test-FW-VN virtual network.</p> 
<p>3. Click Subnets > + Subnet and use the following details, leaving the remaining items at their default values and click OK when completed.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/11.jpg"/>
<p>•Name: Workload-SN</p>
<p>•Address range: 10.0.2.0/24</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/12.jpg"/>
<p>4. Create another subnet by repeating steps 1-3 above, using the values.</p>
<p>•Name: Jump-SN</p> 
<p>•Address range: 10.0.3.0/24</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/13.jpg"/>

<h2>Create a virtual machine in each subnet:</h2>
<p>Now we will create two virtual machines and place them in the two additional subnets created in the previous section, one for the Jump-SN subnet, and one for the Workload-SN subnet.</p>  
<p>1. On the Azure portal, click Create a resource.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/14.jpg"/>
<p>2. Click Compute and then select Windows Server 2016 Datacenter in the Featured list.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/15.jpg"/>
<p>3. Enter these values for the virtual machine, accepting the default values for items not listed below. When finished click Review + Create, then click Create.</p> 
<p>•Basic:</p>
<p>•Subscription: < select your subscription ></p> 
<p>•Resource group: Test-FW-RG < the resource group you created earlier ></p> 
<p>•Virtual machine name: Srv-Jump</p> 
<p>•Region: < The region you selected earlier ></p> 
<p>•Size – Standard DS1 V2</p> 
<p>•Username: demouser</p> 
<p>•Password: demo@pass123</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/16.jpg"/>
<p>•Public inbound ports: RDP (3389)</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/17.jpg"/>
<p>•Disks:</p>  
<p>•Disk options – OS disk type: Premium SSD</p>  
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/18.jpg"/>
<p>•Networking:</p> 
<p>•Virtual Network: Test-FW-VN</p> 
<p>•Subnet: Jump-SN</p> 
<p>•Public IP: click Create new then type Srv-Jump-PIP for the public IP address name and click OK.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/19.jpg"/>
<p>•Management:</p> 
<p>•Boot diagnostics: Off</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/20.jpg"/>
<p>•Click on create button.</p>
<p>4. While the virtual machine is being created, repeat steps 1-3 above to create another virtual machine with the following settings:</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/21.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/22.jpg"/>
<p>•Basics:</p> 
<p>•Subscription: < select your subscription ></p> 
<p>•Resource group: az900-rg< the resource group you created earlier ></p> 
<p>•Virtual machine name: Srv-Work</p> 
<p>•Region: < The region you selected earlier ></p> 
<p>•Username: demouser</p> 
<p>•Password: demo@pass123</p> 
<p>•Public inbound ports: None</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/23.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/24.jpg"/>
<p>•Disks:</p>  
<p>•Disk options – OS disk type: Premium SSD</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/25.jpg"/>
<p>•Networking:</p> 
<p>•Virtual Network: Test-FW-VN</p>  
<p>•Subnet: Workload-SN</p>  
<p>•Public IP: None</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/26.jpg"/>
<p>•Management:</p>   
<p>•Boot diagnostics: Off</p>  
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/27.jpg"/>
<p>•Click on create button.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/28.jpg"/>

<h2>Create a virtual machine in each subnet:</h2>
<p>1. From the portal home page, click Create a resource and in the New pane type Firewall, then click Create.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/29.jpg"/>
<p>2. Click Networking and in the Featured section click See all > Firewall > Create.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/30.jpg"/>
<p>•Subscription: < your Azure subscription ></p>
<p>•Resource group: az900-rg < the resource group you created earlier > • Name: Test-FW01</p> 
<p>•Region: < Select the same location that you used previously ></p> 
<p>•Choose a virtual network: Test-FW-VN < the VNET you created earlier ></p> 
<p>•Public IP address: < select Create new radio button ></p> 
<p>•Public IP address: < accept the default value ></p>  
<p>•Public IP address SKU: Standard</p>  
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/31.jpg"/>
<p>•Click on create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/32.jpg"/>
<p>3. After deployment completes, go to the Test-FW-RG resource group, and click the Test-FW01 firewall.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/33.jpg"/>

<h2>Create a default route:</h2>
<p>1. From the Azure portal home page, click All services. Under Networking, click Route tables.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/34.PNG"/>
<p>2. In the Route tables pane click +  Add and enter the following details and when finished click Create.</h2>
<p>•Name: Firewall-route</p> 
<p>•Subscription: < select your subscription ></p> 
<p>•Resource group: az900-rg< the resource group you created earlier ></p>
<p>•Location: < select the same location that you used previously ></p> 
<p>•Click on create button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/35.jpg"/>
<p>3. When it is finished click Refresh, and then click the Firewall-route route table.</p>
<p>4. Click Subnets > + Associate.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/36.jpg"/>
<p>5. Click Virtual network > Test-FW-VN.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/37.jpg"/>
<p>6. For Subnet, click Workload-SN. Make sure that you select only the WorkloadSN subnet for this route, otherwise your firewall won't work correctly.</p> 
<p>7. Click OK.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/38.jpg"/>
<p>8. Click Routes > + Add and enter the following details and click OK when finished.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/39.jpg"/>
<p>•Route name: FW-DG</p> 
<p>•Address prefix: 0.0.0.0/0</p> 
<p>•Next hop type: Virtual appliance. (Azure Firewall is actually a managed service, but virtual appliance works in this situation.)</p> 
<p>•Next hop address < enter the private IP address for the firewall that you noted previously ></p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/40.jpg"/>

<h2>Configure an application rule:</h2>
<p>1. Open the az900-rg, and click the Test-FW01 firewall.\</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/41.jpg"/>
<p>2. On the Test-FW01 page, under Settings, click Rules.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/42.jpg"/>
<p>3. Click the Application rule collection tab.</p>  
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/43.jpg"/>
<p>4. Click + Add application rule collection and enter the following values, then click Add when finished.</p> 
<p>•Name: App-Coll01</p> 
<p>•Priority: 200 • Action: Allow</p> 
<p>•Rules:</p> 
<p>•Name: AllowWebsite • Source Address:10.0.2.0/24.</p> 
<p>•Protocol:Port: http, https.</p> 
<p>•Target FQDNS: www.microsoft.com (You can specify part of all or a URL, including wild characters, or just a single wild character to indicate all internet sites )</p>  
<p>Note: Azure Firewall includes a built-in rule collection for infrastructure FQDNs that are allowed by default. These FQDNs are specific for the platform and can't be used for other purposes. For more information, see Infrastructure FQDNs. You can also use FQDN tags to represent a group of fully qualified domain names (FQDNs) associated with well known Microsoft services, such as Windows Update, Azure Backup etc.</P> 

<h2>Configure a network rule:</h2>
<p>1. Open the az900-rg, and click the Test-FW01 firewall.</p>
<p>2. On the Test-FW01 page, under Settings, click Rules>Click the Network rule collection tab.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/44.jpg"/>
<p>3. Click + Add network rule collection and enter the following details, when finished click Add.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/45.jpg"/>
<p>•Name: Net-Coll01</p> 
<p>•Priority: 200 • Action: Allow</p> 
<p>•Rules:</p> 
<p>•IP Addresses:</p> 
<p>•Name: AllowDNS</p> 
<p>•Protocol: UDP</p> 
<p>•Source Addresses: 10.0.2.0/24</p> 
<p>•Destination Addresses: 209.244.0.3,209.244.0.4</p> 
<p>•Destination Port:: 53</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/46.jpg"/>

<h2>Change the primary and secondary DNS address for the Srv-Work network interface:</h2>
<p>1. From the Azure portal, open the az900-rg resource group.</p>
<p>2. Click the network interface for the Srv-Work virtual machine, it should be named something like Srv-Work-xyz.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/47.jpg"/>
<p>3. Under Settings, click DNS servers.> click Custom and add the following details and click Save when finished.</p> 
<p>•Box 1 - Add DNS Server: 209.244.0.3</p>  
<p>•Box 2 - Add DNS Server: 209.244.0.4</p>  
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/48.JPG"/>
<p>Note: Updating the DNS records for the Network interface will automatically restart the virtual machine to which it is attached, you should see a message indicating such. Also the IP Addresses we are adding here are pre-existing publicly accessible DNS Server addresses. When our virtual machine looks for an external address it will refer to these DNS servers for the address details.</p> 
<p>4. Go to the Srv-Work virtual machine and ensure it has a status of running, if it is de-allocated click Start, or if it has not re-started click Restart.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/49.JPG"/>
 
<h2>Test the firewall:</h2>
<p>1. From the Azure portal, review the network settings for the Srv-Work virtual machine and note the private IP address.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/50.jpg"/>
<p>2. In the Azure Portal go to the Srv-Jump virtual machine and click Connect, followed by Download RDP File to open an RDP session to the SRVJump virtual machine, using the credentials you specified earlier when creating the VM.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/51.jpg"/>
<p>3. From within the Srv-Jump virtual machine open a remote desktop connection to the Srv-Work private IP address that you noted earlier.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/52.jpg"/>
<p>4. Once logged into the SRV-Jump virtual machine, allow Server Manager to open, which it will do after log in automatically, then go to Local server and turn off IE Enhanced Security Configuration.</p> 
<p>Note: In production environments you would not do this, this is to allow use access the workload server a bit more easily in this test scenario and reduce and prevent pop-ups. In a production you may use a workload server with no GUI environment present.</p>
<p>5. Open Internet Explorer and browse to https://www.microsoft.com</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-004/53.jpg"/>
<p>6. Click OK > Close on the security alerts that may pop-up.</p> 
