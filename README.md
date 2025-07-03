# Environment-WebApi

> This project is an example of an API used to publish and debug a project via Web Deploy in Visual Studio, based on the environment JSON file.

---

## 🚀 Getting Started

### Program.cs

```csharp
var environment = builder.Environment.EnvironmentName;

builder.Configuration
    .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)
    .AddJsonFile($"appsettings.{environment}.json", optional: true, reloadOnChange: true)
    .AddEnvironmentVariables();
````

---

## 🧩 Environment JSON Files

* appsettings.json
* appsettings.Development.json
* appsettings.Beta.json
* appsettings.Production.json

---

## 📤 Launch Settings Configuration for Debugging

**launchSettings.json:**

```json
{
  "$schema": "http://json.schemastore.org/launchsettings.json",
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:31758",
      "sslPort": 44310
    }
  },
  "profiles": {
    "Development": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "launchUrl": "swagger",
      "applicationUrl": "https://localhost:5001;http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    },
    "Beta": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "launchUrl": "swagger",
      "applicationUrl": "https://localhost:5001;http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Beta"
      }
    },
    "Production": {
      "commandName": "Project",
      "dotnetRunMessages": true,
      "launchBrowser": true,
      "launchUrl": "swagger",
      "applicationUrl": "https://localhost:5001;http://localhost:5000",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Production"
      }
    },
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "launchUrl": "swagger",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

---

## 📤 Publish Profiles

Use Web Deploy with publish profiles:

* Beta-FolderProfile.pubxml
* Development-FolderProfile.pubxml
* Production-FolderProfile.pubxml

Example `.pubxml` file:

```xml
<Project>
  <PropertyGroup>
    <EnvironmentName>Beta</EnvironmentName> <!-- Possible values: Production, Development, Stage -->
    <DeleteExistingFiles>true</DeleteExistingFiles>
    <ExcludeApp_Data>false</ExcludeApp_Data>
    <LaunchSiteAfterPublish>true</LaunchSiteAfterPublish>
    <LastUsedBuildConfiguration>Release</LastUsedBuildConfiguration>
    <LastUsedPlatform>Any CPU</LastUsedPlatform>
    <PublishProvider>FileSystem</PublishProvider>
    <PublishUrl>bin\Release\net8.0\publish\</PublishUrl>
    <WebPublishMethod>FileSystem</WebPublishMethod>
    <_TargetId>Folder</_TargetId>
    <SiteUrlToLaunchAfterPublish />
    <TargetFramework>net8.0</TargetFramework>
    <ProjectGuid>b145306a-0951-443c-b259-60425ce82c01</ProjectGuid>
    <SelfContained>false</SelfContained>
  </PropertyGroup>
</Project>
```

---

## ⚙️ Web Config

**web.config**

```xml
<configuration>
  <location path="." inheritInChildApplications="false">
    <system.webServer>
      <handlers>
        <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
      </handlers>
      <aspNetCore processPath="dotnet" arguments=".\EnvironmentWebApi.dll" stdoutLogEnabled="false" stdoutLogFile=".\logs\stdout" hostingModel="inprocess">
        <environmentVariables>
          <environmentVariable name="ASPNETCORE_ENVIRONMENT" value="Production" /> <!-- Possible values: Beta, Development, Stage -->
        </environmentVariables>
      </aspNetCore>
    </system.webServer>
  </location>
</configuration>
```

---

## 📦 Features

✅ Tek tıkla ortam değişkeni debuglama
✅ Tek tıkla ortam değişkeni publish etme
✅ Kolay kullanım

---

## 📁 License

Licensed under the MIT License.

```
