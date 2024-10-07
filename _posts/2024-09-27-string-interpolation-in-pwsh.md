---
layout: post
title: Understanding String Interpolation with HTTP Response Objects in PowerShell
date: 2024-09-27 00:55 -0500
---

So I was writing a script to check healthchecks in powershell. I wanted to output the full response (with headers and content) along with the status code. PowerShell is really nice and gives you the entire object in the response.

Let's take a look at an example where we send a request to Google:

```powershell
PS > $response = Invoke-WebRequest -Uri "https://google.com"
PS > echo $response

StatusCode        : 200
StatusDescription : OK
Content           : <!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="en"><head><meta content="Search the world's information, including
                    webpages, images, videos and more. Google has many speci…
RawContent        : HTTP/1.1 200 OK
                    Date: Fri, 27 Sep 2024 06:03:28 GMT
                    Cache-Control: max-age=0, private
                    Content-Security-Policy-Report-Only: object-src 'none';base-uri 'self';script-src 'nonce-rMAMd_qNc3_WNXq0-Tl0Wg…
Headers           : {[Date, System.String[]], [Cache-Control, System.String[]], [Content-Security-Policy-Report-Only, System.String[]], [Accept-CH, System.String[]]…}
Images            : {@{outerHTML=<img alt="Google" height="92" src="/images/branding/googlelogo/1x/googlelogo_white_background_color_272x92dp.png" style="padding:28px 0
                    14px" width="272" id="hplogo">; tagName=IMG; alt=Google; height=92; src=/images/branding/googlelogo/1x/googlelogo_white_background_color_272x92dp.png;
                    style=padding:28px 0 14px; width=272; id=hplogo}}
InputFields       : {@{outerHTML=<input value="en" name="hl" type="hidden">; tagName=INPUT; value=en; name=hl; type=hidden}, @{outerHTML=<input name="source" type="hidden"
                    value="hp">; tagName=INPUT; name=source; type=hidden; value=hp}, @{outerHTML=<input name="biw" type="hidden">; tagName=INPUT; name=biw; type=hidden},
                    @{outerHTML=<input name="bih" type="hidden">; tagName=INPUT; name=bih; type=hidden}…}
Links             : {@{outerHTML=<a class="gbzt gbz0l gbp1" id=gb_1 href="https://www.google.com/webhp?tab=ww"><span class=gbtb2></span><span class=gbts>Search</span></a>;
                    tagName=A; class=gbzt gbz0l gbp1; id=gb_1; href=https://www.google.com/webhp?tab=ww}, @{outerHTML=<a class=gbzt id=gb_2
                    href="https://www.google.com/imghp?hl=en&tab=wi"><span class=gbtb2></span><span class=gbts>Images</span></a>; tagName=A; class=gbzt; id=gb_2;
                    href=https://www.google.com/imghp?hl=en&tab=wi}, @{outerHTML=<a class=gbzt id=gb_8 href="https://maps.google.com/maps?hl=en&tab=wl"><span
                    class=gbtb2></span><span class=gbts>Maps</span></a>; tagName=A; class=gbzt; id=gb_8; href=https://maps.google.com/maps?hl=en&tab=wl}, @{outerHTML=<a
                    class=gbzt id=gb_78 href="https://play.google.com/?hl=en&tab=w8"><span class=gbtb2></span><span class=gbts>Play</span></a>; tagName=A; class=gbzt;
                    id=gb_78; href=https://play.google.com/?hl=en&tab=w8}…}
RawContentLength  : 58558
RelationLink      : {}
```

The output includes the status code, headers, and content of the response.

But, what if you tried `write-output "$response"` (notice the quotes around `$response`)?

Interestingly, this outputs the Content field of the $response object, even though we didn't specify it. Why does placing quotes around the object result in displaying a string value?

The answer lies in how PowerShell handles string interpolation. When a variable is enclosed in quotes, PowerShell attempts to convert it to a string. So `echo "$response"` is really doing `echo $response.ToString()`

### What is String Interpolation?

Interpolation is the process of replacing placeholders in a string with the actual values of variables. In PowerShell, you can use double quotes to create an interpolated string, where variables are replaced with their values.

For example, consider the following code:

```powershell
$name = "John"
$age = 30

Write-Output "My name is $name and I am $age years old."
```

When you run this code, it will output:

```
My name is John and I am 30 years old.
```

In this example, the variables $name and $age are replaced with their values in the string "My name is $name and I am $age years old." This is interpolation in action.

### What happens when you interpolate a variable that contains an object?

When you interpolate a variable that contains an object, PowerShell will call the ToString() method on that object to convert it to a string. If the object does not have a ToString() method, PowerShell will use the default implementation provided by the System.Object class.

In the case of the $response object, it is an instance of the BasicHtmlWebResponseObject class, which inherits from the WebResponseObject class. The WebResponseObject class overrides the ToString() method to convert the content of the HTTP response to a string.

This is why when you interpolate the $response object in a string, you see the content of the HTTP response displayed.

https://github.com/PowerShell/PowerShell/blob/ba493b6f1af83c03f8480f4bd24afe29a4f13125/src/Microsoft.PowerShell.Commands.Utility/commands/utility/WebCmdlet/Common/WebResponseObject.Common.cs#L180
