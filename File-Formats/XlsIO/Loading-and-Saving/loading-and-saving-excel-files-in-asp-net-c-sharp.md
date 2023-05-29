---
title: Loading and saving workbook in ASP.NET | Syncfusion
description: Explains how to load and save Excel files in ASP.NET applications using Syncfusion Excel library.
platform: file-formats
control: XlsIO
documentation: UG
---
# Loading and saving workbook in ASP.NET

## Opening an existing workbook

You can open an existing workbook by using the overloads of [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_String_) methods of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) interface.

{% tabs %}  
{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(Server.MapPath("App_Data/Sample.xlsx"));
{% endhighlight %}
{% endtabs %}

## Saving an Excel workbook

You can also save the created or manipulated workbook using overloads of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_String_System_Web_HttpResponse_Syncfusion_XlsIO_ExcelDownloadType_Syncfusion_XlsIO_ExcelHttpContentType_) methods.

{% tabs %}
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

## Closing a workbook

Once after the workbook manipulation and save operation are completed, you should close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html), in order to release all the memory consumed by XlsIO’s DOM. The following code snippet illustrates how to close the instance of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html) and dispose the instance of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html).

N> If the new instance for [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) is created in using statement, then there is no need to closing workbook and disposing excelEngine.

{% tabs %}
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

//Close the instance of IWorkbook
workbook.Close();

//Dispose the instance of ExcelEngine
excelEngine.Dispose();
{% endhighlight %}
{% endtabs %}

T>You can use [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object to prevent the data loss while unfortunately closing the workbook or disposing excel engine without saving contents. If it is set to true, then **ExcelWorkbookNotSavedException** will be thrown when you forgot to save the workbook before closing them. Following code illustrates how to set [ThrowNotSavedOnDestroy](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html#Syncfusion_XlsIO_ExcelEngine_ThrowNotSavedOnDestroy) property of [ExcelEngine](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.ExcelEngine.html) object.

{% tabs %}
{% highlight c# tabtitle="C# [Windows-specific]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//No exception will be thrown if there are unsaved workbooks
excelEngine.ThrowNotSavedOnDestroy = true;
{% endhighlight %}
{% endtabs %}
 
## Sending to a client browser

You can save & send the workbook to a client browser from a web site or web application by invoking the below shown overload of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_String_System_Web_HttpResponse_Syncfusion_XlsIO_ExcelDownloadType_) method. This method explicitly make use of an instance of [HttpResponse](https://docs.microsoft.com/en-us/dotnet/api/system.web.httpresponse?view=netframework-4.8) as its parameter in order to stream the workbook to client browser. So this overload is suitable for web application which references **System.Web** assembly.

{% tabs %}
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
workbook.SaveAs("Output.xlsx", Response, ExcelDownloadType.Open);
{% endhighlight %}
{% endtabs %}  
