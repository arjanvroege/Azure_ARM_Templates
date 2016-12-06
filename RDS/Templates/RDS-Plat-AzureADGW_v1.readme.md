This template is based on a cloud-only template using the following technologies: Azure Active Directory Domain Services and Azure Active Directory Application Proxy. This implies that the deployment of an Active Directory and deployment of RD Gateway servers in the DMZ is not part of this template. Later this month I will publish a template which will deploy a RDS environment in an existing Active Directory using RD Gateway servers in the DMZ. This template has the following pre-requisites:

- Azure Active Directory Domain Services ( http://www.vroege.biz/?p=2680 );
- Azure Active Directory Application Proxy ( http://www.vroege.biz/?p=2462 );
- Azure Key Vault for securely storing passwords;
  - Save your local administrator password of the servers to a secret named: localadminCO;
  - Save your certificate password to a secret named: certificatepsswd;
  - Save your password of the domain join user to a secret named: domainjoinpsswd;
- Azure Storage account for hosting the certificate used in your RDS environment;

Next step is to download both the template file and the parameters file from my GitHub account and save both files to a local location in your workstation. Next step is to change the parameter file to your environment. At least the following parameters need to be adjusted to your own environment:

- <b>adminPassword</b>: Change the KeyVault ID so it points to the Azure KeyVault created in step 3;
- <b>CertifcatePFXName</b>: Change this value to the name of the certificate which you have upload to the storage account created in step 4;
- <b>CertifcatePFXPassword</b>: Change the KeyVault ID so it points to the Azure KeyVault created in step 3;
- <b>DomainJoinUserPassword</b>: Change the KeyVault ID so it points to the Azure KeyVault created in step 3;
- <b>DomainFQDN</b>: Change this value to the Fully Qualified Domain Name on your Active Directory domain;
- <b>DomainFQDNExt</b>: Change this value to the Fully Qualified Domain Name of your public domain;
- <b>AssetStorageAccount</b>: Change this value to the Storage Account Name created in Step 4;
- <b>AssetStorageAccountKey</b>: Change this value to the Storage Account Key created in Step 4;

<b>Note</b>: Within the RDS environment a valid certificate is needed for configuring the specific roles. This certificate need to be upload to a private storage account protected with a key. You can use an existing or a new storage account.

When you have adjusted the template and the parameter to your needs you can deploy the template by using the ‘Deploy-AzureResourceGroup.ps1‘ which you can also find on my GitHub account. You need to pass the following parameters to this file:

- <b>ResourceGroupLocation</b>: the location of the Resource Group of all Azure Resources deployed through this template;
- <b>ResourceGroupName</b>: the location of the Resource Group of all Azure Resources deployed through this template;
- <b>TemplateFile</b>: the template which you have saved and changed in the above step;
- <b>ParametersFile</b>: the parameters file which you have saved and changed in the above step;
- <b>Test</b>: Set this Boolean to true if you want to test the deployment and set this Boolean to false if you want to deploy the template;
