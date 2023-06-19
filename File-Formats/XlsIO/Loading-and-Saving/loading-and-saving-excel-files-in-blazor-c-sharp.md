---
title: Loading and saving workbook in Blazor | Syncfusion
description: Explains how to load and save Excel files in Blazor applications using Syncfusion XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---
# Loading and saving workbook in Blazor

## Opening an existing workbook from Stream

You can open an existing workbook from stream by using the overloads of [Open](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html#Syncfusion_XlsIO_IWorkbooks_Open_System_IO_Stream_) methods of [IWorkbooks](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbooks.html) interface. 

The code snippet for this process in Blazor Server-Side application is given below.

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
{% endhighlight %}
{% endtabs %}  

The code snippet for this process in Blazor Client-Side application is given below.

{% tabs %}  
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Load the file into stream
Stream inputStream = await client.GetStreamAsync("sample-data/Sample.xlsx");

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);
{% endhighlight %}
{% endtabs %}  

## Saving an Excel workbook to stream

You can also save the created or manipulated workbook to stream using overloads of [SaveAs](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_SaveAs_System_IO_Stream_) methods.

The code snippet for this process in Blazor Server-Side application is given below.

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

//Save the document as a stream and retrun the stream.
using (MemoryStream outputStream = new MemoryStream())
{
  //Save the created Excel document to MemoryStream.
  workbook.SaveAs(outputStream);

  return outputStream;
}
{% endhighlight %}
{% endtabs %} 

The code snippet for this process in Blazor Client-Side application is given below.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
//Creates a new instance for ExcelEngine
ExcelEngine excelEngine = new ExcelEngine();

//Initialize IApplication
IApplication application = excelEngine.Excel;

//Load the file into stream
Stream inputStream = await client.GetStreamAsync("sample-data/Sample.xlsx");

//Loads or open an existing workbook through Open method of IWorkbooks
IWorkbook workbook = application.Workbooks.Open(inputStream);

//To-Do some manipulation
//To-Do some manipulation

//Set the version of the workbook
workbook.Version = ExcelVersion.Xlsx;

//Save the document as a stream and retrun the stream.
using (MemoryStream outputStream = new MemoryStream())
{
  //Save the created Excel document to MemoryStream.
  workbook.SaveAs(outputStream);

  return outputStream;
}
{% endhighlight %}
{% endtabs %}

## Helper Code Snippets

Create a class file with name as ``FileUtils`` and add the following code to invoke the JavaScript action for downloading the file in browser.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
public static class FileUtils
{
    public static ValueTask<object> SaveAs(this IJSRuntime js, string filename, byte[] data)
        => js.InvokeAsync<object>(
           "saveAsFile",
           filename,
           Convert.ToBase64String(data));
}
{% endhighlight %}
{% endtabs %}

Add the following JavaScript function in the ``index.html`` file present under ``wwwroot``.

{% tabs %}
{% highlight c# tabtitle="C# [Cross-platform]" %}
<script type="text/javascript">
  function saveAsFile(filename, bytesBase64) {

  if (navigator.msSaveBlob) 
  {
    //Download document in Edge browser
    var data = window.atob(bytesBase64);
    var bytes = new Uint8Array(data.length);
    for (var i = 0; i < data.length; i++) 
    {
      bytes[i] = data.charCodeAt(i);
    }
    var blob = new Blob([bytes.buffer], { type: "application/octet-stream" });
    navigator.msSaveBlob(blob, filename);
  }
  else 
  {
    var link = document.createElement('a');
    link.download = filename;
    link.href = "data:application/octet-stream;base64," + bytesBase64;
    document.body.appendChild(link); // Needed for Firefox
    link.click();
    document.body.removeChild(link);
  }
}
</script>
{% endhighlight %}
{% endtabs %}