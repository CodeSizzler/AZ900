<h1>Create Password secret with Azure Key Vault</h1>
<h2>Use Case</h2>
<p>In this walkthrough task we will create an Azure Key vault and then create a password secret within that key vault, providing a securely stored, centrally managed password for use with applications.</p>

<h2>Prerequisites</h2>
<p>You require need an Azure subscription to perform these steps. If you don't have one you can create one by following the steps outlined on the Create your Azure free account today webpage.</p>

<h2>Steps:</h2>

<h2>Create a vault in Azure Key Vault:</h2>
<p>1. Sign into the Azure Portal and go to All services > Security and then select Key vaults.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/1.jpg"/>
<p>2. In the Key vaults pane click on Create key vault.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/2.PNG"/>
<p>3. In the Create key vault blade, enter the details as below and click Create.</p>
<p>•Name: a name for your vault i.e. akvtest1</p> 
<p>•Subscription: < your subscription > </p>
<p>•Resource Group: select Create new and enter a new resource group name i.e.akvrg</p>
<p>•Location: < a Datacenter location near you i.e. Central US > </p>
<p>•Pricing Tier: Standard</p>   
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/3.jpg"/>
<p>•Pricing Tier: Standard • Access policies: < accept default value i.e. 1 principal selected > </p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/4.jpg"/>
<p>•Virtual Network Access: < accept default value i.e. all networks can access > </p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/5.jpg"/>
<p>Click on create button.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/6.jpg"/>
<p>4. Go to the newly created Key vault and verify it is present. You can take a moment to browse through some of the options available within it, primarily under Settings and then options concerning Keys, Secrets, Certificates, Access Policies, Firewalls and virtual networks.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/7.jpg"/>
<p>5. Take note of two values in the key vault.</p>
<p>•Vault Name: In the example it is akvtest1</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/8.jpg"/> 
<p>•DNS name (also sometimes referred to as the Vault URI): In this example it is https://akvtest1.vault.azure.net Applications that use your vault through its REST API must use this URI.</p> 
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/9.jpg"/> 
<p>Note: Your Azure account is the only one authorized to perform operations on this new vault. Yo can modify this if you wish in the Settings > Access policies section.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/10.jpg"/>

<h2>Add a secret to the Key Vault:</h2>
<p>1. On the Key Vault properties pages select Secrets, then select Generate/Import.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/11.jpg"/>
<p>2. On the Create a secret blade enter the below values, leave the other values at their defaults and then click Create.</p>  
<p>•Upload options: Manual</p>
<p>•Name: ExamplePassword</p>
<p>•Value: hVFkk965BuUv96!</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/12.jpg"/>
<p>3. Once the secret has been successfully created, on the Secrets pane, click on the 
ExamplePassword, and note it has a status of Enabled.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/13.jpg"/> 
<p>4. Double click on the password and in the password pane, note the presence of the Secret Identifier. This is the url value that you can now use with applications. It provides a centrally managed and securely stored password for use with applications.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/14.PNG"/> 
<p>5. In the same pane click the button Show Secret Value, to display the password you specified earlier.</p>
<p>Note: It is also possible to set time limitations on when a password is available for use, using the activation and expiration date settings.</p>
<img src="https://codesizzlergit.blob.core.windows.net/az900-003/15.jpg"/> 
 
