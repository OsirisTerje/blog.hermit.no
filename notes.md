# Notes


## Finding installed .Net Frameworks

```
gci ‘HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP’ -recurse | gp -name Version -EA 0 | where { $_.PSChildName -match ‘^(?!S)\p{L}’} | select PSChildName, Version
```

[Read More](https://www.raymond.cc/blog/how-to-check-what-version-of-microsoft-net-framework-is-installed-in-computer/2/)
