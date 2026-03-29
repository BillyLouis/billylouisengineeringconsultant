# billylouisengineeringconsultant
To deploy WebApp to Azure App Service


```shell
##### STEPS: (From Azure Cloud Shell)
### After creation of the website template in Azure Portal > App Service > Create
### Launch the Cloud Shell from Azure Portal
### Follow the instructions on the Microsoft-learning website: how to "launch the webapp"
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



## ##########
##### FULL BUILD AND DEPLOY (SAMPLE)
```shell
billy [ ~ ]$ dotnet new mvc --name billylouisengineeringconsultant.azurewebsites.net

Welcome to .NET 9.0!
---------------------
SDK Version: 9.0.308

Telemetry
---------
The .NET tools collect usage data in order to help us improve your experience. It is collected by Microsoft and shared with the community. You can opt-out of telemetry by setting the DOTNET_CLI_TELEMETRY_OPTOUT environment variable to '1' or 'true' using your favorite shell.

Read more about .NET CLI Tools telemetry: https://aka.ms/dotnet-cli-telemetry

----------------
Installed an ASP.NET Core HTTPS development certificate.
To trust the certificate, run 'dotnet dev-certs https --trust'
Learn about HTTPS: https://aka.ms/dotnet-https

----------------
Write your first app: https://aka.ms/dotnet-hello-world
Find out whats new: https://aka.ms/dotnet-whats-new
Explore documentation: https://aka.ms/dotnet-docs
Report issues and find source on GitHub: https://github.com/dotnet/core
Use 'dotnet --help' to see available commands or visit: https://aka.ms/dotnet-cli
--------------------------------------------------------------------------------------
An issue was encountered verifying workloads. For more information, run "dotnet workload update".
The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore/9.0-third-party-notices for details.

Processing post-creation actions...
Restoring /home/billy/billylouisengineeringconsultant.azurewebsites.net/billylouisengineeringconsultant.azurewebsites.net.csproj:
Restore succeeded.


billy [ ~ ]$ ls
billylouisengineeringconsultant.azurewebsites.net
billy [ ~ ]$ rm -rf billylouisengineeringconsultant.azurewebsites.net/
billy [ ~ ]$ dotnet new mvc --name billylouisengineeringconsultant
The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore/9.0-third-party-notices for details.

Processing post-creation actions...
Restoring /home/billy/billylouisengineeringconsultant/billylouisengineeringconsultant.csproj:
Restore succeeded.


billy [ ~ ]$ ls
billylouisengineeringconsultant
billy [ ~ ]$ mkdir -p go/src/github.com/BillyLouis/
billy [ ~ ]$ ls
billylouisengineeringconsultant  go
billy [ ~ ]$ tree
bash: tree: command not found
billy [ ~ ]$ pwd
/home/billy
billy [ ~ ]$ ls
billylouisengineeringconsultant  go
billy [ ~ ]$ ls billylouisengineeringconsultant/
appsettings.Development.json  appsettings.json  billylouisengineeringconsultant.csproj  Controllers  Models  obj  Program.cs  Properties  Views  wwwroot
billy [ ~ ]$ ls
billylouisengineeringconsultant  go
billy [ ~ ]$ cd go/src/github.com/BillyLouis/
billy [ ~/go/src/github.com/BillyLouis ]$ git br
git: 'br' is not a git command. See 'git --help'.

The most similar commands are
        branch
        var
billy [ ~/go/src/github.com/BillyLouis ]$ git branch
fatal: not a git repository (or any of the parent directories): .git
billy [ ~/go/src/github.com/BillyLouis ]$ git clone https://github.com/BillyLouis/billylouisengineeringconsultant.git
Cloning into 'billylouisengineeringconsultant'...
remote: Enumerating objects: 304, done.
remote: Counting objects: 100% (304/304), done.
remote: Compressing objects: 100% (196/196), done.
remote: Total 304 (delta 96), reused 298 (delta 92), pack-reused 0 (from 0)
Receiving objects: 100% (304/304), 5.73 MiB | 24.84 MiB/s, done.
Resolving deltas: 100% (96/96), done.
billy [ ~/go/src/github.com/BillyLouis ]$ ls
billylouisengineeringconsultant
billy [ ~/go/src/github.com/BillyLouis ]$ cd billylouisengineeringconsultant/
billy [ ~/go/src/github.com/BillyLouis/billylouisengineeringconsultant ]$ ls
appsettings.Development.json  appsettings.json  billylouisengineeringconsultant.csproj  bin  Controllers  Models  obj  Program.cs  Properties  README.md  Views  wget-log  wwwroot
billy [ ~/go/src/github.com/BillyLouis/billylouisengineeringconsultant ]$ dotnet publish -o pub
Restore complete (0.7s)
  billylouisengineeringconsultant succeeded (26.5s) → pub/

Build succeeded in 27.5s
billy [ ~/go/src/github.com/BillyLouis/billylouisengineeringconsultant ]$ cd pub
billy [ ~/go/src/github.com/BillyLouis/billylouisengineeringconsultant/pub ]$ ls
appsettings.Development.json     billylouisengineeringconsultant.deps.json  billylouisengineeringconsultant.runtimeconfig.json              wwwroot
appsettings.json                 billylouisengineeringconsultant.dll        billylouisengineeringconsultant.staticwebassets.endpoints.json
billylouisengineeringconsultant  billylouisengineeringconsultant.pdb        web.config
billy [ ~/go/src/github.com/BillyLouis/billylouisengineeringconsultant/pub ]$ ls wwwroot/
billylouisengineeringconsultant.styles.css     billylouisengineeringconsultant.styles.css.gz  css          favicon.ico.br  js   resume
billylouisengineeringconsultant.styles.css.br  certs                                          favicon.ico  favicon.ico.gz  lib
billy [ ~/go/src/github.com/BillyLouis/billylouisengineeringconsultant/pub ]$ zip -r site.zip *
  adding: appsettings.Development.json (deflated 28%)
  adding: appsettings.json (deflated 26%)
  adding: billylouisengineeringconsultant (deflated 58%)
  adding: billylouisengineeringconsultant.deps.json (deflated 54%)
  adding: billylouisengineeringconsultant.dll (deflated 70%)
  adding: billylouisengineeringconsultant.pdb (deflated 33%)
  adding: billylouisengineeringconsultant.runtimeconfig.json (deflated 49%)
  adding: billylouisengineeringconsultant.staticwebassets.endpoints.json (deflated 95%)
  adding: web.config (deflated 39%)
  adding: wwwroot/ (stored 0%)
  adding: wwwroot/lib/ (stored 0%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/ (stored 0%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/dist/ (stored 0%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/dist/jquery.validate.unobtrusive.min.js.br (stored 0%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/dist/jquery.validate.unobtrusive.min.js (deflated 63%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/dist/jquery.validate.unobtrusive.js (deflated 76%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/dist/jquery.validate.unobtrusive.js.gz (stored 0%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/dist/jquery.validate.unobtrusive.js.br (stored 0%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/dist/jquery.validate.unobtrusive.min.js.gz (stored 0%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/LICENSE.txt (deflated 42%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/LICENSE.txt.br (stored 0%)
  adding: wwwroot/lib/jquery-validation-unobtrusive/LICENSE.txt.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/ (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/ (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/ (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.css.gz (deflated 1%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.min.css (deflated 87%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.min.css.gz (deflated 9%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.css.map.gz (deflated 3%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.css.map (deflated 83%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.min.css.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.css.map.gz (deflated 1%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.min.css.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.min.css.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.css (deflated 89%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.css.map (deflated 84%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.min.css (deflated 87%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.min.css.map (deflated 86%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.min.css.map.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.css.map (deflated 83%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.min.css (deflated 88%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.min.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.css (deflated 72%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.min.css (deflated 69%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.css.map.gz (deflated 2%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.css (deflated 90%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.min.css.map.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.min.css.map.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.css.gz (deflated 4%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.css (deflated 89%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.min.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.css.map.gz (deflated 1%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.css.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.min.css.gz (deflated 1%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.min.css (deflated 68%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.min.css.gz (deflated 1%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.min.css.map (deflated 84%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.min.css.map.gz (deflated 1%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.css.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.css.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.css.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.css (deflated 72%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.css.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.css.gz (deflated 1%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.min.css (deflated 87%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.css.map.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.min.css.map.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.css.gz (deflated 6%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.min.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.min.css.map (deflated 86%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.min.css.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.css.gz (deflated 6%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.css.map (deflated 80%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.min.css.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.css (deflated 88%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.css.map (deflated 84%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.css.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.min.css.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.css.map.gz (deflated 2%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.min.css.map.gz (deflated 2%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.css.map.gz (deflated 3%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.css.map.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.min.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.min.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.min.css.gz (deflated 2%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.min.css.map (deflated 77%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.min.css (deflated 88%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.css.map (deflated 80%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.min.css.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.min.css.map (deflated 84%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.css (deflated 90%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.min.css.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.min.css.map.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.min.css.map (deflated 88%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.min.css.map.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.min.css.map.gz (deflated 2%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.min.css.map.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.min.css.map.gz (deflated 3%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.css.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.css.map (deflated 84%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.css.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.css (deflated 88%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.css.map.br (deflated 1%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.rtl.min.css.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.css.map (deflated 84%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.css.gz (deflated 5%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-utilities.rtl.min.css (deflated 87%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.rtl.min.css.map (deflated 88%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.min.css.br (deflated 4%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.css.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.css.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.rtl.min.css.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap.css.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-reboot.min.css.map (deflated 76%)
  adding: wwwroot/lib/bootstrap/dist/css/bootstrap-grid.min.css.gz (deflated 3%)
  adding: wwwroot/lib/bootstrap/dist/js/ (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.min.js (deflated 71%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.js (deflated 79%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.js.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.js.map (deflated 79%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.js.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.min.js.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.min.js.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.js.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.js (deflated 79%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.js.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.min.js.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.js.map (deflated 79%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.js.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.min.js.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.js.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.js.map (deflated 79%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.min.js.map (deflated 74%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.js.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.min.js (deflated 73%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.min.js.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.min.js.map (deflated 75%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.js.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.min.js.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.min.js.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.min.js (deflated 75%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.min.js.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.min.js.map (deflated 75%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.js.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.min.js.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.esm.min.js.gz (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.min.js.br (stored 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.min.js.map.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.js.map.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.js (deflated 80%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.js.gz (deflated 0%)
  adding: wwwroot/lib/bootstrap/dist/js/bootstrap.bundle.js.br (deflated 0%)
  adding: wwwroot/lib/bootstrap/LICENSE (deflated 42%)
  adding: wwwroot/lib/jquery-validation/ (stored 0%)
  adding: wwwroot/lib/jquery-validation/dist/ (stored 0%)
  adding: wwwroot/lib/jquery-validation/dist/additional-methods.js.br (stored 0%)
  adding: wwwroot/lib/jquery-validation/dist/jquery.validate.min.js.br (stored 0%)
  adding: wwwroot/lib/jquery-validation/dist/additional-methods.min.js.br (stored 0%)
  adding: wwwroot/lib/jquery-validation/dist/additional-methods.min.js.gz (stored 0%)
  adding: wwwroot/lib/jquery-validation/dist/additional-methods.min.js (deflated 71%)
  adding: wwwroot/lib/jquery-validation/dist/jquery.validate.min.js (deflated 68%)
  adding: wwwroot/lib/jquery-validation/dist/additional-methods.js (deflated 74%)
  adding: wwwroot/lib/jquery-validation/dist/additional-methods.js.gz (stored 0%)
  adding: wwwroot/lib/jquery-validation/dist/jquery.validate.min.js.gz (stored 0%)
  adding: wwwroot/lib/jquery-validation/dist/jquery.validate.js (deflated 73%)
  adding: wwwroot/lib/jquery-validation/dist/jquery.validate.js.br (stored 0%)
  adding: wwwroot/lib/jquery-validation/dist/jquery.validate.js.gz (stored 0%)
  adding: wwwroot/lib/jquery-validation/LICENSE.md (deflated 42%)
  adding: wwwroot/lib/jquery-validation/LICENSE.md.br (stored 0%)
  adding: wwwroot/lib/jquery-validation/LICENSE.md.gz (stored 0%)
  adding: wwwroot/lib/jquery/ (stored 0%)
  adding: wwwroot/lib/jquery/dist/ (stored 0%)
  adding: wwwroot/lib/jquery/dist/jquery.js.gz (deflated 0%)
  adding: wwwroot/lib/jquery/dist/jquery.js.br (deflated 0%)
  adding: wwwroot/lib/jquery/dist/jquery.slim.min.map.gz (deflated 0%)
  adding: wwwroot/lib/jquery/dist/jquery.slim.js (deflated 71%)
  adding: wwwroot/lib/jquery/dist/jquery.min.map (deflated 60%)
  adding: wwwroot/lib/jquery/dist/jquery.slim.min.js.br (stored 0%)
  adding: wwwroot/lib/jquery/dist/jquery.min.map.br (deflated 0%)
  adding: wwwroot/lib/jquery/dist/jquery.slim.min.map (deflated 60%)
  adding: wwwroot/lib/jquery/dist/jquery.min.map.gz (deflated 0%)
  adding: wwwroot/lib/jquery/dist/jquery.slim.min.map.br (deflated 0%)
  adding: wwwroot/lib/jquery/dist/jquery.min.js (deflated 65%)
  adding: wwwroot/lib/jquery/dist/jquery.slim.min.js (deflated 66%)
  adding: wwwroot/lib/jquery/dist/jquery.slim.js.gz (deflated 0%)
  adding: wwwroot/lib/jquery/dist/jquery.min.js.gz (stored 0%)
  adding: wwwroot/lib/jquery/dist/jquery.js (deflated 71%)
  adding: wwwroot/lib/jquery/dist/jquery.min.js.br (stored 0%)
  adding: wwwroot/lib/jquery/dist/jquery.slim.js.br (deflated 0%)
  adding: wwwroot/lib/jquery/dist/jquery.slim.min.js.gz (stored 0%)
  adding: wwwroot/lib/jquery/LICENSE.txt (deflated 42%)
  adding: wwwroot/lib/jquery/LICENSE.txt.br (stored 0%)
  adding: wwwroot/lib/jquery/LICENSE.txt.gz (stored 0%)
  adding: wwwroot/certs/ (stored 0%)
  adding: wwwroot/certs/Certificate_MS_Program6_PMP_Finance_and_Investment.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_MS_introductionToCloudComputing.pdf (deflated 1%)
  adding: wwwroot/certs/AZ104MSAzureAdminPreReqRotate.pdf (deflated 15%)
  adding: wwwroot/certs/Certificate_ISO45001_B6ZFX5H3IXD4.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_MS_Program2_PMP_TeamBuilding.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_Github_FundamentalsWorkFlow2AdvanceFeatures.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_AZ104MSAzureToolsAndSecurity.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_MS_Program3_PMP_CommunicateWithStakeholders.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_Docker_Fundamentals.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_MS_IntroductionToSecureNetworking.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_MS_Program5_PMP_Agile_and_Hybrid_Approaches.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_AZ104AzureAdmin1of3.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_AZ104MSAzureAdminPreReq.pdf (deflated 15%)
  adding: wwwroot/certs/Certificate_Github_and_Git_ForDevOps.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_Github_Fundamentals.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_RDMAprogramming.pdf (deflated 2%)
  adding: wwwroot/certs/Certificate_Github_FundamentalBeginner.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_mmWaveCircuitDesign.pdf (deflated 2%)
  adding: wwwroot/certs/Certificate_Github_FundamentalsWorkFlow1.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_MS_ProgramManagementSpecialization_VG66HRH67TLA.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_MS_Program4_PMP_Performance_Domains.pdf (deflated 1%)
  adding: wwwroot/certs/Certificate_MachineLearningStandFord.pdf (deflated 2%)
  adding: wwwroot/certs/Certificate_TCP_IP_Fundamentals.pdf (deflated 2%)
  adding: wwwroot/certs/Certificate_MS_ProgramManagementFundamentals.pdf (deflated 1%)
  adding: wwwroot/billylouisengineeringconsultant.styles.css.gz (stored 0%)
  adding: wwwroot/css/ (stored 0%)
  adding: wwwroot/css/site.css.gz (stored 0%)
  adding: wwwroot/css/site.css (deflated 62%)
  adding: wwwroot/css/site.css.br (stored 0%)
  adding: wwwroot/favicon.ico.br (stored 0%)
  adding: wwwroot/js/ (stored 0%)
  adding: wwwroot/js/site.js.br (stored 0%)
  adding: wwwroot/js/site.js (deflated 26%)
  adding: wwwroot/js/site.js.gz (stored 0%)
  adding: wwwroot/favicon.ico (deflated 56%)
  adding: wwwroot/billylouisengineeringconsultant.styles.css (deflated 52%)
  adding: wwwroot/billylouisengineeringconsultant.styles.css.br (stored 0%)
  adding: wwwroot/favicon.ico.gz (stored 0%)
  adding: wwwroot/resume/ (stored 0%)
  adding: wwwroot/resume/EngineeringBJL1Resume910ref.pdf (deflated 9%)
billy [ ~/go/src/github.com/BillyLouis/billylouisengineeringconsultant/pub ]$ 
billy [ ~/go/src/github.com/BillyLouis/billylouisengineeringconsultant/pub ]$ az webapp deploy \
    --src-path site.zip \
    --resource-group AzAppGp001 \
    --name billylouisengineeringconsultant
Deployment type: zip. To override deployment type, please specify the --type parameter. Possible values: war, jar, ear, zip, startup, script, static
Initiating deployment
Deploying from local path: site.zip
Warming up Kudu before deployment.
Warmed up Kudu instance successfully.
Polling the status of sync deployment. Start Time: 2026-03-29 05:20:44.482498+00:00 UTC
Status: Build successful. Time: 1(s)
Status: Starting the site... Time: 16(s)
Status: Starting the site... Time: 32(s)
Status: Starting the site... Time: 47(s)
Status: Starting the site... Time: 63(s)
Status: Starting the site... Time: 79(s)
Status: Starting the site... Time: 94(s)
Status: Starting the site... Time: 110(s)
Status: Starting the site... Time: 125(s)
Status: Starting the site... Time: 141(s)
Status: Starting the site... Time: 157(s)
Status: Starting the site... Time: 172(s)
Status: Starting the site... Time: 188(s)
Status: Starting the site... Time: 203(s)
Status: Starting the site... Time: 231(s)
Status: Starting the site... Time: 247(s)



```
## ###########

## Authors
- [Billy Louis](): Professional WebApp using .NET 8 (LTS) - Azure AppService.


## Badges
Hardware Team: [EULA.com](https://www.icertis.com/contracting-basics/the-importance-of-the-end-user-license-agreement/)

[![EULA License](https://img.shields.io/badge/License-EULA-red.svg)](https://choosealicense.com/licenses/eula/)
