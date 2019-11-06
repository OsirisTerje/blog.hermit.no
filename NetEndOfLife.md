# Beware of the end-of-life for .net framework and .net core versions

There are multiple versions of .Net Framework, and also of .Net Core.  Many of the versions have now reached their end of life point.   That means the versions are no longer supported, not with bug fixes and not with security fixes either.  

Some version are in the LTS (Long Term Support) mode.  This means they will receive critical fixes, and compatible fixes for a period of 3 years.  Microsoft also states that every second release will be set up for LTS.

Looking at how this is for .Net Core, the following screen shot is from the [.Net Core LifeCycle](https://dotnet.microsoft.com/download/dotnet-core) per Nov 6th 2019.

![](images/2019-11-06_17-10-12.jpg)

The [.Net Core Support Policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) describes in more details how this works, also what release cadence they have right now.

And a similar list for the [.Net Framework lifecycle](https://dotnet.microsoft.com/download/dotnet-framework)

![](images/2019-11-06_20-56-00.jpg)

As can be seen here the .net 4.0 to .net 4.5.1 is at end of life. If you got anything here, it is really time to upgrade.


## Supported OS lifecycles

Your chosen .net framework or .net core version will run on an operating system, and the different versions support different version of the available operating system.  Microsoft will handle only OS support for their own operating system. When you try to figure out where it all ends, you need to work through this dependency chain of lifecycle support.  It is pretty obvious that the earlier versions you try to support, the harder it will be.

The [.Net Core Supported OS Policy](https://github.com/dotnet/core/blob/master/os-lifecycle-policy.md) covers what operating systems are supported by the different versions of .Net Core.  It has links to the underlying operating sysyems supports.  E.g. the .Net Core 3.0 are supported by [these operating systems](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md).  


## Links

[Download start page for all .net core and .net frameworks](https://dotnet.microsoft.com/download)

[Microsoft Lifecycle Policy FAQ](https://support.microsoft.com/en-us/help/17140)

[.NET Core Support Policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)

