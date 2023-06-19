---
title: Loading and saving workbook in Xamarin | Syncfusion
description: Explains how to load and save Excel files in Xamarin applications using Syncfusion XlsIO
platform: file-formats
control: XlsIO
documentation: UG
---
# Loading and saving workbook in Xamarin

## Opening an existing workbook from stream

You can open an existing workbook from stream by using the overloads of [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_IO_Stream_) methods of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) interface.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Load the file into stream
Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = executingAssembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);
{% endhighlight %}
{% endtabs %}  

## Saving an Excel workbook to stream

You can also save the created or manipulated workbook to stream using overloads of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_IO_Stream_) methods.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Load the file into stream
Assembly executingAssembly = typeof(App).GetTypeInfo().Assembly;
Stream inputStream = executingAssembly.GetManifestResourceStream("XamarinSample.Sample.xlsx");

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Xlsx;

//Saving the workbook as stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);
outputStream.Position = 0;

//Saves the memory stream as a file.
Xamarin.Forms.DependencyService.Get<ISave>().SaveAndView("Output.xlsx", "application/msexcel", outputStream);
{% endhighlight %}
{% endtabs %} 

Download the helper files from this [link](https://www.syncfusion.com/downloads/support/directtrac/general/ze/HELPER~1-1423062113.zip) and add them into the mentioned project. These helper files allow you to save the stream as a physical file and open the file for viewing.

<table>
<tr>
<thead><th>
Project</th>
<th>
File Name
</th>
<th>
Summary
</th>
</thead>
</tr>
<tbody>
<tr>
<td>
Portable project
</td>
<td>
ISave.cs
</td>
<td>
Represent the base interface for save operation
</td>
</tr>
<tr>
<td>
iOS Project
</td>
<td>
<ul>
<li>SaveIOS.cs</li>
<li>PreviewControllerDS.cs</li>
</ul>
</td>
<td>
<ul>
<li>Save implementation for iOS device</li>
<li>Helper class for viewing the Excel file in iOS device</li>
</ul>
</td>
</tr>
<tr>
<td>
Android project
</td>
<td>
SaveAndroid.cs
</td>
<td>
Save implementation for Android device
</td>
</tr>
<tr>
<td>
WinPhone project
</td>
<td>
SaveWinPhone.cs
</td>
<td>
Save implementation for Windows Phone device
</td>
</tr>
<tr>
<td>
UWP project
</td>
<td>
SaveWindows.cs
</td>
<td>
Save implementation for UWP device.
</td>
</tr>
<tr>
<td>
Windows(8.1) project 
</td>
<td>
SaveWindows81.cs
</td>
<td>
Save implementation for WinRT device.
</td>
</tr>
</tbody>
</table>
