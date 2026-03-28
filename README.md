# billylouisengineeringconsultant
To deploy WebApp to Azure App Service


```shell
##### STEPS: (From Azure Cloud Shell)
### After creation of the website template in Azure Portal > App Service > Create
### Launch the Cloud Shell from Azure Portal
### Follow the instructions on the Microsoft lean how to "launch the webapp"
```
Link: https://learn.microsoft.com/en-us/training/modules/host-a-web-app-with-azure-app-service/2-create-a-web-app-in-the-azure-portal
```shell
### Bootstrap a web application
# Simply:
$ dotnet new mvc --name <YourAppName>
$ git init
$ git add .
$ git commit -m "Initial commit"

##### STEPS: (from Windows WSL ubuntu24.04)
#### Install|Configure linux packages:
# Because in Azure portal the "Runtime Stack = .NET 8(LTS)" & the OS is "Linux"
# In VS Code using Windows  WSL  - (Open .csproj):
$ code billylouisengineeringconsultant.csproj

# Which shows:
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net9.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>

</Project>

#  Use VS Code + .NET 8 SDK
$ wget https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
$ sudo dpkg -i packages-microsoft-prod.deb
$ sudo apt-get update
$ sudo apt-get install -y dotnet-sdk-9.0

### OR
#  Use VS Code + .NET 9 SDK
$ sudo wget -O - https://packages.microsoft.com/keys/microsoft.asc \
    | gpg --dearmor \
    | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null

$ echo "Types: deb
URIs: https://packages.microsoft.com/ubuntu/22.04/prod/
Suites: jammy
Components: main
Architectures: amd64
Signed-By: /etc/apt/keyrings/microsoft.gpg" \
| sudo tee /etc/apt/sources.list.d/microsoft.sources

$ sudo apt-get update
$ sudo apt-get install -y dotnet-sdk-9.0

$ dotnet --list-sdks
# You should see:
9.0.xxx



### To Compile & Run the code in the browser:
# http://localhost:5000
# http://localhost:5227
$ dotnet restore
$ dotnet build
$ dotnet run


#### If having SDK error issues (in Ubuntu 24.04 only) like:
dotnet-host-8.0 : Conflicts: dotnet-host

# Remove the host:
sudo apt remove -y dotnet-host
sudo apt remove -y dotnet-host-8.0

sudo apt-get update
sudo apt-get install -y dotnet-sdk-9.0
dotnet --list-sdks

```
🟦 Why removing dotnet-host is safe
- Ubuntu’s built‑in .NET host is not used by the project
- Microsoft’s .NET SDK includes its own host
- Removing the Ubuntu version avoids conflicts
- This is the official workaround recommended by Microsoft engineer


## Authors
- [Billy Louis](): Professional WebApp using .NET 8 (LTS) - Azure AppService.


## Badges
Hardware Team: [EULA.com](https://www.icertis.com/contracting-basics/the-importance-of-the-end-user-license-agreement/)

[![EULA License](https://img.shields.io/badge/License-EULA-red.svg)](https://choosealicense.com/licenses/eula/)
