# Steps

## Initialize git

```powershell
git init
```

## Initialize function app

```powershell
func init --no-source-control
```

## Create function

```powershell
func function new -n HelloWorldJS -t HttpTrigger -l JavaScript
```

## Start host

```powershell
func host start
```

## Send request

```powershell
Invoke-WebRequest http://localhost:7071/api/HelloWorldJS -Method Post -body '{"name":"Vidar"}'
```

## Debug in VSCode

```powershell
func host start --debug vscode
```

## Log in to azure

```powershell
az login
az account set --subscription b5de530a-6a76-4cc3-8ea2-98a0d857cccf
```

## Crate resource group

```powershell
az group create --name brimful-of-azure --location WestEurope
```

## Create storage account

```powershell
az storage account create --name brimful01 --location westeurope `
    --resource-group brimful-of-azure --sku Standard_LRS
```

## Create function app in Azure

```powershell
az functionapp create `
    --name vidarfuncs --storage-account brimful01 `
    --resource-group brimful-of-azure `
    --consumption-plan-location westeurope `
    --deployment-local-git
```

## Log in to portal

* Set deployment credentials

## Connect to Azure

```powershell
git add *
git commit -m "Initial commit"
git remote add azure <...>
git push
```

## Test function

* Postman
* Azure console

## Create Slack function 

```powershell
func function new -n Kudu2SlackJS -t HttpTrigger -l JavaScript
```

## Prepare to use npm

```powershell
npm init
npm add request --save
npm i
```

## Implement slack function

