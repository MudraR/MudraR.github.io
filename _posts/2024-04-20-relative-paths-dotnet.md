---
layout: post
title:  ".NET Methods Don't Expand Paths"
date: 2024-04-19 15:23 -0500
tags: [powershell, dotnet]
---

Relative paths are interpreted differently in .NET methods than in PowerShell.

## Problem
I encountered an error when working with the .NET namespace `System.Security.Cryptography.X509Certificates`. Despite being in the directory where the certificate file was located, the system could not find the file and threw an exception.

![relative-path-exception](/assets/img/2024-04-20-dotnet-methods-path/relative-path-exception.png)

While PowerShell automatically resolves relative paths based on the current directory, .NET methods do not. In .NET, when you provide a relative path, it is interpreted relative to the current working directory of the _application process_, **not** necessarily the location of the script/executable.

## Resolution
I resolved it by calling the class using the expanded full path of the certificate. 

```PowerShell
[Security.Cryptography.X509Certificates.X509Certificate2]::New([System.IO.Path]::GetFullPath((Join-Path (Get-Location) $Certificate)))
```

![expanded-path](/assets/img/2024-04-20-dotnet-methods-path/expanded-path.png)

By using `System.IO.Path.GetFullPath`, I was able to provide the full path of the certificate file to the .NET method, which successfully loaded the certificate. 


## References

- [System.IO.Path.GetFullPath Method](https://docs.microsoft.com/en-us/dotnet/api/system.io.path.getfullpath?view=net-6.0)
- [X509Certificate2 Constructor](https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.x509certificates.x509certificate2.-ctor?view=net-6.0)
- [Join-Path](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/join-path?view=powershell-7.1)
