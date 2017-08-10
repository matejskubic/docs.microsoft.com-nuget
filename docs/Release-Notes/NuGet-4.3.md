---
# required metadata

title: NuGet 4.0 RTM Release Notes | Microsoft Docs
author: karann
ms.author: karann
manager: unnir
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
#ms.service:
ms.technology: null
ms.assetid: 906cc4dd-7948-4e86-a093-21df830ce8c3

# optional metadata

description: Release notes for NuGet 4.3 RTM including known issues, bug fixes, added features, and DCRs.
keywords: NuGet 4.3 RTM release notes, bug fixes, known issues, added features, DCRs
#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer:
- karann
- unnir
#ms.suite:
#ms.tgt_pltfrm:
#ms.custom:

---

# 4.3 RTM Release Notes

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, has a bunch of quality fixes and improves performance. This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.

## Known issues

### NuGet restore may treat disabled package sources as enabled in some cases

#### Issue:
The following restore command line techniques will treat disabled packages sources as enabled. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
1) msbuild /t:restore
2) dotnet restore (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)

#### Workaround:
1) Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)
2) Delete your disabled source and continue to use msbuild or dotnet.exe.
3) For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.


### NuGet restore may fail when you have multiple projects referencing another project in a solution

#### Issue:
NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### Workaround:
Fix the casings or relative paths to be the same for all project references.

## Issues fixed in NuGet 4.3 RTM timeframe

**Bug:**

* msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)

* dotnet Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)

* Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)

* netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

* RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)

* If your solution has projectreferences that refer to the same project, with different casing, restore may not work. This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)

* Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)

* NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)

* Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)

* Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)

* Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

**DCR:**

* Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)

* TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)

* Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)

* NuGet restore is selecting compile assets from runtime section. - [#4207](https://github.com/NuGet/Home/issues/4207)

* Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)

**Docs:**

* MSBuild restore and NuGet.config - [#5043](https://github.com/NuGet/Home/issues/5043)

* AutoReferenced docs and fwlink - [#4470](https://github.com/NuGet/Home/issues/4470)

**Feature:**

* NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)

* NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)

* NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)

* Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)

* NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)

* Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

* Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)

## Links to GitHub issues fixed in RTM

[Issues List](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")