# Tenekon.MSBuild.Packaging.ProjectBuildInPackage [![Nuget](https://img.shields.io/nuget/v/Tenekon.MSBuild.Packaging.ProjectBuildInPackage)](https://www.nuget.org/packages/Tenekon.MSBuild.Packaging.ProjectBuildInPackage)

_Allow project reference content to be added to the NuGet-package during pack process._

> Was in the past part of the [Teronis.DotNet code base](https://github.com/teneko/Teronis.DotNet/tree/develop/src/MSBuild/Packaging/ProjectBuildInPackage) but _Tenekon.MSBuild.Packaging.ProjectBuildInPackage_ deserves its own repository.

> Was recently named `Teronis.MSBuild.Packaging.ProjectBuildInPackage`.

## Installation

Package Managaer

```
Install-Package Tenekon.MSBuild.Packaging.ProjectBuildInPackage -Version <type here version>
```

.NET CLI

```
dotnet add package Tenekon.MSBuild.Packaging.ProjectBuildInPackage --version <type here version>
```

## Settings

### Disable welcome message

```
<PropertyGroup>
  <NoProjectBuildInPackageWelcome>false</NoProjectBuildInPackageWelcome>
</PropertyGroup>
```

### Modify verbosity

```
</PropertyGroup>
  <!-- You can choose between detailed or d, normal or n and false to disable verbosity. -->
  <ProjectBuildInPackageVerbosity>normal</ProjectBuildInPackageVerbosity>
</PropertyGroup>
```

## Usage

1\. Specify ```PrivateAssets="all"``` to those `<ProjectReference ... />`s whose build artefacts you want to have to be included into the package.
<br/>2\. Pack your project.

## Example:

### Before

```
<PropertyGroup>
  <TargetFrameworks>netstandard2.0;netcoreapp3.1;net5.0</TargetFrameworks>
  <AssemblyName>Tenekon.NetStandard.Core</AssemblyName>
</PropertyGroup>
<ItemGroup>
  <ProjectReference Include="..\..\Core.Localization\src\Tenekon.NetStandard.Core.Localization.csproj" />
</ItemGroup>
```

### After

```
<PropertyGroup>
  <TargetFrameworks>netstandard2.0;netcoreapp3.1;net5.0</TargetFrameworks>
  <AssemblyName>Tenekon.NetStandard.Core</AssemblyName>
</PropertyGroup>
<ItemGroup>
  <ProjectReference Include="..\..\Core.Localization\src\Tenekon.NetStandard.Core.Localization.csproj" PrivateAssets="all" />
</ItemGroup>
```

## Verification

There are three ways to verify that it worked:

1\. Look at the console output and seek out for something like this:

```
3>Target _WalkEachTargetPerFramework:
3>  Target CopyProjectBuildInPackage:
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Thanks for using my package. <3
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\Tenekon.NetStandard.Core.Localization.dll (local) to .\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\Tenekon.NetStandard.Core.Localization.pdb (local) to .\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\Tenekon.NetStandard.Core.Localization.xml (local) to .\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\de-DE\Tenekon.NetStandard.Core.Localization.resources.dll (local) to .\de-DE\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\en-US\Tenekon.NetStandard.Core.Localization.resources.dll (local) to .\en-US\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\nl-NL\Tenekon.NetStandard.Core.Localization.resources.dll (local) to .\nl-NL\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] 6 local files have been copied to package. (TargetFramework=net5.0)
3>  Target CopyProjectBuildInPackage:
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Thanks for using my package. <3
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\Tenekon.NetStandard.Core.Localization.dll (local) to .\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\Tenekon.NetStandard.Core.Localization.pdb (local) to .\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\Tenekon.NetStandard.Core.Localization.xml (local) to .\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\de-DE\Tenekon.NetStandard.Core.Localization.resources.dll (local) to .\de-DE\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\en-US\Tenekon.NetStandard.Core.Localization.resources.dll (local) to .\en-US\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\nl-NL\Tenekon.NetStandard.Core.Localization.resources.dll (local) to .\nl-NL\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] 6 local files have been copied to package. (TargetFramework=netcoreapp3.1)
3>  Target CopyProjectBuildInPackage:
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Thanks for using my package. <3
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\Tenekon.NetStandard.Core.Localization.dll (local) to .\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\Tenekon.NetStandard.Core.Localization.pdb (local) to .\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\Tenekon.NetStandard.Core.Localization.xml (local) to .\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\de-DE\Tenekon.NetStandard.Core.Localization.resources.dll (local) to .\de-DE\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\en-US\Tenekon.NetStandard.Core.Localization.resources.dll (local) to .\en-US\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] Copy ..\..\Core.Localization\src\bin\Debug\netstandard2.0\nl-NL\Tenekon.NetStandard.Core.Localization.resources.dll (local) to .\nl-NL\ (package)
3>    [Tenekon.MSBuild.Packaging.ProjectBuildInPackage] 6 local files have been copied to package. (TargetFramework=netstandard2.0)
```

This indicates that in each framework in project `Tenekon.NetStandard.Core` the framework specific files from project `Tenekon.NetStandard.Core.Localization` has been added to package.

2\. Unzip the `.nupkg` and look inside the `*.nuspec`-file

It should look like this:

```
<dependencies>
  <group targetFramework=".NETCoreApp3.1">
    <dependency id="Microsoft.Bcl.HashCode" version="1.1.1" exclude="Build,Analyzers" />
    <dependency id="Microsoft.CSharp" version="4.7.0" exclude="Build,Analyzers" />
    <dependency id="Microsoft.Extensions.Logging.Abstractions" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="MorseCode.ITask" version="2.0.3" exclude="Build,Analyzers" />
    <dependency id="System.Configuration.ConfigurationManager" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="System.Interactive.Async" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="System.Management" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="System.Text.Json" version="5.0.1" exclude="Build,Analyzers" />
    <dependency id="System.Threading.Tasks.Dataflow" version="5.0.0" exclude="Build,Analyzers" />
  </group>
  <group targetFramework="net5.0">
    <dependency id="Microsoft.Bcl.HashCode" version="1.1.1" exclude="Build,Analyzers" />
    <dependency id="Microsoft.CSharp" version="4.7.0" exclude="Build,Analyzers" />
    <dependency id="Microsoft.Extensions.Logging.Abstractions" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="MorseCode.ITask" version="2.0.3" exclude="Build,Analyzers" />
    <dependency id="System.Configuration.ConfigurationManager" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="System.Interactive.Async" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="System.Management" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="System.Text.Json" version="5.0.1" exclude="Build,Analyzers" />
    <dependency id="System.Threading.Tasks.Dataflow" version="5.0.0" exclude="Build,Analyzers" />
  </group>
  <group targetFramework=".NETStandard2.0">
    <dependency id="Tenekon.Nullable" version="0.1.8-alpha.202" exclude="Build,Analyzers" />
    <dependency id="Microsoft.Bcl.HashCode" version="1.1.1" exclude="Build,Analyzers" />
    <dependency id="Microsoft.CSharp" version="4.7.0" exclude="Build,Analyzers" />
    <dependency id="Microsoft.Extensions.Logging.Abstractions" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="MorseCode.ITask" version="2.0.3" exclude="Build,Analyzers" />
    <dependency id="System.Configuration.ConfigurationManager" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="System.Interactive.Async" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="System.Management" version="5.0.0" exclude="Build,Analyzers" />
    <dependency id="System.Text.Json" version="5.0.1" exclude="Build,Analyzers" />
    <dependency id="System.Threading.Tasks.Dataflow" version="5.0.0" exclude="Build,Analyzers" />
  </group>
</dependencies>
```

There **should no entry listed** that looks like:

```
<dependency id="Tenekon.NetStandard.Core.Localization" version="0.1.8-alpha.202" exclude="Build,Analyzers" />
```

3\. Unzip the `.nupkg` and look inside `lib/<target-framework>/` whether `Tenekon.NetStandard.Core.Localization.(dll|pdb|xml)` is present.

## Frequent questions

**Question**
<br/>Why NuGet package does not include all dependencies when packing?

**Answer**
<br/>Let's first assume the following:

```
<!-- Project A -->
<ItemGroup>
  <PackageReference Include="SomePackage" Version="*" />
</ItemGroup>

<!-- Project B -->
<ItemGroup>
  <ProjectReference Include="ProjectA" PrivateAssets="all">
  <!--<PackageReference Include="Tenekon.MSBuild.Packaging.ProjectBuildInPackage" Version="0.1.7" />-->
</ItemGroup>
```

You are telling NuGet that you don't want to have Project A to be picked  up as NuGet-dependency. This is implicit, you don't have control about that. **The down-side is** the assmeblies of Project A, but not the assemblies of the packages of Project A, are not present in package of Project B.

By removing `PrivateAssets="all"` you disable the implicit behaviour of NuGet and the Project A will be picked up as NuGet dependency and EACH non-dependency package (also called transitive package).

Now let's asumme this:

```
<!-- Project A -->
<ItemGroup>
  <PackageReference Include="SomePackage" Version="*" />
</ItemGroup>

<!-- Project B -->
<ItemGroup>
  <ProjectReference Include="ProjectA" PrivateAssets="all">
  <PackageReference Include="Tenekon.MSBuild.Packaging.ProjectBuildInPackage" Version="0.1.7" />
</ItemGroup>
```

By having installed my package I assist in the implicit behaviour of NuGet: By not picking up Project A as NuGet-dependency copy over the direct assemblies produced by Project A to the bin-folder of Project B. **This has the following drawback:**

Because of the implicit behaviour and the usage of my package you have assemblies of Project A in Project B that are in need of the assemblies provided by packages (in your example "Some Package") you referenced in Project A. So a workaround is to add the packages from Project A in Project B explicitly as shown here:

```
<!-- Project A -->
<ItemGroup>
  <PackageReference Include="SomePackage" Version="*" />
</ItemGroup>

<!-- Project B -->
<ItemGroup>
  <ProjectReference Include="ProjectA" PrivateAssets="all">
  <PackageReference Include="Tenekon.MSBuild.Packaging.ProjectBuildInPackage" Version="0.1.7" />
  <!-- Use the SAME version like in Project A. -->
  <PackageReference Include="SomePackage" Version="*" />
</ItemGroup>
```
