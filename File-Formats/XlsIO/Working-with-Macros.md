---
title: Macros | Excel library | Syncfusion
description: In this section, you can learn how to create, edit and remove macros and perform different macro operations in Excel using XlsIO
platform: file-formats
control: XlsIO
documentation: UG
---
# Working with Macros in Syncfusion Excel library

Macro is a set of process that can be run repeatedly in Excel document. 

## Creating a Macro

XlsIO allows to create macros in Excel document through [IVbaProject](https://help.syncfusion.com/cr/file-formats/Syncfusion.Office.IVbaProject.html) interface. The macro document can be saved into different formats such as XLS, XLTM and XLSM.
XlsIO supports creating macro in following types using [VbaModuleType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Office.VbaModuleType.html) enum.

* Document 
* StdModule
* Class
* MsForm

You can add a Vba module through [IVbaModules](https://help.syncfusion.com/cr/file-formats/Syncfusion.Office.IVbaModules.html) interface in XlsIO.

### Document
Document is the default module type which will be added for every worksheet and one for entire workbook while creating VbaProject. 

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Adding Document to the workbook
IVbaProject project = workbook.VbaProject;
IVbaModule module = project.Modules.Add("Document ", VbaModuleType. Document);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Adding Document to the workbook
IVbaProject project = workbook.VbaProject;
IVbaModule module = project.Modules.Add("Document", VbaModuleType.Document);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
//Adding Document to the workbook
Dim project As IVbaProject = workbook.VbaProject
Dim [module] As IVbaModule = project.Modules.Add("Document ", VbaModuleType. Document)
{% endhighlight %}
{% endtabs %}   

The following code illustrate how to use Document module in Excel document.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  // Accessing sheet module
  IVbaModule vbaModule = vbaModules[sheet.CodeName];

  //Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open\n MsgBox \" Workbook Opened \" \n End Sub";

  //Saving as macro document
  FileStream output = new FileStream("Output.xlsm", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsMacro);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Accessing sheet module
  IVbaModule vbaModule = vbaModules[sheet.CodeName];

  //Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open\n MsgBox \"Workbook Opened\" \n End Sub";

  //Saving as macro document
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Creating new Workbook
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  ‘Accessing sheet module
  Dim vbaModule As IVbaModule = vbaModules(sheet.CodeName)

  'Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open" & vbLf & " MsgBox "" Workbook Opened "" " & vbLf & " End Sub"

  'Saving as macro document
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}
{% endtabs %}

A complete working example to create macro as document in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Create%20Macro%20as%20Document).    

The Vba project in the output looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image1.png)

The macro output in the Excel document looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image2.png)

### StdModule
StdModule is the module created for whenever a macro process is recorded in Excel document.

The following code illustrate how to add a StdModule using Add method. Here, the parameters name and [VbaModuleType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Office.VbaModuleType.html) enum value is used.

* Test – Macro module name added to the Vba project.
* StdModule – Type of the Vba module.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Adding StdModule to the workbook
IVbaProject project = workbook.VbaProject;
IVbaModule module = project.Modules.Add("Test", VbaModuleType.StdModule);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Adding StdModule to the workbook
IVbaProject project = workbook.VbaProject;
IVbaModule module = project.Modules.Add("Test", VbaModuleType.StdModule);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
//Adding StdModule to the workbook
Dim project As IVbaProject = workbook.VbaProject
Dim [module] As IVbaModule = project.Modules.Add("Test", VbaModuleType.StdModule)
{% endhighlight %}
{% endtabs %}   

The following code illustrate how to create a macro using StdModule in Excel document.
{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Adding a vba module
  IVbaModule vbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule);

  //Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open\n MsgBox \"Macro Added\" \n End Sub";

  //Saving as macro document
  FileStream output = new FileStream("Output.xlsm", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsMacro);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Adding a vba module
  IVbaModule vbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule);

  //Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open\n MsgBox \"Macro Added\" \n End Sub";

  //Saving as macro document
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Creating new Workbook
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  'Adding a vba module
  Dim vbaModule As IVbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule)

  'Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open" & vbLf & " MsgBox ""Macro Added"" " & vbLf & " End Sub"

  'Saving as macro document
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}
{% endtabs %}   

A complete working example to create macro as standard module in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Create%20Macro%20as%20StdModule).    

The Vba project in the output Excel document looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image3.png)

The Macro output in the Excel document looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image4.png)

### Class
Class module allows us to create our own object model to use it where same kind of objects needs to be added with different values such as creating the employee information list. XlsIO supports creating a class module in Excel document.

The following code illustrate how to add a class in XlsIO. Here, the parameters name and [VbaModuleType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Office.VbaModuleType.html) enum value is used.

* Test – Class name used in the Vba project
* ClassModule – Type of Vba module

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Adding class module to the workbook
IVbaProject project = workbook.VbaProject;
IVbaModule module = project.Modules.Add("Test", VbaModuleType.ClassModule);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Adding class module to the workbook
IVbaProject project = workbook.VbaProject;
IVbaModule module = project.Modules.Add("Test", VbaModuleType.ClassModule);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
//Adding class module to the workbook
Dim project As IVbaProject = workbook.VbaProject
Dim [module] As IVbaModule = project.Modules.Add("Test", VbaModuleType.ClassModule)
{% endhighlight %}
{% endtabs %}   

The following code illustrate how to use class module to run a macro with another module in Excel document.
{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Adding a class module
  IVbaModule clsModule = vbaModules.Add("Test", VbaModuleType.ClassModule);
  clsModule.Code = "Public Sub Create()\n MsgBox \"Created a class module\" \n End Sub";

  //Adding a vba module
  IVbaModule vbaModule = vbaModules.Add("Module1", VbaModuleType.StdModule);

  //Using class in StdModule
  vbaModule.Code = "Sub Auto_Open()\n Dim obj As New test \n obj.Create \n End Sub";

  //Saving as macro document
  FileStream output = new FileStream("Output.xlsm", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsMacro);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Adding a class module
  IVbaModule clsModule = vbaModules.Add("Test", VbaModuleType.ClassModule);
  clsModule.Code = "Public Sub Create()\n MsgBox \"Created a class module\" \n End Sub";

  //Adding a vba module
  IVbaModule vbaModule = vbaModules.Add("Module1", VbaModuleType.StdModule);

  //Using class in StdModule
  vbaModule.Code = "Sub Auto_Open()\n Dim obj As New test \n obj.Create \n End Sub";

  //Saving as macro document
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Creating new Workbook
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  'Adding a vba module
  Dim vbaModule As IVbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule)

  'Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open" & vbLf & " MsgBox ""Macro Added"" " & vbLf & " End Sub"

  'Saving as macro document
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}
{% endtabs %}   

A complete working example to create macro as class in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Create%20Macro%20as%20Class).    

The Vba project in the output Excel document looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image5.png)

The Macro output in the Excel document looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image6.png)

### MsForm
MsForm is the form module in which we can have form controls such as textbox, label, buttons etc. Form module cannot be created by XlsIO, but it allows to copy from a form module existing another workbook to new workbook.

The following code illustrate how to add a class in XlsIO. Here, the parameters name and [VbaModuleType](https://help.syncfusion.com/cr/file-formats/Syncfusion.Office.VbaModuleType.html) enum value is used.

* UserForm – Class name used in the Vba project
* MsForm – Type of Vba module

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Adding class module to the workbook
IVbaProject project = workbook.VbaProject;
IVbaModule module = project.Modules.Add("UserForm", VbaModuleType.MsForm);
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Adding class module to the workbook
IVbaProject project = workbook.VbaProject;
IVbaModule module = project.Modules.Add("UserForm", VbaModuleType.MsForm);
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
//Adding class module to the workbook
Dim project As IVbaProject = workbook.VbaProject
Dim [module] As IVbaModule = project.Modules.Add("UserForm", VbaModuleType.MsForm)
{% endhighlight %}
{% endtabs %}   

The following code illustrate how to copy a form from another workbook to new workbook.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Opening form module existing workbook
  FileStream input = new FileStream("Test.xls", FileMode.Open, FileAccess.ReadWrite);
  IWorkbook newBook = application.Workbooks.Open(input);

  IVbaProject newProject = newBook.VbaProject;

  //Accessing existing form module
  IVbaModule form = newProject.Modules["UserForm1"];

  //Adding a form module in new workbook
  IVbaModule formModule = project.Modules.Add(form.Name, VbaModuleType.MsForm);

  //Copying the form code behind
  formModule.Code = form.Code;

  //Copying the designer of the form
  formModule.DesignerStorage = form.DesignerStorage;

  //Saving as macro document
  FileStream output = new FileStream("Output.xlsm", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsMacro);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Opening form module existing workbook
  IWorkbook newBook = application.Workbooks.Open("Test.xls");
  IVbaProject newProject = newBook.VbaProject;

  //Accessing existing form module
  IVbaModule form = newProject.Modules["UserForm1"];

  //Adding a form module in new workbook
  IVbaModule formModule = project.Modules.Add(form.Name, VbaModuleType.MsForm);

  //Copying the form code behind
  formModule.Code = form.Code;

  //Copying the designer of the form
  formModule.DesignerStorage = form.DesignerStorage;

  //Saving as macro document
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Creating new Workbook
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  'Open form existing workbook
  Dim newBook As IWorkbook = application.Workbooks.Open("Test.xls")
  Dim newProject As IVbaProject = newBook.VbaProject

  'Accessing existing form module
  Dim form As IVbaModule = newProject.Modules("UserForm1")

  'Adding a form module in new workbook
  Dim formModule As IVbaModule = project.Modules.Add(form.Name, VbaModuleType.MsForm)

  'Copying the form code behind
  formModule.Code = form.Code

  'Copying the designer of the form
  formModule.DesignerStorage = form.DesignerStorage

  'Saving as macro document
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}
{% endtabs %}   

A complete working example to create macro as MS Form in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Create%20Macro%20as%20MSForm).

The Vba project in the output Excel document looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image7.png)

### Assigning Macro to Shapes
XlsIO supports assigning macros to the shape controls in the Excel document through [OnAction](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IShape.html#Syncfusion_XlsIO_IShape_OnAction) property. 

The following code illustrate how to assign macros to shapes in Excel document.
{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Adding a vba module
  IVbaModule vbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule);

  //Adding vba code to the module
  vbaModule.Code = "Sub Invoke()\n MsgBox \"Macro Added\" \n End Sub";

  //Adding a auto shape
  IShape shape = sheet.Shapes.AddAutoShapes(AutoShapeType.Rectangle, 1, 2, 60, 70);
  shape.Name = "Shape1";

  //Assigning a Macro to shape
  shape.OnAction = "StdModule.Invoke";

  //Saving as macro document
  FileStream output = new FileStream("Output.xlsm", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsMacro);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Adding a vba module
  IVbaModule vbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule);

  //Adding vba code to the module
  vbaModule.Code = "Sub Invoke()\n MsgBox \"Macro Added\" \n End Sub";

  //Adding a auto shape
  IShape shape = sheet.Shapes.AddAutoShapes(AutoShapeType.Rectangle, 1, 2, 60, 70);
  shape.Name = "Shape1";

  //Assigning a Macro to shape
  shape.OnAction = "StdModule.Invoke";

  //Saving as macro document
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Creating new Workbook
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  'Adding a vba module
  Dim vbaModule As IVbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule)

  'Adding vba code to the module
  vbaModule.Code = "Sub Invoke()" & vbLf & " MsgBox ""Macro Added"" " & vbLf & " End Sub"

  'Adding a auto shape
  Dim shape As IShape = sheet.Shapes.AddAutoShapes(AutoShapeType.Rectangle, 1, 2, 60, 70)

  shape.Name = "Shape1"

  'Assigning a Macro to shape
  shape.OnAction = "StdModule.Invoke"

  'Saving as macro document
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}
{% endtabs %}   

A complete working example to assign macro to shape in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Shapes%20with%20Macro).

When the shape is clicked, the output looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image8.png)

### Saving macro enabled document into stream
By default, while saving the Excel workbook into stream, the file type will be based on the Excel version used. For Excel97to2003 version, the file format will be XLS type.  Above this version, the document will be saved as XLSX format. So, while saving the macro enabled documents into XLSM and XLTM formats into stream, the [ExcelSaveType](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelSaveType.html) should be provided as **SaveAsMacro** and **SaveAsMacroTemplate**. 

The following code illustrate how to save macro-enabled documents into stream.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  workbook.Version = ExcelVersion.Excel2016;
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Adding a vba module
  IVbaModule vbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule);

  //Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open\n MsgBox \"Macro Added\" \n End Sub";

  //Saving as Macro in XLTM format
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream, ExcelSaveType.SaveAsMacroTemplate);
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Creating new workbook
  IWorkbook workbook = application.Workbooks.Create(1);
  IWorksheet sheet = workbook.Worksheets[0];

  //Creating Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Adding a vba module
  IVbaModule vbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule);

  //Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open\n MsgBox \"Macro Added\" \n End Sub";

  //Saving as Macro in XLSM format
  MemoryStream stream = new MemoryStream();
  workbook.SaveAs(stream, ExcelSaveType.SaveAsMacro);
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Creating new Workbook
  Dim workbook As IWorkbook = application.Workbooks.Create(1)
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  'Adding a vba module
  Dim vbaModule As IVbaModule = vbaModules.Add("StdModule", VbaModuleType.StdModule)

  'Adding vba code to the module
  vbaModule.Code = "Sub Auto_Open" & vbLf & " MsgBox ""Macro Added"" " & vbLf & " End Sub"

  ‘Saving as Macro in XLSM format
  Dim stream As MemoryStream = New MemoryStream()
  workbook.SaveAs(stream, ExcelSaveType.SaveAsMacro)
End Using
{% endhighlight %}
{% endtabs %} 

A complete working example to save macro enabled document into stream in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Save%20as%20Stream).  

## Editing a Macro
XlsIO allows to edit the existing macros in the Excel documents. To edit macros in Excel document, the module containing the macro code needs to be modified. By using the name of the module, it can be accessed and edited in XlsIO.

The following code illustrate how to edit existing macro in Excel document.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  //Opening form module existing workbook
  FileStream input = new FileStream("Test.xls", FileMode.Open, FileAccess.ReadWrite);
  IWorkbook workbook = application.Workbooks.Open(input);
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Access a Vba Module
  IVbaModule vbaModule = vbaModules["Module1"];

  //Edit the macro
  vbaModule.Name = "CreateData";
  vbaModule.Code = "Sub Auto_Open()\n MsgBox \"Macro is edited\" \n End Sub ";

  //Saving as macro document
  FileStream output = new FileStream("Output.xlsm", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsMacro);

  input.Close();
  output.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  // Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Opening a workbook
  IWorkbook workbook = application.Workbooks.Open("Test.xls");
  workbook.Version = ExcelVersion.Excel2016;
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Access a Vba Module
  IVbaModule vbaModule = vbaModules["Module1"];

  //Edit the macro
  vbaModule.Name = "CreateData";
  vbaModule.Code = "Sub Auto_Open()\n MsgBox \"Macro is edited\" \n End Sub ";

  //Saving as macro document
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Opening a Workbook
  Dim workbook As IWorkbook = application.Workbooks.Open("Test.xls")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  'Accessing a vba module
  Dim vbaModule As IVbaModule = vbaModules("Module1")

  'Editing a module
  vbaModule.Name = "CreateData"
  vbaModule.Code = "Sub Auto_Open()" & vbLf & " MsgBox ""Macro is edited"" " & vbLf & " End Sub "

  'Saving as macro document
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}
{% endtabs %}   

A complete working example to edit macro in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Edit%20Macro).  

The Vba project in the output Excel document looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image9.png)

The Macro output in the Excel document looks like below.

![working with macros](Working-with-Macros_images/Working-with-Macros_image10.png)

N> Macros are parsed only when accessed. By default, opening and saving a macro file will preserve its macros.

## Removing Macros
Excel macro-enabled documents can be saved as normal documents where the macro process is not necessary. XlsIO supports saving the macro-enabled documents such as XLS, XLSM, XLTM without macros and normal documents such as XLSX and XLS. For that, macro in the Excel documents needs to be removed.

Macro in the Excel document can be removed in the following ways.

* Remove(String name)
* RemoveAt(int index)
* Clear()
* SkipOnSave

### Remove(string name)
Macro process exist in the Vba project’s code modules. To remove a macro, the Vba modules needs to be removed.

* name – Name of the Vba module needs to be removed.

The following code illustrate how to remove a module using [Remove](https://help.syncfusion.com/cr/file-formats/Syncfusion.Office.IVbaModules.html#Syncfusion_Office_IVbaModules_Remove_System_String_) method.
{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  //Opening form module existing workbook
  FileStream input = new FileStream("Test.xls", FileMode.Open, FileAccess.ReadWrite);
  IWorkbook workbook = application.Workbooks.Open(input);
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Remove macro module
  vbaModules.Remove("Module1");

  //Saving as macro document
  FileStream output = new FileStream("Output.xlsm", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsMacro);

  input.Close();
  output.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  // Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Opening a workbook
  IWorkbook workbook = application.Workbooks.Open("Test.xls");
  workbook.Version = ExcelVersion.Excel2016;
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Remove macro module
  vbaModules.Remove("Module1");

  //Saving as macro document
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Opening a Workbook
  Dim workbook As IWorkbook = application.Workbooks.Open("Test.xls")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  //Remove macro module
  vbaModules.Remove("Module1")

  'Saving as macro document
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}
{% endtabs %} 

A complete working example to remove macro using name in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Remove%20Macro%20with%20Name).    

### RemoveAt(int index)
Vba module can be removed using the position from the [IVbaModules](https://help.syncfusion.com/cr/file-formats/Syncfusion.Office.IVbaModules.html) collection.

* Index – Position of the Vba module in the modules collection.

The following code illustrate how to remove a macro using module index.
{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  //Opening form module existing workbook
  FileStream input = new FileStream("Test.xls", FileMode.Open, FileAccess.ReadWrite);
  IWorkbook workbook = application.Workbooks.Open(input);
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Remove macro module
  vbaModules.RemoveAt(0);

  //Saving as macro document
  FileStream output = new FileStream("Output.xlsm", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsMacro);
  input.Close();
  output.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  // Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Opening a workbook
  IWorkbook workbook = application.Workbooks.Open("Test.xls");
  workbook.Version = ExcelVersion.Excel2016;
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Remove macro module
  vbaModules.RemoveAt(0);

  //Saving as macro document
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Opening a Workbook
  Dim workbook As IWorkbook = application.Workbooks.Open("Test.xls")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  //Remove macro module
  vbaModules.RemoveAt(0)

  'Saving as macro document
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}
{% endtabs %} 

A complete working example to remove macro using index in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Remove%20Macro%20with%20Index).      

### Clear()
[Clear()](https://help.syncfusion.com/cr/file-formats/Syncfusion.Office.IVbaModules.html#Syncfusion_Office_IVbaModules_Clear) method removes all the Vba modules at once by clearing the module collection.

The following code illustrate how to remove all macros using **Clear** method.
{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  //Opening form module existing workbook
  FileStream input = new FileStream("Test.xls", FileMode.Open, FileAccess.ReadWrite);
  IWorkbook workbook = application.Workbooks.Open(input);
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Remove all macros
  vbaModules.Clear();

  //Saving as macro document
  FileStream output = new FileStream("Output.xlsm", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsMacro);
  input.Close();
  output.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  // Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Opening a workbook
  IWorkbook workbook = application.Workbooks.Open("Test.xls");
  workbook.Version = ExcelVersion.Excel2016;
  IWorksheet sheet = workbook.Worksheets[0];

  //Accessing Vba project
  IVbaProject project = workbook.VbaProject;

  //Accessing vba modules collection
  IVbaModules vbaModules = project.Modules;

  //Remove all macros
  vbaModules.Clear();

  //Saving as macro document
  workbook.SaveAs("Output.xlsm");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Opening a Workbook
  Dim workbook As IWorkbook = application.Workbooks.Open("Test.xls")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Creating Vba project
  Dim project As IVbaProject = workbook.VbaProject

  'Accessing vba modules collection
  Dim vbaModules As IVbaModules = project.Modules

  //Remove all macros
  vbaModules.Clear()

  'Saving as macro document
  workbook.SaveAs("Output.xlsm")
End Using
{% endhighlight %}
{% endtabs %}   

A complete working example to remove all macros in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Clear%20All%20Macros).      

### SkipOnSave
[SkipOnSave](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IApplication.html#Syncfusion_XlsIO_IApplication_SkipOnSave) allows to resave the Excel document into normal XLSX and XLS documents.

The following code illustrate how to save the macro-enabled document into normal Excel document.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  //Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  //Opening form module existing workbook
  FileStream input = new FileStream("Test.xls", FileMode.Open, FileAccess.ReadWrite);
  IWorkbook workbook = application.Workbooks.Open(input);
  IWorksheet sheet = workbook.Worksheets[0];

  //Skip Macros while saving
  application.SkipOnSave = SkipExtRecords.Macros;                

  //Saving as Excel without macro 
  FileStream output = new FileStream("Output.xlsx", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output, ExcelSaveType.SaveAsXLS);
  input.Close();
  output.Close();
}
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
using (ExcelEngine excelEngine = new ExcelEngine())
{
  // Instantiate the excel application object.
  IApplication application = excelEngine.Excel;

  // Opening a workbook
  IWorkbook workbook = application.Workbooks.Open("Test.xls");
  workbook.Version = ExcelVersion.Excel2016;
  IWorksheet sheet = workbook.Worksheets[0];

  //Skip Macros while saving
  application.SkipOnSave = SkipExtRecords.Macros;                

  //Saving as Excel without macro
  workbook.SaveAs("Output.xlsx");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Opening a Workbook
  Dim workbook As IWorkbook = application.Workbooks.Open("Test.xls")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  //Skip Macros while saving
  application.SkipOnSave = SkipExtRecords.Macros             

  'Saving as Excel without macro 
  workbook.SaveAs("Output.xlsx")
End Using
{% endhighlight %}
{% endtabs %} 

A complete working example to skip macro on save in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Create%20and%20Edit%20Macros/Skip%20Macro%20and%20Save).      
  
