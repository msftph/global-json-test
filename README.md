# Global Json Test

This repo tests global.json scoping to see if dotnet will stop evaulating global.json if it finds one somewhere in the folder hierarchy. 

There are two global.json files in this sample, one at the root of the repo and one in the project folder:

* [Repo Root](global.json) Targets net6.0
* [Project](GrandParent/global.json) Targets net8.0

The following sdks are installed:

```
PS> > dotnet --list-sdks
6.0.423 [C:\Program Files\dotnet\sdk]
8.0.205 [C:\Program Files\dotnet\sdk]
8.0.206 [C:\Program Files\dotnet\sdk]
```

Running dotnet build from the solution:

```
PS> dotnet build
MSBuild version 17.3.4+a400405ba for .NET
  Determining projects to restore...
C:\Program Files\dotnet\sdk\6.0.423\Sdks\Microsoft.NET.Sdk\targets\Microsoft.NET.TargetFrameworkInference.targets(144,5): e
rror NETSDK1045: The current .NET SDK does not support targeting .NET 8.0.  Either target .NET 6.0 or lower, or use a versi
on of the .NET SDK that supports .NET 8.0. [C:\Users\pahuber\source\github.com\msftph\global-json-test\GrandParent\GrandPar
ent.csproj]

Build FAILED.

C:\Program Files\dotnet\sdk\6.0.423\Sdks\Microsoft.NET.Sdk\targets\Microsoft.NET.TargetFrameworkInference.targets(144,5): e
rror NETSDK1045: The current .NET SDK does not support targeting .NET 8.0.  Either target .NET 6.0 or lower, or use a versi
on of the .NET SDK that supports .NET 8.0. [C:\Users\pahuber\source\github.com\msftph\global-json-test\GrandParent\GrandPar
ent.csproj]
    0 Warning(s)
    1 Error(s)

Time Elapsed 00:00:00.56
```

Running dotnet build from the project:

```
PS> dotnet build
MSBuild version 17.9.8+610b4d3b5 for .NET
  Determining projects to restore...
  Restored C:\Users\pahuber\source\github.com\msftph\global-json-test\GrandParent\GrandParent.csproj (in 87 ms).
  GrandParent -> C:\Users\pahuber\source\github.com\msftph\global-json-test\GrandParent\bin\Debug\net8.0\GrandParent.dll

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:04.00

Workload updates are available. Run `dotnet workload list` for more information.
```