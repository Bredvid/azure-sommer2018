# Intro til Azure - sommer 2018

## Azure Functions

### Opprette og utvikle lokalt

Trenger:

* Azure CLI
    * `scoop install azure-cli`
* Azure Functions Core Tools v2 (beta)
    * `npm i -g azure-functions-core-tools@core --unsafe-perm true`
* (test: åpne PowerShell og sjekk at følgende kommandoer er tilgjengelig: `az` og `func`)

```powershell
func init --worker-runtime node # Initialisere functions-prosjekt. Bruk `--no-source-control` hvis man **IKKE* vil ha initialisert en lokal Git-repo.
func start # Teste at prosjektet er ok. Firewall vil spørre om tilgang første gang denne kjøres.
func new --language javascript --name HelloWorld --template 'HTTP Trigger' # Opprette en funksjon
func start # Observer at ny funksjon ble funnet av runtime
```

### Opprette ressurser i Azure

```powershell
az login # Logge på ved å følge instruksjonene. Bruk Bredvid-login
az account set -s b5de530a-6a76-4cc3-8ea2-98a0d857cccf # Sette Azure subscription
az group create -n sommer2018_rg --location westeurope
az configure --defaults group=sommer2018_rg location=westeurope
az storage account create -n sommer2018storage --sku Standard_LRS
az functionapp create --name sommerhit2018 -l -c westeurope -s sommer2018storage # Ta vare på Git URL til repository-et
```

### Produksjonssette til Azure

Finn brukernavn og passord for remote Git:

```powershell
az functionapp deployment list-publishing-profiles -n sommerhit2018
```

Klipp og lim remote URL på formatet: `http://<brukernavn>:<passord>@sommerhit2018.scm.azurewebsites.net/sommerhit2018.git`

Sett en remote i Git og pushe kode til Azure:

```powershell
git remote add azure <url fra forrige steg>
git push -u azure master
```

## Web application - ASP.NET Core 2.1

Trenger:

* Dotnet SDK
    * `scoop install dotnet-sdk`
    * Eller: [.NET Downloads](https://www.microsoft.com/net/download/windows)
* Visual Studio Code
    * `scoop install vscode`
    * Eller: [Visual Studio Code](https://code.visualstudio.com/)
* (test: åpne PowerShell og sjekkt at følgende kommandoer er tilgjengelig: `dotnet` og `code`)

