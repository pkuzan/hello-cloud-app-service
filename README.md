# Hello Cloud App Service 
An Azure App Service experiment.

This project demonstrates how to deploy a s Spring Boot application to Azure App Service using the 
azure-webapp-maven-plugin.

HelloCloud uses an H2 database with Spring Data JPA for persistence. This will be replaced with SQL Server.
Currently there is only a Swagger UI.


##
Setup

```
az login
az account show --query "{subscriptionId:id, tenantId:tenantId}"
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/&lt;your subscription id&gt;"
```

It will respond :
```
{
  "appId": "&lt;app id&gt;",
  "displayName": "&lt;displaynane&gt;",
  "name": "&lt;name&gt;",
  "password": "&lt;password&gt;",
  "tenant": "&lt;tennant&gt;"
}
```



In your Maven settings.xml add the following, replacing the placeholders with your values, this 
will be used to authenticate the plugin.

```
&lt;servers&gt;
   &lt;server&gt;
     &lt;id&gt;azure-ftp-auth&lt;/id&gt;
      &lt;configuration&gt;
         &lt;client&gt;app id&lt;/client&gt;
         &lt;tenant&gt;tennand&lt;/tenant&gt;
         &lt;key&gt;password&lt;/key&gt;
         &lt;environment&gt;AZURE&lt;/environment&gt;
      &lt;/configuration&gt;
   &lt;/server&gt;
&lt;/servers&gt;
```
The appName and resourceGroup attributes of the azure-webapp-maven-plugin in the POM will need to be edited, 
appName needs to be something globally unique and resourceGroup should refer to an existing Resource Group otherwise a 
new one will be created. 

```
&lt;resourceGroup&gt;HelloCloud&lt;/resourceGroup&gt;
&lt;appName&gt;hello-cloud-pk-007&lt;/appName&gt;
```

Run azure-webapp:deploy to deploy to App Service.
