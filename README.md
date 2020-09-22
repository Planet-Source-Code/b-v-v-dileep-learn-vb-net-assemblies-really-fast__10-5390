<div align="center">

## Learn VB\.NET assemblies really fast\!


</div>

### Description

This article explains .NET assemblies.The .NET assemblies are the basic building blocks of .NET applications, so learning about .NET assemblie is important.Please please dont forget to rate me!
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[B\.v\.v\.Dileep](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/b-v-v-dileep.md)
**Level**          |Beginner
**User Rating**    |2.8 (11 globes from 4 users)
**Compatibility**  |VB\.NET
**Category**       |[Coding Standards](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/coding-standards__10-33.md)
**World**          |[\.Net \(C\#, VB\.net\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/net-c-vb-net.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/b-v-v-dileep-learn-vb-net-assemblies-really-fast__10-5390/archive/master.zip)





### Source Code

```
VB.NET Assemblies
Introduction:
     The main problem with conventional COM component or Win32 DLL on a machine often leads to incompatibility.When different versions of the same type of COM or DLLs are installed on a machine these arises issues commonly called as DLL Hell. To overcome these incompatibilities, .NET provides a concept called Assemblies.The whole programming concept of .NET programming is based on use of assemblies.
Global Assembly Cache(GAC):
       All the assemblies stored in a machine are visible from Global Assembly Cache(GAC).You can see all the assemblies installed on your machine using the GAC viewer located at your <Windir>\assembly folder on Win XP and WinNT on Windows 2000.The other way to see the installed assemblies is by using .Net configuration tool, which is located at Control Panel | Administrative Tools | Microsoft .NET Framework(version).
Creating Assemblies:
  To use assemblies the steps are:
  1.Creating a Shared assembly.
     i.Strong name the assembly.
     ii.Putting the assembly in Global Assembly Cache(GAC).
  2.Creating a simple client.
The main use of using assemblies is to reduce DLL conflicts, so to see the advantages of assemblies we see:
  3.Creating a new version of Shared assembly
  4.Configuring the client to use the new version of the assembly.
  1.Creating a Shared assembly:
     Lets use a simple class named SimpleAssembly as our assembly.Any client should use this assembly.
The SimpleAssembly is merely a normal class,which returns the message “From SimpleAssembly” to the called client.
Create a new Class Library in VB.NET named SimpleAssembly, and add the following code:
        Public Class SimpleAssembly
        Public Function message()
        Return ("From SimpleAssembly")
        End Function
    End Class
That’s it we created the class to be used as assembly!
    i.Strong naming the assembly:
   The next step is to make our class Strong Name.A Strong name identifies an assembly uniquiely from others.There are much like GUIDs for COM components.To strong name an assembly VS.NET comes with an utility called as sn, using which we can strong name an assembly.
Open .NET console window from Start | Programs | Visual Studio.NET 2003 | Visual Studio .NET 2003 Tools | Visual Studio .NET 2003 Command Prompt. At the command prompt type: sn /k Skey.snk. This creates a file named Skey.snk which is the unique ID for our assembly.Now we have to associate this key to out SimpleAssembly.Copy the Skey.snk file to the folder where the files of our SimpleAssembly are located.
After copying the file open SimpleAssembly class library, and open the AssemblyInfo.vb file.The AssemblyInfo.vb file tells the CLR about the version numbers description,etc for an project
An AssemblyInfo.vb file looks like:
        <Assembly: AssemblyTitle("")>
    <Assembly: AssemblyDescription("")>
    ..
Now we have to associate the unique key generated to our SimpleAssembly class.Open AssemblyInfo.vb file and specify the key pair file as:
       <Assembly: AssemblyKeyFile(“path of key file generated”)>
    <Assembly: AssemblyTitle("")>
    <Assembly: AssemblyDescription("")>
No build the SimpleAssembly class library by Build | Build SimpleAssembly
    ii.Putting the assembly in GAC:
     Now that we have created an assembly we have to keep it in the GAC.In the .NET Configuration tool click on My Computer node and then right click on Assembly Cache and select Add from the menu.Browse to the SimpleAssembly.dll and click ok to add to assembly cache.Now our SimpleAssembly can be viewed from the GAC.
2.Creating a simple client:
   Now that we created an assembly it is of no use, until we use it in our client applications.We should have a client application from which we can call our SimpleAssembly class.To do that, create a new Windows application and add a reference to our SimpleAssembly class by right clicking on the reference section in the project window and selecting Add reference from the menu.In the window that appears click browse and select our SimpleAssembly.dll file and click Ok.Now a reference to our SimpleAssembly is added.
Add the following code to the button_click:
          Public Class Form1 Inherits System.Windows.Forms.Form
      #Region " Windows Form Designer generated code "
       Dim a1 As New SimpleAssembly.SimpleAssembly
Private Sub Button1_Click(ByVal sender As System.Object, ByVal System.EventArgs) HandleButton1.Click
    MessageBox.Show(a1.message())
  End Sub
End Class
Now when you click Button1, you will reeive a message box with text “From SimpleAssembly”.
3.Creating a new version of assembly:
     Therefore we created a Client to use our assembly.But this is not the outstanding feature of assemblies,we can do the same with COM, and DLLs.
To understand the feature of assembies, lets modify the SimpleAssembly class library as:
          Public Class SimpleAssembly
       Public Function message()
       Return ("Hello From SimpleAssembly")
      End Function
     End Class
  To reflect the new version of our SimpleAssembly , lets change its version number as:               <Assembly:AssemblyVersion("1.1.*")> from AssemblyInfo.vb file.Now build the new version of our SimpleAssembly by clicking Build | Build SimpleAssembly.When see the new build dll from bin folder the version is something as 1.1…..
Now as our new version of our SimpleAssembly we have to add to the GAC as described above.You will find two versions of SimpleAssembly ‘s in GAC with different version numbers.
4.Configuring the client to use new version of assembly:
       Now to configure our SimpleClient to use the new version of SimpleAssembly,from the GAC right click the      SimpleAssembly with version number 1.1.. and select properties.From properties of new version of SimpleAssembly, copy its version number.Now right click applications section in the .NET Configuration tool and select add from menu and select the SimpleClient.exe from the list or click browse to locate the file SimpleClient.exe file.
Now our SimpleClient is added to the applications section.
Right click the Configured assemblies node under SimpleClient and select Add from the menu.An dialog box named Configure an Assembly select the radio button “Choose as assembly from the list of assemblies this application uses”, now click “Choose assembly…” and then select the SimpleAssembly from the list and then click Ok.Now an dialog box named SimpleAssembly properties appear and from this select the “Binding Policy” tab.In the Binding Policy tab in the “Requested Version section textbox enter “1.0.0.0-1.0.9999.9999” and in the new version section textbox, enter the new version of the SimpleAssembly class and then click Ok.
     Now run the SimpleClient application and you will see that this uses the new version of the SimpleAssembly!
Behind the scene:
In SimpleClient folder look in the bin folder you will observe SimpleCLient.exe.config file, this is the file that makes the SimpleClient application to use the new version of the SimpleAssembly class.If you delete this file, you will observe that the SimpleClient uses the older version of the SimpleAssembly.
```

