# Starting up with C# and .Net Core

## Get the tools

### .Net core
Ensure you have the .net core sdk installed.

[Download and install it from here](https://dotnet.microsoft.com/download/dotnet-core/thank-you/sdk-3.1.301-windows-x64-installer)

The run the following command to ensure you got it all right:

```
dotnet

(then)

dotnet --list-sdks
```

The first should just show you itself.  The second lists the sdks you have installed with their version numbers.

### IDEs

You should at least have [Visual Studio Code](https://code.visualstudio.com/download)

Start it up and from the Extensions icon (on the left side, 5th down probably) add the following extensions:

* C#  (from Microsoft)
* GitLens

Optionally you can also install [Visual Studio (large IDE)](https://visualstudio.microsoft.com/downloads/) which is superb for debugging.  Can come in handy. Select Community Edition, which is free. 

## Basic c# .net core command line application

Create a basic application:

```
dotnet new nunit
```

This is a scaffolding operation for a unit test project, the code generated is the csproj project files, and then the UnitTest1.cs file which contains the unit test itself in C# code. 

You can build and run test tests simply by:

```
dotnet test
```

If you just wanted to build, without running the test, it is just

```
dotnet build
```

The start code by writing:

```
code .
```

(Notice the dot!)

And it will start up with the project in the editor.

The `dotnet new`  command has multiple templates to choose from.  Get a list by using the `dotnet new --list`

Create a new folder, and then run `dotnet new console` which gives you the basic Hello World example program.

You can also add another folder, and then run `dotnet new classlib`.

*Notice, some of the classnames and namespaces are in lower case only.  In C# the convention is Pascal convention,  first letter Uppercase, the rest lower case.*







