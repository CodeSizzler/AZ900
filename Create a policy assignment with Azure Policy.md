<h1>Create a policy assignment with Azure Policy</h1>
<h2>Use Case:</h2>
<p>In this walkthrough task we will locate an Azure Policy to restrict deployment of Azure resources to a particular Datacenter, and then assign that allowed location policy to a subscription. We will then verify that creating an Azure resource, such as a virtual machine, outside of the allowed location is blocked. We will finally remove the allowed location policy assignment, to allow us deploy resources again to any Datacenter location using that same subscription.</p>

<h2>Prerequisites:</h2>
<p>You require need an Azure subscription to perform these steps. If you don't have one you can create one by following the steps outlined on the Create your Azure free account today webpage.</p>

<h2>Steps:</h2>

<h2>Create a Policy assignment:</h2>
<p>1. Launch the Azure Policy service in the Azure portal by clicking All services then, Everything, then type Policy in the search box and select Policy </p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/1.jpg"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/2.jpg"/>
<p>Note: Azure Policy is also accessible under the All services > Management + governance section in the portal.</p>
<p>2. Go to Authoring > Definitions and take a moment to have a quick browse through the list of built-in policy definitions that are available for you to use.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/3.jpg"/>
<p>3. Select Assignments on the left side of the Policy page. An assignment is a policy that has been assigned to take place within a specific scope.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/4.jpg"/>
<p>4. Select Assignments on the left side of the Policy page. An assignment is a policy that has been assigned to take place within a specific scope.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/5.jpg"/>
<p>5. Select Assign Policy from the top of the Policy - Assignments page and on the subsequent Assign Policy page, select the Scope selector by clicking the ellipsis and setting the following values, then click Select at the bottom of the Scope page.</p>
<p>•Subscription: < choose your own subscription > </p>
<p>•Resource Group: < accept the default value i.e. leave blank > </p> 
<p>Note: A scope determines what resources or grouping of resources the policy assignment gets enforced on. In our case we could assign this policy to a specific resource group, however we will assign the policy at subscription level. Also, be aware that resources can be excluded based on the Scope. Exclusions are optional.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/6.jpg"/>
<p>6. Select the Policy definition ellipsis button to open the list of available definitions. Azure Policy comes with built-in policy definitions you can use, this is the same list that we saw earlier in the Definitions pane. Many are available, such as the below, but again you can take a quick moment to scroll through and search for ones that may interest you:</p> 
<p>•Require tag and its value</p>
<p>•Append tag and its value</p>
<p>•Require SQL Server version 12.0</p>
<p>In the Available Definitions pane in the Search box type location and click on the Allowed locations definition, then click Select.</p>
<p>Note: This Allowed Locations policy definition will specify a location into which all resources must be deployed. If a different location is chosen deployment will not be allowed. For a partial list of available built-in policies, you can also see them at the https://docs.microsoft.com/en-us/azure/governance/policy/samples/index page.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/7.jpg"/> 
<p>7. In the Assign policy pane, in the PARAMETERS section, click on the arrow at the end of the Allowed locations box and from the subsequent list choose Japan West. Leave all other values as they are and Click Assign.</p>
<p>Note: The Assignment name is automatically populated with the policy name you selected, but you can change it if you wish. You can also add an optional Description and Assigned by will automatically fill based on whoever is logged in. This field is optional, so custom values can be entered. Leave the Create a Managed Identity option unchecked. However, this box must be checked when the policy or initiative includes a policy with the deployIfNotExists effect.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/8.jpg"/> 
<p>8. The Allowed locations policy assignment is now listed on the Policy - Assignments pane and it is now in place and available to enforce at the scope level we specified i.e. at subscription level.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/9.jpg"/>   
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/10.jpg"/>   
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/11.jpg"/>   

<h2>Test Allowed location policy:</h2> 
<p>1. In the Azure Portal, in the FAVORITES list on the left hand side, then click Create virtual machine.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/12.PNG"/>
<p>2. In the Create a virtual machine pane on the Basics tab fill in the fields with the following values, leaving all other values as default, and Click Review + create:</p>
<p>•Subscription: < select your own subscription. Ensure it is the same subscription you assigned the allowed locations policy to earlier> </p>
<p>•Resource group: click Create new and enter a value i.e. vmpolcheckrg</p>
<p>•Virtual machine name: vmpolcheck1</p>
<p>•Region: select any Datacenter location other than the one that you used as a parameter value earlier in the policy assignment i.e. we assigned Japan West earlier as the allowed Datacenter location, so use (Europe) North Europe now</p>
<p>•Username: azureuser</p> 
<p>•Password: Password0134!</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/13.PNG"/>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/14.PNG"/>
<p>3. You will receive a Validation failed message, and click on the Click here to view details message the resultant Errors blade, on the Summary tab note the error message, Resource xyz was disallowed by Policy and the policy name listed as Allowed locations.</p>
<p>You can dig in further for specifics, by clicking on the Raw Error tab and viewing the output and also by clicking on the Allowed locations policy, to view the policy that blocked the deployment.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/15.jpg"/>

<h2>Delete the policy assignment:</h2> 
<p>1. In the Azure Portal click All Services > Management + governance then Policy and on the Policy pane select Compliance in the left side of the page. Within this pane you can view the compliance state of the various policies you have assigned.</p>
<p>Note:The Allowed location policy is listed as non-compliant in the screenshot, as there are pre-existing resources deployed outside of Japan West, which were created prior to the policy assignment, when using Azure Cloud Shell and other Azure resources.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/16.PNG"/>
<p>2. Go to Assignments and click on the ellipsis at the end of the Allowed locations policy assignment. Then select Delete Assignment from the resultant menu.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/17.jpg"/>  
<p>3. Confirm you wish to delete the policy assignment in the Delete assignment dialogue by clicking Yes.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-002/18.jpg"/>     
