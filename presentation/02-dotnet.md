# Adding .NET Core functions

## Create function

```powershell
func function new --name HelloWorldCSharp --template HttpTrigger --language C#
type .\HelloWorldCSharp run.csx
type .\HelloWorldCSharp run.csx | clip
```

## Create .NET project

```powershell
dotnet new classlib
mv js.csproj Funcs.csproj
dotnet build
```

## Add Nuget packages

```powershell
dotnet add package Microsoft.AspNetCore.Mvc.Core
dotnet add package Microsoft.Azure.WebJobs --version 3.0.0-beta4
dotnet restore
dotnet build
```

## Copy files during build

Add to `Funcs.csproj`:

```xml
<ItemGroup>
    <None Update="host.json">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="HelloWorldCSharp\function.json">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="HelloWorldJS\function.json">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="HelloWorldJS\index.js">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="Kudu2SlackJS\function.json">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="Kudu2SlackJS\index.js">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </None>
    <None Update="local.settings.json">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
      <CopyToPublishDirectory>Never</CopyToPublishDirectory>
    </None>
  </ItemGroup>
```

## Change function.json

Add:

```json
{
  "scriptFile": "../Funcs.dll",
  "entryPoint": "Funcs.HttpTrigger.Run"
}
```

## Build and run

```powershell
dotnet build
func host start --script-root .\bin\debug\netstandard2.0\
```

## Call .NET function

```powershell
Invoke-webrequest http://localhost:7071/api/HelloWorldCSharp -method POST -Body '{"name":"Vidar"}'
```
