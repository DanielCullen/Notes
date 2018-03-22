# Notes

<br/>

This repository defined utilities for `ETMall` projects, and reference through `NuGet` packages.

If you are finding the way to deploy new features, check [Quick Start](/home#user-content-quick-start) section.

<br/><br/>

# Quick Start


### Managing The `.nuspec` File

This section describes how you update your `.nuspec` for quick fix/update, [additional dependencies work](/home#user-content-dependencies) is required if necessary.

<br/><br/>

#### Package Version

This section is same as [specification describing](/home#user-content-package-version-1).

```diff
    <!-- The package version number that is used when resolving dependencies -->
-   <version>1.0.0</version>
+   <version>1.1.0</version>
```
<br/>
#### Release Notes

This section is same as [specification describing](/home#user-content-release-notes-1).

```diff
    <!-- Any details about this particular release -->
-   <releaseNotes>The very first pack.</releaseNotes>
+   <releaseNotes>Fix the issue that html closing tag doesn't generate correctly.</releaseNotes>
```

<br/><br/>

### Versioning Assembly

This section makes the version of `.dll` shows correctly.
<br/>
#### .NET Framework
`YourLovelyProject.Properties.AssemblyInfo.cs`
``` diff
using System.Reflection;
using System.Runtime.CompilerServices;
using System.Runtime.InteropServices;

// General Information about an assembly is controlled through the following
// set of attributes. Change these attribute values to modify the information
// associated with an assembly.
[assembly: AssemblyTitle("ETMall.Common.Utility")]
[assembly: AssemblyDescription("")]
[assembly: AssemblyConfiguration("")]
[assembly: AssemblyCompany("")]
[assembly: AssemblyProduct("ETMall.Common.Utility")]
[assembly: AssemblyCopyright("Copyright ©  2018")]
[assembly: AssemblyTrademark("")]
[assembly: AssemblyCulture("")]

// Setting ComVisible to false makes the types in this assembly not visible
// to COM components.  If you need to access a type in this assembly from
// COM, set the ComVisible attribute to true on that type.
[assembly: ComVisible(false)]

// The following GUID is for the ID of the typelib if this project is exposed to COM
[assembly: Guid("7f9d8b00-3c42-4b8f-b396-4fc9220f0452")]

// Version information for an assembly consists of the following four values:
//
//      Major Version
//      Minor Version
//      Build Number
//      Revision
//
// You can specify all the values or you can default the Revision and Build Numbers
// by using the '*' as shown below:
- [assembly: AssemblyVersion("1.0.0.0")]
+ [assembly: AssemblyVersion("1.1.0.0")]
- [assembly: AssemblyFileVersion("1.0.0.0")]
+ [assembly: AssemblyFileVersion("1.1.0.0")]
```
<br/><br/>
### Publish
<br/>
#### Pack

```
./nuget.exe pack <someSpecification.nuspec> -OutputDirectory '<pathToStorePackage>'
```
<br/>

#### Deploy

```
./nuget.exe push <specification.nupkg> <apiKey|secret> -source <privateNuGetServer>
```
The `NuGet` server we currently hosting on *http://nuget01.etzone.net*, `ApiKey` can also been found in it's configuration file.

<br/><br/>
# Specification Describing
<br/>
The first section of each title is managing via `.nuspec`, and the other one for `.csproj` with `.NET Core`.
<br/>
### Identifier

Basically same as namespace but must to be unique for whole `NuGet.private` or `Nuget.org`.The great pattern is to use your company name as the first part of the identifier like `ETMall.Awesome.Core`.

##### nuspec
```
    <!-- The identifier that must be unique within the hosting gallery -->
    <id>ETMall.Common.DataAccess</id>

```

##### csproj
```
   <PackageId>ETMall.Common.DataAccess</PackageId>
```


### Tags

Basically for searching, split them with space.

##### nuspec
```diff
    <!-- Tags appear in the gallery and can be used for tag searches -->
-   <tags>etmall common dataaccess dblayer redis sqlserver</tags>
+   <tags>etmall common dataaccess dblayer redis sqlserver oracle</tags>
```

##### csproj
```diff
-   <PackageTags>etmall common dataaccess dblayer redis sqlserver</PackageTags>
+   <PackageTags>etmall common dataaccess dblayer redis sqlserver oracle</PackageTags>
```

![spinning](/uploads/c4dc14250fa9f8e776f9422cb2a68805/spinning.PNG)

<br/><br/>

### Package Version

##### nuspec
```diff
    <!-- The package version number that is used when resolving dependencies -->
-   <version>1.0.0</version>
+   <version>1.1.0</version>
```
also see [Assembly](/home#versioning-assembly).
##### csproj
```diff
    <!-- The package version number that is used when resolving dependencies -->
-   <Version>1.0.0</Version>
+   <Version>1.1.0</Version>
    <!-- This section makes the version of .dll shows correctly. -->
-   <AssemblyVersion>1.0.0.0</AssemblyVersion>
-   <FileVersion>1.0.0.0</FileVersion>
+   <AssemblyVersion>1.1.0.0</AssemblyVersion>
+   <FileVersion>1.1.0.0</FileVersion>
```

<br/><br/>
### Release Notes

##### nuspec
```diff
    <!-- Any details about this particular release -->
-   <releaseNotes>The very first pack.</releaseNotes>
+   <releaseNotes>Fix the issue that html closing tag doesn't generate correctly.</releaseNotes>
```
##### csproj

```diff
    <!-- The package version number that is used when resolving dependencies -->
-   <PackageReleaseNotes>The very first pack.</PackageReleaseNotes>
+   <PackageReleaseNotes>Fix the issue that html closing tag doesn't generate correctly.</PackageReleaseNotes>
```
<br/><br/>
### Dependencies

Describing lowest dependency in this section.
##### nuspec
```diff
    <!-- Dependencies are automatically installed when the package is installed-->
    <dependencies>
      <dependency id="ETMall.Common.Utility" version="1.1.2"  />
      <dependency id="Oracle.DataAccess.x86" version="2.112.1.0" />
      <dependency id="StackExchange.Redis" version="1.0.488"  />
-     <dependency id="Dapper" version="1.42" />
+     <dependency id="Dapper" version="1.50.4" />
    </dependencies>
```

##### csproj


```diff
  <ItemGroup>
    <PackageReference Include="ETMall.Common.Utility" Version="1.1.2" />
    <PackageReference Include="Oracle.DataAccess.x86" Version="2.112.1.0" />
    <PackageReference Include="StackExchange.Redis" Version="1.0.488" />
-   <PackageReference Include="Dapper" Version="1.42" />
+   <PackageReference Include="Dapper" Version="1.50.4" />
  </ItemGroup>
```
<br/><br/>
#### Managing Dependencies

##### Syntax
*  Describing dependencies with a specified range. [MSDN](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#version-ranges-and-wildcards) for more information.

| Notation | Applied rule | Description |
|----------|--------------|-------------|
| 1.0 | 1.0 ≥ x | Minimum version, inclusive |
| (1.0,) | 1.0 > x | Minimum version, exclusive |
| [1.0] | x == 1.0 | Exact version match |
| (,1.0] | x ≤ 1.0 | Maximum version, inclusive |
| (,1.0) | x < 1.0 | Maximum version, exclusive |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | Exact range, inclusive |
| (1.0,2.0) | 1.0 < x < 2.0 | Exact range, exclusive |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | Mixed inclusive minimum and exclusive maximum version |
| (1.0)    | invalid | invalid |

##### How NuGet resolves package dependencies.
<br/>
###### Lowest applicable version
   ![image](/uploads/9a9f58227a04071bead916787aa3f538/image.png)
   ![image](/uploads/bbdf5c7b85713af0b1ea6eac57c680c6/image.png)

<br/>

###### Nearest

![image](/uploads/1e9d37c307080e9443ac9d1a83184daa/image.png)

###### Cousin dependencies

![image](/uploads/7e01ac532a0ae959a6e849ee485fb0d1/image.png)

![image](/uploads/97772a8a8c6a18adbf699ec29e9c6e46/image.png)

<br/>

More specification via `.csproj` see also [supported element](https://docs.microsoft.com/en-us/dotnet/core/tools/csproj).
<br/><br/>

### Files included

Listed file would be included in package.

```diff
  <files>
+   <file src="bin\Release\ETMall.Common.Utility.dll" target="lib" />
+   <file src="bin\Release\README.md" target="lib" />
  </files>
```
<br/>
# Q & A
<br/>
### 1. The Trick?

>>>
Technically speaking, a `NuGet` package is just a `ZIP` file that's been renamed with the `.nupkg` extension and whose contents match certain conventions. 
>>>

If there has any problem using `NuGet CLI` or `.NET Core CLI`(neither of them available on `CICD` etc.), you can just `ZIP` them as `.nupkg`.
<br/><br/>

### 2. How To Decide Dependencies?

~~In my opinion, just make sure feature works.~~

Prevent duplication inherited tree.

<br/><br/>
### 3. "Move it into a framework-specific folder. If this assembly is targeted for multiple frameworks, ignore this warning." keeps annoying me !!!

*  The easiest way is to modified both `<OutputPath>` and `<Files>` elements.
<br/>

#### OutputPath in .csproj
```diff
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
    <DebugType>pdbonly</DebugType>
    <Optimize>true</Optimize>
-   <OutputPath>bin\Release</OutputPath>
    <!--                      Or simply sets to net452 etc.--!>
+   <OutputPath>bin\Release\$(TargetFrameworkVersion)</OutputPath>
    <DefineConstants>TRACE</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
    <DocumentationFile>
    </DocumentationFile>
  </PropertyGroup>
```

#### Files in `.nuspec`

```diff
  <files>
-   <file src="bin\Release\README.md" target="lib"/>
-   <file src="bin\Release\ETMall.Common.Utility.dll" target="lib" />
+   <file src="lib\**" target="lib/net452"/>
  </files>
```


*  [Migrating to .NET Standard Library](/migrating-to-.net-standard-library.) is recommended. 












