<h1>Use Tags with Azure resources</h1>
<h2>Use Case</h2>
<p>In this walkthrough task we will create Azure resources to allow us to create a lock against them, then you will add a Delete Lock to prevent deletion of a resource group. You will then verify that deletion of the resource group is indeed blocked, and also that any resources within the resource group are also blocked from being deleted by the parent Lock. You will then remove the lock and verify it has been removed by deleting the resource group.</p>

<h2>Prerequisites</h2>
<p>You require need an Azure subscription to perform these steps. If you don't have one you can create one by following the steps outlined on the Create your Azure free account today webpage.</p>

<h2>Steps:</h2>
<h2>Create Azure resources to allow us to apply Tags to them:</h2>
<p>1. Sign into the Azure Portal and click on the Cloud Shell icon in the top right hand corner.</p>
<p>2. The Cloud Shell is launched in the bottom of the browser window.</p>
<p>3. Create a resource group into which we will place our resources by running the following Azure CLI command. You can copy and paste the command from the below directly into the Cloud Shell console, then press Enter to run the command. This command will run fine in either powershell or bash console.</p>
	<p>```cli</p>
	<p>az group create `</p>
	<p>--name tagrg `</p>
	<p>--location westeurope</p>
	<p>```</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/01.jpg"/>
<p>4. Run the below Azure CLI command to create a virtual machine. Again, you can copy and paste the command from below directly into the Cloud Shell console and press Enter to run it.</p>
	<p>```cli</p>
	<p>az vm create `</p>
	<p>--name vmtag1 `</p>
	<p>--resource-group tagrg `</p>
	<p>--image Win2019Datacenter `</p>
	<p>--location westeurope ` --admin-username</p>
	<p>azureuser `</p>
	<p>--admin-password Password0134!</p>
	<p>```</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/02.jpg"/>
<p>Note: The command will take 2 to 3 minutes to complete. The command will create a virtual machine and various resources associated with it such as storage, networking and security resources. You can close the Azure Cloud Shell once it is complete.</p>

<h2>View the tags for a resource or a resource group:</h2>
<p>In the Azure Portal, open the resource group we just created i.e. tagrg, on the Overview pane alongside Tags, note there are no values listed and a message reads Click here to add tags. This indicates no tags have been applied to the resource group or resources.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/03.jpg"/>

<h2>Add tags:</h2>
<p>1. Still in the Tagrg resource group click on the Click here to add tags link and in the subsequent Tags pane enter the values below, click Save and then Close. 1.	Still in the Tagrg resource group click on the Click here to add tags link and in the subsequent Tags pane enter the values below, click Save and then Close.</p>
	<p>•Name: Environment</p>
	<p>•Value: Production</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/04.jpg"/>
<p>2. In the Tagrg resource group Overview section, the Tags section now has the tag Name:Value pair of Environment: Production present.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/05.jpg"/>
<p>3. Open up the virtual machine resource and in the Overview pane note that the tags assigned to the resource group are not present in the resource beneath it.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/06.jpg"/>

<h2>Bulk assign tags to resources:</h2>
<p>1. Return to the resource group tagrg check the checkboxes beside all resources listed under the resource group by clicking on the NAME checkbox then click the Assign Tags button.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/07.jpg"/>
<p>2. In the Tags pane enter the values below, click Save and then Close.</p>
	<p>•Name: Department</p>
	<p>•Value: IT and</p>
	<p>•Name: Environment</p>
	<p>•Value: Production</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/08.jpg"/>
<p>3. Open up the virtual machine resource and note the presence of the two tags Department:IT and Environment:Production:</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/09.JPG"/>
<p>4. In the virtual machine Overview pane note that the values for Tags has returned of the link stating Click here to add tags., indicating there are no tags now present.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/10.jpg"/>
<p>5. In the Tags pane a number of tags are listed. To view all resources with a specific tag, click the Name:Value pair that you want to view resources for i.e. click Department:IT</p>
<p>•After clicking on the Name Value pair Department:IT, in the resultant Department:IT pane, all resources with this *Name:Value* pair are listed.</p>
<p>Note: For quick access, you could pin the Tags service view to the dashboard.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/11.JPG"/>

<h2>Delete tags:</h2>
<p>In the resource group you created earlier i.e. tagrg, open the virtual machine and click on the Tags section. In the resultant Tags pane we have an option to Delete All tags, or click the *dustbin icon* beside individual *Name:Value* pairs, to delete individual tags. Click Delete All then click Save and Close.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-007/12.jpg"/>
