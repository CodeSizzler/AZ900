<h1>Manage access to Azure resources using RBAC</h1>
<h2>Use Case</h2>
<p>In this walkthrough task we will create some Azure resources that we can manage using Role-Based-Access-Control (RBAC), then we will view access control at subscription level, then view roles and permissions at resource group level for azure resources, and view individual user and all role assignments. You will then add a new role assignment for the virtual machine contributor role and then remove a role assignment for the resources you deployed.</p>

<h2>Prerequisites</h2>
<p>You require need an Azure subscription to perform these steps. If you don't have one you can create one by following the steps outlined on the Create your Azure free account today webpage.</p>

<h2>Steps:</h2>

<h2>Create Azure resources to manage:</h2>
<p>1. Sign into the Azure Portal and click on the Cloud Shell icon in the top right hand corner.</p> 
<p>2. The Cloud Shell is launched in the bottom of the browser window.</p> 
<p>3. Create a resource group into which we will place our resources by running the following Azure CLI command. You can copy and paste the command from the below directly into the Cloud Shell console, then press Enter to run the command. This command will run fine in either powershell *or* bash console.</p> 
	<p>```cli</p> 
	<p>az group create `</p> 
	<p>--name rbacrg `</p> 
	<p>--location westeurope</p> 
	<p>```</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Access/01.png"/>
<p>4. Run the below Azure CLI command to create a virtual machine. Again, you can copy and paste the command from below directly into the Cloud Shell console and press Enter to run it.</p>
	<p> ```cli</p>  
	
	<p>az vm create `</p>  
	<p>--name vmrbac1 `</p>  
	<p>--resource-group rbacrg `</p>  
	<p>--image Win2019Datacenter `</p>  
	<p>--location westeurope ` --admin-username</p>  
	<p>azureuser `</p>  
	<p>--admin-password Password0134!</p>  
	<p>```</p>  
<p>Note: The command will take 2 to 3 minutes to complete. The command will create a virtual machine and various resources associated with it such as storage, networking and security resources. You can close the Azure Cloud Shell once it is complete.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Access/02.png"/>

<h2>View access control at subscription level:</h2>
<p>The next thing we need to do, in the context of access control, is to decide where to open the Access control (IAM) blade, through which we configure Role-BasedAccess-Control (RBAC), and that depends on what resources you want to manage access for. i.e. do you want to manage access for everything in a management group, everything in a subscription, everything in a resource group, or a single resource? The Access control (IAM) blade is available at all of these levels and provides the same functionality in each. We will firstly have a look at the Access control (IAM) options for a subscription.</p> 
<p>1. In the Azure portal, click All services and the Subscriptions, double click on a subscription from the subscriptions listed and then click on Access control (IAM)the scope.</p>  
<p>Note: The screenshot above shows an example of the Access control (IAM) blade for a subscription. If you make any access control changes here, they would apply to the entire subscription. Likewise, any changes made at management group, resource group or individual resource level apply just at those levels.</p>  
 
<h2>View roles and permissions:</h2> 
<p>A role definition is a collection of permissions that you use for role assignments. Azure has over 70 built-in roles for Azure resources. Follow these steps to view the available roles and permissions for the resources we deployed earlier.</p> 
<p>1. Go to Resource groups and choose rbacrg i.e. the resource group you created earlier. Within the rbacrg resource group, click on Access control (IAM) and then select the Roles tab to see a list of all the built-in and custom roles.</p> 
<p>Note: You can see the number of users and groups that are assigned to each role at the current scope.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Access/03.jpg"/>
<p>2. Click on the Owner role to see who has been assigned this role and also view the permissions for the role.</p> 
<p>Note: As per the screenshot, there are two users listed who are assigned the Owner role. Your list of users will be different.</p>

<h2>View individual user and all role assignments for a resource:</h2>
<p>When managing access, you want to know who has access, what are their permissions, and at what scope. To list access for a user, group, service principal, or managed identity, you view their role assignments.</p>
<p>1. In the resource group you created earlier i.e. rbacrg go to Access control (IAM) and select the Check Access tab.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Access/04.JPG"/>
<p>2. In the Find boxes enter the below values, to search the directory for for display    names, email addresses, or object identifiers. The matching results are displayed below the Find boxes.</p> 
	<p>•Azure AD user, group, or service principal</p> 
	<p>•< your own user name i.e. in this case we used eamonn Kelly</p>  
<p>Note:Your results will be different and related to your own user account.</p>
<p>3. Click the matching result to open the < name > assignments - scope pane. On this pane, you can see the roles assigned to the selected user and the scope. If there are any deny assignments at this scope or inherited to this scope, they will be listed. We can see the user has the role of Owner assigned and can manage everything.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Access/05.JPG"/>
<p>4. Still on the resource group Access control (IAM) pane, click the Role assignments tab to view all the role assignments at this scope. On the Role assignments tab, you can see who has access at this scope.</p>  
<p>Note: Some of roles present, are listed as (Inherited). This means they are assigned from another scope. Access, in general, is either assigned specifically to this resource, or inherited from an assignment to the parent scope. Your values will be different to those displayed here.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Access/06.jpg"/>

<h2>Add a role assignment:</h2>
<p>In RBAC, to grant access, you assign a Role to a user, group, service principal, or managed identity. We will assign the role to a user in the following steps.</p> 
<p>1. Open the resource group Access control (IAM) and click the Role assignments tab, then click Add and choose Add role assignment to open the Add role assignment pane.</p>  
<p>Note: If you don't have permissions to assign roles, the Add role assignment option will be disabled.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Access/07.JPG"/>
<p>2. In the Add role assignment pane fill in the following values, then click Save to assign the role.</p>
	<p>•Role: select a Role from the drop down list i.e. *Virtual Machine Contributor*</p>
	<p>•Assign access to: Azure AD user, group, or service principal</p>
	<p>•Select: < type your own user name, and your user name should appear in the list, then click on a user name to select it ></p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-005/AZ-900 1/Manage Access/08.jpg"/>
<p>3. The user is now assigned the specified role at the selected scope.</p> 	
	
	


 
