---
title: Loading and saving workbook
description: Explains various load and save operations in XlsIO
platform: File-formats
control: XlsIO
documentation: UG
---

# Loading and Saving Workbook

## Opening an existing workbook

You can open an existing workbook by using the Open method of IWorkbooks interface.

{% tabs %}  
{% highlight c# %}
//Creates a new instance for ExcelEngine.

ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks

IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileName);



{% endhighlight %}

{% highlight vb %}
'Creates a new instance for ExcelEngine.

Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks

Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(fileName)



{% endhighlight %}
{% endtabs %}  

## Opening an existing workbook from Stream

You can open an existing workbook from stream by using the overloads of Open methods of IWorkbooks interface.

{% tabs %}  
{% highlight c# %}
//Creates a new instance for ExcelEngine.

ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks

IWorkbook workbook = excelEngine.Excel.Workbooks.Open(workbookStream);



{% endhighlight %}

{% highlight vb %}
'Creates a new instance for ExcelEngine.

Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks

Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(workbookStream)



{% endhighlight %}
{% endtabs %}  

## Saving a Excel workbook to file system

You can save the created or manipulated workbook to file system using Save method of IWorkbook interface. The workbook is saved in the xls/xlsx format based on the application/workbook version specified, whereas saved in Excel 97-2003 (*.xls) format by default.

{% tabs %}  
{% highlight c# %}
//Creates a new instance for ExcelEngine.

ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks

IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Set the version of the workbook.

workbook.Version = ExcelVersion.Excel2013;

//Save the workbook in file system as xlsx format

workbook.SaveAs(outputFileName);



{% endhighlight %}

{% highlight vb %}
'Creates a new instance for ExcelEngine.

Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks

Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Set the version of the workbook.

workbook.Version = ExcelVersion.Excel2013

'Save the workbook in file system as xlsx format

workbook.SaveAs(outputFileName)



{% endhighlight %}
{% endtabs %}  

## Saving a Excel workbook to stream

You can also save the created or manipulated workbook to stream using overloads of Save methods

{% tabs %}  
{% highlight c# %}
//Creates a new instance for ExcelEngine.

ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks

IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Set the version of the workbook.

workbook.Version=ExcelVersion.Excel2013;

//Save the workbook in file system as xlsx

workbook.SaveAs(outputStream);



{% endhighlight %}

{% highlight vb %}
'Creates a new instance for ExcelEngine.

Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks

Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Set the version of the workbook.

workbook.Version = ExcelVersion.Excel2013

'Save the workbook in file system as xlsx

workbook.SaveAs(outputStream)



{% endhighlight %}
{% endtabs %} 
 
## Sending to a client browser

You can save & send the workbook to a client browser from a web site or web application by invoking the below shown overload of Save method.  This method explicitly make use of an instance of [HttpResponse](https://msdn.microsoft.com/en-us/library/system.web.httpresponse(v=vs.110).aspx# "") as its parameter in order to stream the workbook to client browser. So this overload is suitable for web application which references System.Web assembly.

{% tabs %}  
{% highlight c# %}
//Creates a new instance for ExcelEngine.

ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks

IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Set the version of the workbook.

workbook.Version=ExcelVersion.Excel2013;

//Save the workbook in file system

workbook.SaveAs(OutputFileName, Response, ExcelDownloadType.Open);



{% endhighlight %}

{% highlight vb %}
'Creates a new instance for ExcelEngine.

Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks

Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Set the version of the workbook.

workbook.Version = ExcelVersion.Excel2013

'Save the workbook in file system

workbook.SaveAs(OutputFileName, Response, ExcelDownloadType.Open)



{% endhighlight %}
{% endtabs %}  

## Closing a workbook

Once after the workbook manipulation and save operation are completed, you should close the instance of IWorkbook and dispose the instance of ExcelEngine, in order to release all the memory consumed by XlsIO’s DOM. The following code snippet illustrates how to close the instance of IWorkbook and dispose the instance of ExcelEngine.

{% tabs %}  
{% highlight c# %}
//Creates a new instance for ExcelEngine.

ExcelEngine excelEngine = new ExcelEngine();

//Loads or open an existing workbook through Open method of IWorkbooks

IWorkbook workbook = excelEngine.Excel.Workbooks.Open(fileName);

//To-Do some manipulation

//To-Do some manipulation

//Set the version of the workbook.

workbook.Version=ExcelVersion.Excel2013;

//Save the workbook in file system.

workbook.SaveAs(outputFileName);

// Close the instance of IWorkbook.

workbook.Close();

// Dispose the instance of ExcelEngine.

excelEngine.Dispose();



{% endhighlight %}

{% highlight vb %}
'Creates a new instance for ExcelEngine.

Dim excelEngine As New ExcelEngine()

'Loads or open an existing workbook through Open method of IWorkbooks

Dim workbook As IWorkbook = excelEngine.Excel.Workbooks.Open(fileName)

'To-Do some manipulation

'To-Do some manipulation

'Set the version of the workbook.

workbook.Version = ExcelVersion.Excel2013

'Save the workbook in file system.

workbook.SaveAs(outputFileName)

' Close the instance of IWorkbook.

workbook.Close()

' Dispose the instance of ExcelEngine.

excelEngine.Dispose()



{% endhighlight %}
{% endtabs %}  

