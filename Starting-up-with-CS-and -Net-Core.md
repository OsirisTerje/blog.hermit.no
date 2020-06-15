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

Create a basic application, Add a folder Test and then there:

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

Create a new sibling folder to test (name it cons), and then run `dotnet new console` which gives you the basic Hello World example program.

You can also add yet another sibling folder MyLib, and then run `dotnet new classlib`.

*Notice, some of the classnames and namespaces are in lower case only.  In C# the convention is Pascal convention,  first letter Uppercase, the rest lower case.*

[More info on dotnet new](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-new)

Now change the name from Class1 to Math

Add a method like:

```
public double Add (double a, double b)
{
    return a + b;
}

```

The project is called mylib (as the file mylib.csproj).  You rename this to e.g. MyMath.csproj.

Now, go back to the root folder for these three projects and run:

```
dotnet new sln
```

It will create a file named after the folder you're in, in my case `examples.sln`

Assuming you have installed VS Community edition, start it up doing:

```
devenv examples.sln
```

It will be slower on startup than VS code, as expected - it is a bigger IDE, but after a while you'll see the Solution explorer to the right side, showing a single node named Solution (which is the last file you created)

Now from the context menu on that node, select Add/Existing projects, and located and add the three csproj files you have recently created. 

When finished, it should look like:

![](https://github.com/OsirisTerje/osiristerje.github.io/blob/master/images/sln-example.jpg)


Select the top level Build menu, and do Build solution

If you get any problems, open up the 3 csproj files (double click in sln).
Ensure the Cons and the Test have TargetFramework set to netcoreapp3.1 and the MyMath have the same set to netstandard2.1

*Do another build, and you should be fine..... perhaps a context menu Restore Nuget packages, if it is hard to get going.*

Now, click the Dependency node on Cons and select Add Project Reference. and then select the MyMath project.  Do the same for the Test project.

Now, take a look inside the csproj files and see that it has now added a ProjectReference node.  Now you know how it looks, and you can add these in the editor later, if you prefer that.

```
<ItemGroup>
    <ProjectReference Include="..\mylib\MyMath.csproj" />
  </ItemGroup>
```










