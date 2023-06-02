---
title: Loading and saving workbook |Syncfusion|
description: Explains the various types of the load and save operations in present in the Syncfusion XlsIO control
platform: file-formats
control: XlsIO
documentation: UG
---

# Loading and Saving Workbook

There are various types of load and save operations in Syncfusion XlsIO. Please specific operations are documented under below re-directions.

* [ASP.NET Core](loading-and-saving/loading-and-saving-excel-files-in-asp-net-core-c-sharp)
* [ASP.NET MVC](loading-and-saving/loading-and-saving-excel-files-in-asp-net-mvc-c-sharp)
* [ASP.NET](loading-and-saving/loading-and-saving-excel-files-in-asp-net-c-sharp)
* [Blazor](loading-and-saving/loading-and-saving-excel-files-in-blazor-c-sharp)
* [Xamarin](loading-and-saving/loading-and-saving-excel-files-in-xamarin-c-sharp)
* [Windows Forms](loading-and-saving/loading-and-saving-excel-files-in-windows-forms-c-sharp)
* [WPF](loading-and-saving/loading-and-saving-excel-files-in-wpf-c-sharp)
* [UWP](loading-and-saving/loading-and-saving-excel-files-in-uwp-c-sharp)
* [WinUI](loading-and-saving/loading-and-saving-excel-files-in-winui-c-sharp)
* [.NET MAUI](loading-and-saving/loading-and-saving-excel-files-in-maui-c-sharp)

## Closing a workbook

Once after the workbook manipulation and save operation are completed, you should close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html), in order to release all the memory consumed by XlsIO’s DOM. The following code snippet illustrates how to close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html).

N> If the new instance for [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) is created in using statement, then there is no need to closing workbook and disposing excelEngine.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Close the instance of IWorkbook
workbook.Close();

//Dispose the instance of ExcelEngine
excelEngine.Dispose();
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Close the instance of IWorkbook
workbook.Close();

//Dispose the instance of ExcelEngine
excelEngine.Dispose();
{% endhighlight %}
{% endtabs %}

T>You can use [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object to prevent the data loss while unfortunately closing the workbook or disposing excel engine without saving contents. If it is set to true, then **ExcelWorkbookNotSavedException** will be thrown when you forgot to save the workbook before closing them. Following code illustrates how to set [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}
{% endtabs %} 

A complete working example for creating and editing an Excel workbook in C# is present on [this GitHub page](https://github.com/SyncfusionExamples/XlsIO-Examples/tree/master/Read%20and%20Edit%20Excel/Read%20and%20Edit%20Excel).
 
## Sending to a client browser

You can save & send the workbook to a client browser from a web site or web application by invoking the below shown overload of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_String_System_Web_HttpResponse_Syncfusion_XlsIO_ExcelDownloadType_) method. This method explicitly make use of an instance of [HttpResponse](https://docs.microsoft.com/en-us/dotnet/api/system.web.httpresponse?view=netframework-4.8) as its parameter in order to stream the workbook to client browser. So this overload is suitable for web application which references **System.Web** assembly.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Load the file into stream
FileStream inputStream = new FileStream("Sample.xlsx", FileMode.Open, FileAccess.Read);

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Xlsx;

//Save the workbook to stream
MemoryStream outputStream = new MemoryStream();
workbook.SaveAs(outputStream);
outputStream.Position = 0;

//Return the file with content type
return File(outputStream, "Application/msexcel", "Output.xlsx");
{% endhighlight %}

{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(Server.MapPath("App_Data/Sample.xlsx"));

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Xlsx;

//Save the workbook to disk in xlsx format
workbook.SaveAs("Output.xlsx", Response, ExcelDownloadType.Open, ExcelHttpContentType.Excel2016);
{% endhighlight %}
{% endtabs %}  
