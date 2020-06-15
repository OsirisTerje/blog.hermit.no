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

Now change your program code in Program.cs to look like:

```csharp
using System;
using System.Linq;

namespace cons
{
    public class Program
    {
        static void Main(string[] args)
        {
            if (!args.Any())
            {
                Console.WriteLine("Math arg1 arg2");
                return;
            }

            if (args.Length != 2)
            {
                Console.WriteLine($"Math needs two arguments, just got {args.Length}");
                return;
            }

            var ok = double.TryParse(args[0], out double a);
            if (!ok)
            {
                Console.WriteLine($"First argument must be a float number, but was {args[0]}");
                return;
            }

            ok = double.TryParse(args[1], out double b);
            if (!ok)
            {
                Console.WriteLine($"Second argument must be a float number, but was {args[1]}");
                return;
            }

            var math = new MyLib.Math();
            var result = math.Add(a, b);
            Console.WriteLine($"Result is {result:F2}");
        }
    }
}

```

And you can try to run it doing :

```
dotnet run 45.5  45
Result is 90.50
```
or without arguments or whatever, to check the error handling.

Notice in the code the use of string interpolation, using the `$" {somevar}"` syntax.

Notice also the inclusion of the `System.Linq`, which gave you access to the Any method. 

And notice the use of the `var` keyword, which says that the variable should be anything inferred by what is on the right hand side.  So in this case the `result` will be a double, because the math.Add statement returns a double.

Now, the code is a bit duplicated, and the static Main is a bit big, so let us rearrange it a bit.

```
using System;
using System.Collections.Generic;
using System.Linq;

namespace cons
{
    public class Program
    {
        static void Main(string[] args)
        {
            var program = new Program(args);
            program.Run();
        }

        private readonly IReadOnlyCollection<string> arguments;

        public Program(IReadOnlyCollection<string> args)
        {
            arguments = args;
        }

        public void Run()
        {
            if (!arguments.Any())
            {
                Console.WriteLine("Math arg1 arg2");
                return;
            }

            if (arguments.Count != 2)
            {
                Console.WriteLine($"Math needs two arguments, just got {arguments.Count}");
                return;
            }

            var result1 = Parse(arguments.First(), "First");
            if (!result1.Ok)
                return;
            var result2 = Parse(arguments.Skip(1).First(), "Second");
            if (!result2.Ok)
                return;
            
            var math = new MyLib.Math();
            var result = math.Add(result1.Result, result2.Result);
            Console.WriteLine($"Result is {result:F2}");
        }

        private (bool Ok, double Result) Parse(string arg, string position)
        {
            var ok = double.TryParse(arguments.First(), out double parsedValue);
            if (!ok)
            {
                Console.WriteLine($"{position} argument must be a float number, but was {arg}");
            }

            return (ok, parsedValue);
        }
    }
}

```

We have now introduced a few more concepts:

* The program is split into a simple static Main, and the rest as Instance methods.
* Constructors with parameters
* Local member variable
* Generic list with string
* Tuples as results from a method
* Private function

```
dotnet run 45.5  45
Result is 91.00
```

Oops - something went wrong somewhere.....   That result is not correct.

## Unit testing

Now go into the test project.

Return to Visual Studio,a dn look at the left side.  You should see a Test Explorer window there.  (If not, get it from the top menu, Test/Test Explorer)

Press the Run All button to the left in the top button bar of that hub.

It should go green.  Double click the Test1 node, to see the code.

We now want to unit test the program we wrote.  

Let us start with checking the Math library we had

```csharp
        [Test]
        public void TestMath()
        {
            var sut = new MyLib.Math();
            var result = sut.Add(45.5, 45);
            Assert.That(result, Is.EqualTo(90.5).Within(0.001));
        }
```

Notice the Within constraint added.  Doubles are never exact, so we put a range to it.

Now do a Test All again, and it should go green. 

#### Testing the program

The program itself seems to have the error, but it is not that easy to test.  So let us make the program itself more testable.

First, add a project reference in the Test project to the cons project.

Then make the Run method return a double, which should be the result from the Add operation.  There is one snag here, and that is in case of errors, we can't really see that explicitly.  So we will introduce a bool Property.

Add the following to the class:

```csharp
        public bool Ok { get; private set; } = false;
```

Now, in the Run method, after the parsing, just before the call the Math.Add, do:

```csharp
    Ok = true;
```

This property is now read only from the outside.  The private set'er ensures we can set it from inside the class.

Then, make the Parse method public too. We do this so that we can test this by itself.  Make a /// comment above the Parse method in Visual Studio, it should expand to a comment block:  Add the comment `Made public for testing`

Go back to the test project, and in the same test class (we could make a new one, but just for speedy dev now, we'll continue with the same).

Add a new Test method, but now we shall use another type of test:

```csharp

```









