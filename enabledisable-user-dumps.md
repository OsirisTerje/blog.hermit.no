---
id: 160455
title: How to enable/disable user dumps
date: 2017-10-27T19:14:29+01:00
author: terje
layout: page
guid: http://hermit.no/?page_id=160455
catchevolution-sidebarlayout:
  - default
---
<h2>Downloads</h2>
See a faster way to do this using <a href="https://marketplace.visualstudio.com/items?itemName=OsirisTerje.IFix" target="_blank" rel="noopener">IFix</a> , read the <a href="http://hermit.no/managing-userdumps-using-ifix/" target="_blank" rel="noopener">blogpost here </a>

OR

<a href="https://github.com/KDISim/CrashDumps/releases/tag/1.0" target="_blank" rel="noopener">G</a>et the userdump registry files here: <a href="https://github.com/KDISim/CrashDumps/releases/tag/1.0" target="_blank" rel="noopener">Download here</a>
<h2>Description</h2>
If you have an application crashing on you, in particular one of your own design - and in production -  enabling user dumps allow you to grab the state of the application at the time of the crash.  This dump can be directly opened in Visual Studio, where you can see the modules loaded, and then starting a debug session you get the call stack, and threads running.    If you also have the corresponding pdb files you can go directly to - literally-  the source of the problem.

To get the dumps, you must enable local dumps on your machine - or the machine where the issue happens. You do this using by setting a registry key at:
<blockquote>
<pre>[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps]</pre>
</blockquote>
and you use two settings:

DumpType, a DWORD, where value= 2 is enable full dump, and 0 is disable.

DumpFolder, a string, where you can set the location where you want the dumps to be collected.

You can use the RegEdit program to set these, or use reg file scripts.

&nbsp;

I have made two reg files, which can be run directly from a command prompt, to enable and disable the local dumps.  The folder path is set to D:\CrashDumps, so if that is not suitable to you, you can change to whatever you like.  The files are text, and easily edited.

If you run the scripts directly they will prompt you, if you want it silently then:
<pre>regedit /s EnableDump.reg

regedit /s DisableDump.reg</pre>
Further there is a test program to verify that the crash dumps settings you have set actually works - if enabled, or not - if disabled.

Running the program, just called Crash, give you this sequence:

<a href="http://hermit.no/wp-content/uploads/2017/10/crash.jpg"><img class="alignnone wp-image-160456 size-full" src="http://hermit.no/wp-content/uploads/2017/10/crash.jpg" alt="" width="858" height="226" /></a>

and the following output:

<a href="http://hermit.no/wp-content/uploads/2017/10/crash2.jpg"><img class="alignnone wp-image-160457 size-full" src="http://hermit.no/wp-content/uploads/2017/10/crash2.jpg" alt="" width="681" height="68" /></a>

And if you then look in the given dumpfolder:

<a href="http://hermit.no/wp-content/uploads/2017/10/crash3.jpg"><img class="alignnone wp-image-160458 size-full" src="http://hermit.no/wp-content/uploads/2017/10/crash3.jpg" alt="" width="1147" height="90" /></a>

Grab the package from the github release download link at the top..
<h3>Links:</h3>
<a href="https://github.com/KDISim/CrashDumps" target="_blank" rel="noopener">Github project site</a>

<a href="https://msdn.microsoft.com/en-us/library/windows/desktop/bb787181%28v=vs.85%29.aspx" target="_blank" rel="noopener">MSDN post on User Dumps</a>

&nbsp;