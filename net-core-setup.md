---
id: 160430
title: How to do .Net core setup for tests
date: 2017-10-08T15:07:40+01:00
author: terje
layout: page
guid: http://hermit.no/?page_id=160430
catchevolution-sidebarlayout:
  - default
---
This is a short recipe for how to set up your project for testing .net core.

Test projects needs to target a platform, see the <a href="https://www.microsoft.com/net/targeting" target="_blank" rel="noopener noreferrer">different possible platforms,</a> and possible <a href="https://docs.microsoft.com/en-us/dotnet/standard/net-standard" target="_blank" rel="noopener noreferrer">settings for frameworks and platforms</a>.  The latter link show settings that can be applied to both the csproj file and the c# files.

A possible platform is .Net Core 2.2

Download .Net core 2.2.5 from <a href="https://github.com/dotnet/core/blob/master/release-notes/download-archives/2.0.0-download.md" target="_blank" rel="noopener noreferrer">here</a>

Add nuget package Microsoft.Net.Test.Sdk to your project

A possible csproj file can look like:

<pre>&lt;Project Sdk="Microsoft.NET.Sdk"&gt;

&lt;PropertyGroup&gt;
  &lt;TargetFramework&gt;netcoreapp2.2&lt;/TargetFramework&gt; 
  &lt;LangVersion&gt;latest&lt;/LangVersion&gt;
&lt;/PropertyGroup&gt; 

&lt;ItemGroup&gt; 
   &lt;PackageReference Include="Microsoft.NET.Test.Sdk" Version="16.3.0" /&gt; 
   &lt;PackageReference Include="NUnit" Version="3.12.0" /&gt; 
   &lt;PackageReference Include="NUnit3TestAdapter" Version="3.15.1" /&gt; &lt;/ItemGroup&gt;

&lt;/Project&gt;</pre>

Also see Rob Prousse <a href="http://www.alteridem.net/2017/05/04/test-net-core-nunit-vs2017/" target="_blank" rel="noopener noreferrer">blogpost </a>on testing .net core, and  <a href="https://github.com/nunit/docs/wiki/.NET-Core-and-.NET-Standard" target="_blank" rel="noopener noreferrer">NUnit docs</a>  for more details.

<h2>Traps:</h2>

<ul>
    <li>Trying to use .Net Standard as target for your tests.  This will not work.  You need a platform target for your test projects.
<ul>
    <li>Even if your test projects targets .net core, your production code, the code under test, can still be .net standard</li>
</ul>
</li>
    <li>Trying to use a Vsix test adapter to test .net core.  This will not work.  You need to use the <a href="https://www.nuget.org/packages/NUnit3TestAdapter/" target="_blank" rel="noopener noreferrer">nuget test adapter</a>., and the version must be <strong>3.8.0</strong> or higher.</li>
    <li>Forgetting to add the <a href="https://www.nuget.org/packages/Microsoft.NET.Test.Sdk/" target="_blank" rel="noopener noreferrer">Microsoft.Net.Test.Sdk</a> package. This does not come with the adapter, even if that might be a good idea, and might happen later on, but right now it needs to be added manually.</li>
    <li>Forgetting to restart Visual Studio after adding an adapter.</li>
    <li>Updating older projects and forgetting to update <a href="https://www.nuget.org/packages/Microsoft.NET.Test.Sdk/" target="_blank" rel="noopener noreferrer">Microsoft.Net.Test.Sdk</a> to the latest version,  see <a href="http://captainclueless.blogg.no/1507716395_bitten_twice_dont_remember_dont_learn_read_to_avoid_or_eat_caramel_pudding.html" target="_blank" rel="noopener noreferrer">details here.</a></li>
</ul>