<h1>Manage Azure resources using Locks</h1>
<h2>Use Case</h2>
<p>In this walkthrough task we will create Azure resources to allow us to create a lock against them, then you will add a Delete Lock to prevent deletion of a resource group. You will then verify that deletion of the resource group is indeed blocked, and also that any resources within the resource group are also blocked from being deleted by the parent Lock. You will then remove the lock and verify it has been removed by deleting the resource group.</p> 
 
<h2>Prerequisites</h2>
<p>You require need an Azure subscription to perform these steps. If you don't have one you can create one by following the steps outlined on the Create your Azure free account today webpage.</p>

<h2>Steps:</h2>
<h2>Create Azure resources to allow us to create a lock against them:</h2> 
<p>1. Sign into the Azure Portal and click on the Cloud Shell icon in the top right hand corner.</p>
<p>2. The Cloud Shell is launched in the bottom of the browser window.</p> 
<p>3. Create a resource group into which we will place our resources by running the following Azure CLI command. You can copy and paste the command from the below directly into the Cloud Shell console, then press Enter to run the command. This command will run fine in either powershell *or* bash console.</p> 
	<p>•```cli</p> 
	<p>•az group create `</p> 
	<p>•--name lockscrg `</p> 
	<p>•--location westeurope</p> 
	<p>•```</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/01.jpg"/>
<p>4. Run the below Azure CLI command to create a virtual machine. Again, you can copy and paste the command from below directly into the Cloud Shell console and press Enter to run it.</p>
	<p>•```cli</p> 
	<p>•az vm create `</p> 
	<p>•--name vmlocks1 `</p> 
	<p>•--resource-group lockscrg `</p> 
	<p>•--image Win2019Datacenter `</p> 
	<p>•--location westeurope `</p> 
	<p>•--admin-username demouser `</p> 
	<p>•--admin-password demo@pass123</p> 
	<p>•```</p>
<p>Note: The command will take 2 to 3 minutes to complete. The command will create a virtual machine and various resources associated with it such as storage, networking and security resources. You can close the Azure Cloud Shell once it is complete.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/02.jpg"/>

<h2>Add a Lock to prevent deletion of a resource:</h2>
<p>1. In the Azure Portal go to the resource group you just created i.e. lockscrg, then go to Settings > Locks.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/03.jpg"/>
<p>2. To add a lock, select Add and then enter the following values, clicking OK when finished.</p> 
	<p>•Lock name: resource group lock</p>  
	<p>•Lock Type: Delete ( the other lock type available to us here is *Readonly*)</p>  
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/04.jpg"/>
<p>3. Now let us try delete the resource group we just created the Delete lock for, by going to the resource group i.e. lockscrg, then the clicking on Overview and selecting Delete resource group.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/05.jpg"/>
<p>4. In the Are you sure you want to delete "lockscrg"? blade, type the name of the resource group i.e.lockscrg and click the Delete button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/06.jpg"/>
<p>5. You receive an error message stating the resource group is locked and can't be deleted.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/07.jpg"/>
<p>6. Within the same resource group open the virtual machine i.e.vmlocks1, go to the Overview pane and select Delete.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/08.jpg"/>
<p>7. In the resultant Delete virtual machine pane, select Yes to confirm your wish to delete the virtual machine.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/09.jpg"/>
<p>8. You receive an error message stating.</p>
<p>Note: Although we did not create a lock specifically for the virtual machine, we did create a lock at the resource group level, which contains the virtual machine resource. As such this *parent* level lock prevents us from deleting the virtual machine, the virtual machine resource inherits the lock from the parent.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/10.jpg"/>

<h2>Remove a lock:</h2>
<p>1. Return to the resource group and go to Settings > Locks.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/11.jpg"/>
<p>2. Click the ellipsis at the end of the Delete lock that you created earlier and select Delete on the resultant menu.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/12.jpg"/>
<p>3. In the resource group Overview pane, click on Delete resource group an din the resultant Are you sure you want to delete "lockscrg"? pane, type in the name of the resource group and click Delete to delete the resource group.</p> 
<p>Note: The resource group and all resources within it are successfully deleted now, because the delete lock has been removed.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/13.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Azure/14.jpg"/>









