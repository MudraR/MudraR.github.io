---
layout: post
title: Using ForEach() Method for Array Iteration
date: 2024-05-13 05:21 -0500
tags: [powershell, dotnet, github, copilot]
---

I learned about a nifty `ForEach()` powershell method when looping through an array. You can call it on a collection and pass a script block to it!

## Context: 
I was recently reading the new docs for GitHub copilot on how you can now use it in the CLI. GitHub launched the `gh copilot explain` and `gh copilot suggest` commands as part of the copilot extension in the GitHub CLI.

##  Example Problem: 
How can I get an explanation of all of the sql files in a folder? 

## Example Solution: 

```powershell
$files = @($(Get-ChildItem -Path .\ -r -Filter *.sql))
$files.foreach{gh copilot explain $(Get-Content $PSItem)}
```

## Refernces 
- [PowerShell Array ForEach](https://learn.microsoft.com/en-us/powershell/scripting/learn/deep-dives/everything-about-arrays?view=powershell-7.4#foreach-method)
- [GitHub Copilot CLI](https://docs.github.com/en/copilot/github-copilot-in-the-cli/using-github-copilot-in-the-cli)
- [Script Blocks](https://learn.microsoft.com/en-us/powershell/scripting/learn/deep-dives/everything-about-arrays?view=powershell-7.4#foreach-method)