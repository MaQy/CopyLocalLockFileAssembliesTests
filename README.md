# CopyLocalLockFileAssembliesTests
Tests to showcase how CopyLocalLockFileAssemblies property doesn't work in .NET 5 when there is a framework reference. There are two projects in this solution, `CopyLocalLockFileAssembliesWithFrameworkReference` and `CopyLocalLockFileAssembliesWithoutFrameworkReference`. Both are almost identical:

- Both are console applications.
- Both have two target frameworks, .NET 5 and .NET Core 3.1.
- Both have the parameter `CopyLocalLockFileAssemblies` set to true.
- Both reference the package `Microsoft.Extensions.Configuration` 5.0.0.

The only difference is that `CopyLocalLockFileAssembliesWithFrameworkReference` has a framework reference to `Microsoft.AspNetCore.App`. This assembly is already included in the ASP.NET Core framework and, for some reason, it is not copied to the output folder in .NET 5 but it is copied over in .NET Core 3.1. The strangest thing is that if the build is executed in the command line including the output parameter then the DLL is copied over:

`dotnet build CopyLocalLockFileAssembliesWithFrameworkReference\CopyLocalLockFileAssembliesWithFrameworkReference.csproj -o folderWithLibraries`

This repository was created just to showcase this issue so it can be troubleshooted by Microsoft.
