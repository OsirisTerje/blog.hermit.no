---
id: 160604
title: How to get some output from dotnet test
date: 2019-02-15T11:33:29+01:00
author: terje
layout: revision
guid: http://hermit.no/160603-autosave-v1/
permalink: /160603-autosave-v1/
---
Running <code>dotnet test</code> will not show you any output, not from your test code and not from the adapter/engine. 

It runs by default in <strong>quiet mode</strong>. 

To get output from the adapter, run it in normal mode,  by setting the verbose option to normal

<code>-v n</code>

You still wont get anything out from your test code though. 

