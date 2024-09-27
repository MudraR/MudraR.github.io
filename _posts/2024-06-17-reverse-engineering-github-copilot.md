---
layout: post
title: reverse-engineering-github-copilot
date: 2024-06-17 19:37 -0500
---

I use GitHub Copilot for free due to my .edu account. GitHub Copilot is an AI-powred programming tool that uses machine learning to provide suggestions as you code. It was developed by OpenAI, GitHub, and Microsoft using a model trained on billions of lines of public code.

At this time, GitHub Copilot is private and there is no public API. However, GitHub Copilot offers the GitHub copilot extension to various IDEs. To use the IDE, you have to OAuth into GitHub using the copilot extension.

The endpoint is `https://github.com/login/device/code` to generate an OAuth token.

The client header and body is

```powershell
    # Define necessary variables
        $headers = @{
            'accept' = 'application/json'
            'editor-version' = 'Neovim/0.10.0'
            'editor-plugin-version' = 'copilot.vim/1.36.0'
            'content-type' = 'application/json'
            'user-agent' = 'GithubCopilot/1.155.0'
            'accept-encoding' = 'gzip,deflate,br'
        }

        $body = @{
            'client_id' = 'Iv1.b507a08c87ecfe98'
            'scope' = 'read:user'
        } | ConvertTo-Json
```

Up until Jan 18, the https://copilot-proxy.githubusercontent.com/v1/engines/copilot-codex/completions endpoint was used to get suggestions. However, this endpoint was disabled and the new endpoint is https://copilot.github.com/v1/engines/codex/completions.

https://github.blog/changelog/2024-01-18-copilot-january-18th-update/
