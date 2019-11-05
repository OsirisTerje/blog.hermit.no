---
id: 160603
title: How to get some output from dotnet test
date: 2019-02-15T11:24:12+01:00
author: terje
layout: page
guid: http://hermit.no/?page_id=160603
catchevolution-sidebarlayout:
  - default
---
Running <code>dotnet test</code> will not show you any output, not from your test code and not from the adapter/engine. 

It runs by default in <strong>quiet mode</strong>. 

To get output from the adapter, run it in normal mode,  by setting the verbose option to normal

<code>-v n</code>

You still wont get anything out from your test code though. 

See https://github.com/Microsoft/vstest/issues/799
