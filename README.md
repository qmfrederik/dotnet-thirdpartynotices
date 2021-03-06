# dotnet-thirdpartynotices

[![NuGet](https://img.shields.io/nuget/v/dotnet-thirdpartynotices.svg)](https://www.nuget.org/packages/dotnet-thirdpartynotices/)

## Example of a generated file

![example](https://i.imgur.com/rsqwaWP.png)

## Installation

```
dotnet tool install -g dotnet-thirdpartynotices
```

## Get started

Go inside the project directory and run:

```
dotnet-thirdpartynotices
```

To change the name of the file that will be generated:

```
dotnet-thirdpartynotices --output-filename "third party notices.txt"
```

If your project is in a different directory:

```
dotnet-thirdpartynotices <project directory path>
dotnet-thirdpartynotices --output-filename "third party notices.txt" <project directory path>
```

## How it works

### 1. Resolve assemblies

It uses MSBuild to resolve assemblies that should land in the publish folder or release folder. 

For .NET Core projects this is done using `ComputeFilesToPublish` target. 

For traditional .NET Framework and .NET Standard projects this is done using `ResolveAssemblyReferences` target

### 2. Try to find license based on the information from .nuspec or FileVersionInfo

It tries to find `.nuspec` for those assemblies and attempts to crawl the license content either from licenseUrl or projectUrl. 

Crawling from projectUrl currently works only with github.com projectUrls

Crawling from licenseUrl works with github.com, opensource.org and anything with `text/plain` Content-Type.

If `.nuspec` cannot be found it tries to guess the license using `FileVersionInfo` and checking things like product name.

## Notice

This tool is still experimental and might not work with certain projects. There might be some crashes but hopefully they'll be fixed soon.
