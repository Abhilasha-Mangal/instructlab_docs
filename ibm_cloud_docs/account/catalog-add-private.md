---

copyright:
  years: 2019, 2023
lastupdated: "2023-04-26"

keywords: catalog, catalogs, private catalogs, account catalogs, catalog visibility, software visibility, import software

subcollection: account

---

{{site.data.keyword.attribute-definition-list}}

# Onboarding software to your account
{: #create-private-catalog}

The process to onboard software to your account includes importing a version to a private catalog, validating that the version can be successfully installed on the target infrastructure that you require, and sharing the software to your account. The software is then available to users in your account.
{: shortdesc}

## Before you begin
{: #prereq-create}

1. Verify that you're using a Pay-As-You-Go or Subscription account. See [Viewing your account type](/docs/account?topic=account-account_settings#view-acct-type) for more details.

1. Review the list of software that you can onboard:

   * Helm charts on Kubernetes and {{site.data.keyword.openshiftshort}} clusters
   * Terraform templates
   * OVA images that are deployed on VMware Solutions Dedicated - vCenter Server
   * Virtual server images with Terraform deployed on VPC infrastructure or {{site.data.keyword.powerSys_notm}}
   * Virtual server images for VPC
   * Operators with a TGZ file from GitHub or GitLab repositories
   * Operator bundles from Red Hat OpenShift registries

1. Upload your source code to a release in your GitHub or GitLab repository. See [Setting up your source code repository](/docs/sell?topic=sell-source-repo-setup).

1. Make sure you're assigned the following [IAM access](/docs/account?topic=account-groups):

   * Editor role on the catalog management service
   * Viewer role on all resource groups in your account
   * Writer role on the {{site.data.keyword.secrets-manager_short}} service

1. Install the {{site.data.keyword.cloud_notm}} CLI and the {{site.data.keyword.bplong_notm}} plug-in. See [Setting up the CLI](/docs/schematics?topic=schematics-setup-cli) for more information.

For containerized apps, complete the following prerequisites:

   1. Create your [Kubernetes cluster](/docs/containers?topic=containers-getting-started) or [Red Hat OpenShift cluster](/docs/openshift?topic=openshift-getting-started).
   2. For deployments to {{site.data.keyword.cloud_notm}} Kubernetes Service, [set up your Helm chart](/docs/containers?topic=containers-helm).
   3. For deployments to Red Hat OpenShift, set up your [Helm chart](/docs/openshift?topic=openshift-helm) or [Operator](/docs/openshift?topic=openshift-operators).

For virtual server images, complete the following prerequisites:

   1. Review the list of [supported images](/docs/vpc?topic=vpc-about-images).
   2. If required, create your [Terraform template](/docs/schematics?topic=schematics-create-tf-config). Virtual server image for VPC does not require a Terraform template.
   3. Create an instance of [{{site.data.keyword.cloud_notm}} Object Storage](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) and add your image to a bucket.

Before you can onboard software to your account by using Terraform, make sure that you have completed the following:
{: terraform}

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://www.terraform.io/docs/language/index.html){: external}.
{: terraform}

To share software with other accounts, your software must be approved in Partner Center. For more information, see [Getting set up to sell software](/docs/sell?topic=sell-sw-getting-started).
{: important}

## Creating a private catalog
{: #create-catalog-ui}
{: ui}

Private catalogs provide a way for you to manage access to products for users in your account.

1. Go to **Manage** > **Catalogs** in the {{site.data.keyword.cloud_notm}} console, and click **Create a catalog**.
1. Enter a name and description of your catalog.
1. Select to exclude or include all products in the {{site.data.keyword.cloud_notm}} catalog in your private catalog. For more information about how this affects visibility in the catalog, see [Managing catalog settings](/docs/account?topic=account-filter-account&interface=ui).
1. Click **Create**.

## Importing software to your private catalog
{: #add-public-repo-ui}
{: ui}

Complete the following steps to import software to your private catalog:

1. From the Private products page, click **Add**.
1. Select your deployment method.
1. Select whether you are adding your product from a private or public repository. Or, if you're onboarding an Operator from a Red Hat registry, select your Red Hat repository type: **Certified**, **Marketplace**, **Community**.

   If you're adding your product from a private repository, you can provide a personal access token or you can use a secret. Instead of giving users a personal access token, you can give them access to a secret, add the token to a secret, and centrally manage all tokens and access the secret allows.

   * If you're using a personal access token, select **No** to indicate that you aren't using a secret and provide your personal access token.
   * If you're using a secret, select **Yes** and click **Select from Secrets Manager**. Select your service instance, secret group, and secret. If you don't see your secret, make sure you're using the correct secret group and service instance.

    The message `No service instance available` might be displayed if you haven't created a secret or if you don't have the correct access to use secrets, even if you have service instances that are created.
    {: note}

1. Enter your source URL. You can review the following list of supported formats per software type:

   * Helm chart: `https://raw.githubusercontent.com/IBM/charts/master/repo/ibm-helm`
   * Node-RED Operator: `https://github.com/IBM-Cloud/operator-bundle-sample/archive/refs/tags/v0.0.3.tar.gz`
   * Operator bundle from a {{site.data.keyword.openshiftshort}} registry: For an example, select the `Akka Cluster Operator` from the list of available Operators in the Certified repository.
   * OVA image: `https://github.com/gcatalog/OVA-sample/blob/main/ova-sample.yaml`
   * Terraform template: `https://github.com/IBM-Cloud/terraform-sample/releases/tag/v1.0.0`
   * Virtual server image with Terraform: `https://github.com/IBM-Cloud/isv-vsi-product-deploy-sample/releases/download/v1.0/isv-vsi-product-deploy-sample.tar.gz`

   * Virtual server image for VPC: Select an image from the list of available images, or import a new image to onboard it.

    A virtual server image for VPC can only be added to one product within one private catalog at a time. If the virtual server image you want to import is already imported into another product, you must remove the image from that product or delete the product before you add the virtual server image to a new product.
    {: note}

1. If applicable, enter the version of the software in the format of major version, minor version, and revision. For example, enter version 1.1.2.
1. Select a catalog category for the product. Categories are used to organize products in the {{site.data.keyword.cloud_notm}} catalog based on function, use, or common solutions.
1. Click **Add product**.

## Adding catalog entry details
{: #catalog-tile}
{: ui}

When you publish your product to the catalog for users with access to your private catalog, they see a tile with the product name and other details that add during onboarding. In addition to the category that you set when you import your software, you can add other filters that are related to industry, compliance, technologies it works with, and more. Each of these filters is used in the catalog for users to find software that fits their needs. In the catalog entry details section, you can also evaluate and make updates to the short descriptions, documentation URL, and even keywords to help user search and find your product quickly.

1. From the Catalog entry details section, click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit").
2. Review the information that was imported with your product, and make edits as needed.
3. Review the filters and industry options to select catalog filters that apply. You can select up to five industry filters.
4. Check your catalog entry preview to see how your catalog tile displays to users who are evaluating your software in the catalog.
5. Click **Save** when you're happy with your changes.

## Configuring the software
{: #catalog-configure-details}
{: ui}

### Helm chart
{: #catalog-config-helm}
{: ui}

1. From the version list that's displayed on the product details page, click the row that contains your software.
1. Review the version details, and click **Next**.
1. Configure the preinstallation, and click **Next**.
1. Configure the deployment details by setting the access that's required to run the installation script and setting the deployment values, and click **Next**.

### Terraform
{: #catalog-config-tf}
{: ui}

1. From the version list that's displayed on the product details page, click the row that contains your software.
1. Review the version details, and click **Next**.
1. Configure the deployment values.
1. If applicable, edit the output value descriptions, and click **Next**.
1. Define the required IAM access, and click **Next**.

### Operator from GitHub repository
{: #catalog-config-opgh}
{: ui}

1. From the version list that's displayed on the product details page, click the row that contains your software.
1. Review the version details, and click **Next**.

### Operator from Red Hat registry
{: #catalog-config-oprh}
{: ui}

1. From the version list that's displayed on the product details page, click the row that contains your software.
1. Review the version details, and click **Next**.

### OVA image
{: #catalog-config-ova}
{: ui}

1. From the version list that's displayed on the product details page, click the row that contains your software.
1. Review the version details, and click **Next**.

### Virtual server image with Terraform
{: #catalog-config-vsi}
{: ui}

1. From the version list that's displayed on the product details page, click the row that contains your software.
1. Review the version details, and click **Next**.
1. Configure the deployment values.
1. If applicable, edit the output value descriptions, and click **Next**.
1. Define the required IAM access, and click **Next**.

### Virtual server image for VPC
{: #catalog-config-vsivpc}
{: ui}

1. From the version list that's displayed on the product details page, click the row that contains your software.
1. Review the list of images, and click **Next**.
1. Review the version details, and click **Next**.

## Adding license agreements
{: #catalog-add-license}
{: ui}

Provide the URLs to the license agreements that users are required to accept when they install the product. The license agreements are in addition to the {{site.data.keyword.cloud_notm}} Services Agreement.

1. Click **Add license agreements** > **Add license**.
1. Enter the name and URL, and click **Update** > **Next**.

## Editing your readme file
{: #catalog-readme-edit}
{: ui}

When users install the software, they can view product information by clicking the Readme file link. This information is generated from the readme file that you uploaded to your source repository.

1. From the Edit readme tab, preview how the information in the readme file will be displayed to users when they install the software.
1. To make updates, click the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit") next to the Readme section title.
1. Click **Save**.
1. Click **Next**.

If you are importing a virtual server image for VPC, the readme file is not automatically generated. Copy and paste the contents of the [readme file template](/media/docs/downloads/software/sw-readme-tab-template.md){: external} and make updates as needed.
{: note}

## Validating the software
{: #catalog-validate-product}
{: ui}

When you validate your software, you're confirming that the current version can be successfully installed on the deployment target. The validation steps vary based on your deployment method.

To monitor the progress of the validation process, click **View logs**.
{: tip}

### Helm chart
{: #catalog-validate-helm}
{: ui}

1. From the Validate product tab, select your cluster.
1. If the deployment target is a Kubernetes cluster, select a namespace or create a new one. If the deployment target is a Red Hat OpenShift cluster, select a project or create a new one.
1. Click **Next**.
1. Configure your {{site.data.keyword.bplong_notm}} workspace.
1. Click **Next**.
1. If applicable, review the license agreements, and select **I have read and agree to the following license agreements:**.
1. Click **Validate**.

### Terraform
{: #catalog-validate-tf}
{: ui}

1. From the Validate product tab, configure your {{site.data.keyword.bplong_notm}} workspace.
1. Click **Next**.
1. If applicable, review the license agreements, and select **I have read and agree to the following license agreements:**.
1. Click **Validate**.

### Operator from GitHub repository
{: #catalog-validate-opgh}
{: ui}

1. From the Validate product tab, select your Red Hat OpenShift cluster.
1. Select a project or create a new one. A project is similar to a Kubernetes cluster namespace, and the list is populated from your Red Hat OpenShift environment.
1. Click **Next**.
1. Configure your {{site.data.keyword.bplong_notm}} workspace.
1. Click **Next**.
1. If applicable, review the license agreements, and select **I have read and agree to the following license agreements:**.
1. Click **Validate**.

### Operator from Red Hat registry
{: #catalog-validate-oprh}
{: ui}

1. From the Validate product tab, select an update channel.
1. Select an approval strategy.
1. Select your Red Hat OpenShift cluster.
1. Select a project or create a new one. A project is similar to a Kubernetes cluster namespace, and the list is populated from your Red Hat OpenShift environment.
1. Click **Next**.
1. Configure your {{site.data.keyword.bplong_notm}} workspace.
1. Click **Next**.
1. If applicable, review the license agreements, and select **I have read and agree to the following license agreements:**.
1. Click **Validate**.

### OVA image
{: #catalog-validate-ova}
{: ui}

1. From the Validate product tab, review the license agreements, and select **I have read and agree to the following license agreements:**.
1. Click **Validate**.

### Virtual server image with Terraform
{: #catalog-validate-vsi}
{: ui}

1. From the Validate product tab, configure your {{site.data.keyword.bplong_notm}} workspace.
1. Click **Next**.
1. If applicable, review the license agreements, and select **I have read and agree to the following license agreements:**.
1. Click **Validate**.

### Virtual server image for VPC
{: #catalog-validate-vsivpc}
{: ui}

1. From the validate version tab, configure the validation target, and click **Next**.
1. Optionally, configure your Schematics workspace, and click **Next**.
1. If applicable, review the license agreements, and select **I have read and agree to the following license agreements:**.
1. Click **Validate**.

## Manage compliance
{: #catalog-manage-controls}
{: ui}

Controls are safeguards that are used to meet security and compliance requirements. Only controls that are supported by Security and Compliance Center, formatted correctly, and validated by Code Risk Analysis and Security and Compliance Center scans appear in the catalog. For more information, see [Adding compliance details](/docs/account?topic=account-catalog-format-controls).

1. Click **Add controls**.
1. Choose a profile.
1. Select the controls that you want to add to your version.
1. Click **Add**.
1. In the Code Risk Analyzer scan section, click **Run scan**.
1. Wait for the scan to finish.
1. In the Security and Compliance Center scan section, select the profile that you scanned.
1. Select the Security and Compliance Center scan.
1. Click **Add scan**.
1. Click **Next**.

## Review requirements
{: #catalog-manage-review-reqs}

You must complete validation and any other requirements to share to your account. When you're ready to make your product available to all users who have access to your private catalog, click **Ready to share**.

## Sharing the software
{: #validating-software}
{: ui}

If you want to share your product to your account or enterprise, click the name of the product in the navigation to go to the product details page. From the **Actions** menu, click **Share**. Select where you want to share your product, and click **Share**.


## Onboarding software to your catalog by using the CLI
{: #create-cicd-product}
{: cli}

Complete the following steps to add your software by using the CLI. You can use this task in a CI/CD process.

1. Create a private catalog. Private catalogs provide a way for you to manage access to products for users in your account. For more information, see the [cli documentation](/docs/cli?topic=cli-manage-catalogs-plugin#create-catalog) for creating a private catalog.
    ```bash
    ibmcloud catalog create --name CATALOG [--catalog-description "DESCRIPTION"]
    ```
    {: codeblock}

1. Add software to your private catalog. For more information, see the [cli documentation](/docs/cli?topic=cli-manage-catalogs-plugin#create-offering) for adding software to your private catalog.
    ```bash
    ibmcloud catalog offering create --catalog "Name of catalog" --zipurl https://software.url.com.tgz
    ```
    {: codeblock}

    If you want to import software from a private repository, you can use a personal access token by adding [--token TOKEN] to your command.
    {: important}

1. Add a category. By default, the **Developer tools** category is added to your product. For more information, see the [cli documentation](/docs/cli?topic=cli-manage-catalogs-plugin#add-category-offering) for adding a category.
    ```bash
    ibmcloud catalog offering add-category --catalog "Name of catalog" --offering "software-offering" --category "category"
    ```
    {: codeblock}

1. Import the software version that you want in your catalog.
    ```bash
    ibmcloud catalog offering import-version -c <CATALOGID> -o <OFFERINGID> --zipurl <TGZ> --target-version <VERSION>
    ```
    {: codeblock}

    The following shows the list of supported formats per software type:

    * Helm chart: `https://raw.githubusercontent.com/IBM/charts/master/repo/ibm-helm`
    * Node-RED Operator: `https://github.com/IBM-Cloud/operator-bundle-sample/archive/refs/tags/v0.0.3.tar.gz`
    * Operator bundle from a {{site.data.keyword.openshiftshort}} registry: For an example, select the `Akka Cluster Operator` from the list of available Operators in the Certified repository.
    * OVA image: `https://github.com/gcatalog/OVA-sample/blob/main/ova-sample.yaml`
    * Terraform template: `https://github.com/IBM-Cloud/terraform-sample/releases/tag/v1.0.0`
    * Virtual server image with Terraform: `https://github.com/IBM-Cloud/isv-vsi-product-deploy-sample/releases/download/v1.0/isv-vsi-product-deploy-sample.tar.gz`

1. Validate the software. For more information, see the [cli documentation](/docs/cli?topic=cli-manage-catalogs-plugin#validate-offering) for validating the software.
    ```bash
    ibmcloud catalog offering version validate --version-locator VERSION_NUMBER --cluster CLUSTER_ID --namespace NAME [--timeout TIMEOUT] [--wait WAIT] [--override-values VALUES|FILENAME]
    ```
    {: codeblock}

    Deploying the software can take a few minutes. You can check the validation status by querying the product validation state. The validation is complete when the state is Valid. For more information, see the [cli documentation](/docs/cli?topic=cli-manage-catalogs-plugin#validate-status-offering) for validation status.
    ```bash
    ibmcloud catalog offering version validate-status --version-locator VERSION_NUMBER [--output FORMAT]
    ```
    {: codeblock}

1. Publish your software to make it available to users in your account. For more information, see the [cli documentation](/docs/cli?topic=cli-manage-catalogs-plugin#publish-offering-to-account) for publishing to your account.
    ```bash
    ibmcloud catalog offering publish account [--catalog CATALOG][--offering OFFERING]
    ```
    {: codeblock}


## Creating a private catalog by using the API
{: #create-catalog-api}
{: api}

Private catalogs provide a way for you to manage access to products for users in your account. You can programmatically create a private catalog by calling the Catalog Management API as shown in the following sample request. For more information, see the [Catalog Management API](/apidocs/resource-catalog/private-catalog?code=java#create-catalog) for creating a catalog.

```java
String label = "{label}";
String shortDesc = "{shortDesc}";
CreateCatalogOptions createOptions = new CreateCatalogOptions.Builder().label(label).shortDescription(shortDesc).build();
Response<Catalog> response = service.createCatalog(createOptions).execute();
System.out.println(response.getResult());
```
{: codeblock}
{: java}

```javascript
label = "{label}";
shortDesc = "{shortDesc}";
response = await service.createCatalog({ 'label': label, 'shortDescription': shortDesc });
console.log(response);
```
{: codeblock}
{: javascript}

```python
label = "{label}"
shortDesc = "{shortDesc}"
response = self.service.create_catalog(label=label, short_description=shortDesc)
print(response)
```
{: codeblock}
{: python}

```go
label := "{label}"
shortDesc := "{shortDesc}"
createOptions := service.NewCreateCatalogOptions()
createOptions.SetLabel(label)
createOptions.SetShortDescription(shortDesc)
_, response, _ := service.CreateCatalog(createOptions)
fmt.Println(response)
```
{: codeblock}
{: go}

## Importing software to your private catalog by using the API
{: #import-product-api}
{: api}

You can programmatically import software to your catalog by calling the Catalog Management API as shown in the following sample request. This API creates the software and imports it as well. For detailed information about the API, see [Catalog Management API](/apidocs/resource-catalog/private-catalog?code=go#import-offering).

```java
id = "{id}";
offeringURL = "{offeringURL}";
ImportOfferingOptions offeringOptions = new ImportOfferingOptions.Builder().catalogIdentifier(id).zipurl(offeringURL).build();
Response<Offering> response = service.importOffering(offeringOptions).execute();
System.out.println(response.getResult());
```
{: codeblock}
{: java}

```javascript
id = "{id}";
offeringURL = "{offeringURL}";
response = await service.importOffering({ 'catalogIdentifier': id, 'zipurl': offeringURL });
console.log(response);
```
{: codeblock}
{: javascript}

```python
id = "{id}"
offeringURL = "{offeringURL}"
response = self.service.import_offering(catalog_identifier=id, zipurl=offeringURL)
print(response)
```
{: codeblock}
{: python}

```go
id := "{id}"
offeringURL := "{offeringURL}"
offeringOptions := service.NewImportOfferingOptions(id, offeringURL)
_, response, _ := service.ImportOffering(offeringOptions)
fmt.Println(response)
```
{: codeblock}
{: go}

## Validating your software by using the API
{: #validate-product-api}
{: api}

You can programmatically validate your product to by calling the Catalog Management API as shown in the following sample request. This process can take several minutes. For detailed information about the API, see [Catalog Management API](/apidocs/resource-catalog/private-catalog?code=java#validate-install).

```java
String authRefreshToken = "{authRefreshToken}";
String versionLocator = "{versionLocator}";
ValidationInstallOptions installOptions = new ValidationInstallOptions.Builder().xAuthRefreshToken(authRefreshToken).versionLocId(versionLocator).build();
Response<Void> response = service.validationInstall(installOptions).execute();
System.out.println(response.getResult());
```
{: codeblock}
{: java}

```javascript
versionLocator = "{versionLocator}";
authRefreshToken = "{authRefreshToken}";
response = await service.validationInstall({ 'versionLocatorId': versionLocator, 'xAuthRefreshToken': authRefreshToken });
console.log(response);
```
{: codeblock}
{: javascript}

```python
authRefreshToken="{authRefreshToken}"
versionLocator = "{versionLocator}"
response = self.service.validation_install(version_locator_id=versionLocator, x_auth_refresh_token=authRefreshToken)
print(response)
```
{: codeblock}
{: python}

```go
versionLocator := "{versionLocator}"
authRefreshToken := "{authRefreshToken}"
installOptions := service.NewValidationInstallOptions(versionLocator, authRefreshToken)
response, _ := service.ValidationInstall(installOptions)
fmt.Println(response)
```
{: codeblock}
{: go}

## Publishing your software to your account by using the API
{: #publish-product-api}
{: api}

You can programmatically publish your software to your account by calling the Catalog Management API as shown in the following sample request. For detailed information about the API, see [Catalog Management API](/apidocs/resource-catalog/private-catalog?code=java#account-publish-version).

```java
String versionLocator = "{versionLocator}";
AccountPublishVersionOptions publishOption = new AccountPublishVersionOptions.Builder().versionLocId(versionLocator).build();
Response<Void> response = service.accountPublishVersion(publishOption).execute();
System.out.println(response.getResult());
```
{: codeblock}
{: java}

```javascript
versionLocator = "{versionLocator}";
response = await service.accountPublishVersion({ 'versionLocId': versionLocator});
console.log(response);
```
{: codeblock}
{: javascript}

```python
versionLocator = "{versionLocator}"
response = self.service.account_publish_version(version_loc_id=versionLocator)
print(response)
```
{: codeblock}
{: python}

```go
versionLocator := "{versionLocator}"
publishOptions := service.NewAccountPublishVersionOptions(versionLocator)
response, _ := service.AccountPublishVersion(publishOptions)
fmt.Println(response)
```
{: codeblock}
{: go}


## Creating a private catalog by using Terraform
{: #create-catalog-terraform}
{: terraform}

Use the following steps to create a private catalog by using Terraform.

1. Add your argument to your `main.tf` file. The following example creates a private catalog by using the `ibm_cm_catalog` resource, where `label` is a display name to identify the catalog.

   ```terraform
   resource "ibm_cm_catalog" "cm_catalog" {
   label = "label"
   short_description = "short_description"
   }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Catalog Management](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_catalog){: external} page.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://www.terraform.io/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://www.terraform.io/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

## Importing a product to your catalog by using Terraform
{: #create-cicd-product-terraform}
{: terraform}

Use the following steps to import a product to your private catalog by using Terraform.

1. Add your argument to your `main.tf` file. The following example adds your product by using the `ibm_cm_offering` resource, where `label` is a display name to identify the product.

   ```terraform
   resource "ibm_cm_offering" "cm_offering" {
   catalog_id = "catalog_id"
   label = "label"
   tags = [ "tags" ]
   }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Catalog Management](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_offering){: external} page.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://www.terraform.io/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://www.terraform.io/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

## Importing a version of your software by using Terraform
{: #create-cicd-version-terraform}
{: terraform}

After you add your product, use the following steps to add a version of your software by using Terraform.

1. Add your argument to your `main.tf` file. The following example accesses the software version by using the `cm_version` resource, where `offering_id` identifies the software.

   ```terraform
   resource "cm_version" "cm_version" {
   catalog_identifier = "catalog_identifier"
   offering_id = "offering_id"
   zipurl = "zipurl"
   }
   ```
   {: codeblock}

   For more information, see the argument reference details on the [Terraform Catalog Management](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cm_version){: external} page.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://www.terraform.io/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://www.terraform.io/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}
