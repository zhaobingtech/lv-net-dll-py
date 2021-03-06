# .NET DLL (with LabVIEW classes) in Python [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/etfovac/lv-net-dll-py/blob/master/LICENSE) [![DOI](https://zenodo.org/badge/286333382.svg)](https://zenodo.org/badge/latestdoi/286333382)
 
 Access a .NET DLL (with LabVIEW classes) in Python  

``` python 
    ca_obj = ClientApp1Lib.ClientApp1Lib.ClientApp1()  
    # alas, it calls "new" which triggers file search popup window (known LabVIEW class issue)  
```  
``` python
    # so start with a non initialized obj ref and use Create.vi to initialize the LabVIEW class ref
    ca_obj = AssemblyLib.ClientApp1Lib.ClientApp1  
    ca_Type = clr.GetClrType(AssemblyLib.ClientApp1Lib.ClientApp1) # get type  
    print(ca_Type.FullName, "\t", ca_Type)  
    # GetUninitializedObject to avoid constructor and 'new' issue  
    ca_obj = System.Runtime.Serialization.FormatterServices.GetUninitializedObject(ca_Type)  
```  
``` python
    print(ca_obj.IsValid(), "\t", ca_obj) # False
    ca_obj = AssemblyLib.ClientApp1Lib.ClientApp1.Create(ca_obj, ca_obj)
    print(ca_obj.IsValid(), "\t", ca_obj) # True
``` 
Note: For more on the constructor node issue in VS see <a href="https://github.com/etfovac/dll/issues/2#issue-673036198">'new' triggers browsing to lvclass file on disk</a>  

### Dependency
<a href="https://github.com/etfovac/dll/tree/master/InteropAssembly">ClientApp1.dll (my InteropAssembly example)</a>  

### References
<a href="https://github.com/etfovac/dll/blob/master/ConsoleApp_RA_e0/Program.cs">ConsoleApp_RA_e0/Program.cs (my C# Console example)</a>  
<a href="https://github.com/pythonnet/pythonnet/wiki/How-to-call-a-dynamic-library">How to call a dynamic library (pythonnet wiki)</a>   
<a href="https://stackoverflow.com/questions/49942487/python-for-net-how-to-explicitly-create-instances-of-c-sharp-classes-using-dif">python for net how to explicitly create instances of csharp classes (stackoverflow qa)</a>   
