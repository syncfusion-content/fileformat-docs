---
title: How to check whether an Excel document contains macro | Syncfusion
description: Code example to check whether an Excel document contains macro using Syncfusion .NET Excel library (XlsIO).
platform: file-formats
control: XlsIO
documentation: UG
---

# How to check whether an Excel document contains macro?
You can check whether the Excel document contains macro using [HasMacros](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html#Syncfusion_XlsIO_IWorkbook_HasMacros) property of [IWorkbook](https://help.syncfusion.com/cr/file-formats/Syncfusion.XlsIO.IWorkbook.html). The value true indicates that the Excel document has a Vba project.

The following code illustrate how to check whether an Excel document contains macro using XlsIO.
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

  //Check macro exist
  bool IsMacroEnabled = workbook.HasMacros;     

  // Save the workbook
  FileStream output = new FileStream("Output.xls", FileMode.Create, FileAccess.ReadWrite);
  workbook.SaveAs(output);
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
  IWorksheet sheet = workbook.Worksheets[0];

  //Check macro exist
  bool IsMacroEnabled = workbook.HasMacros;        

  //Save the workbook
  workbook.SaveAs("Output.xls");
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET [Windows-specific]" %}
Using excelEngine As ExcelEngine = New ExcelEngine()
  'Instantiate the excel application object.
  Dim application As IApplication = excelEngine.Excel

  'Opening a Workbook
  Dim workbook As IWorkbook = application.Workbooks.Open("Test.xls")
  Dim sheet As IWorksheet = workbook.Worksheets(0)

  'Check macro exist
  Dim IsMacroEnabled As Boolean = workbook.HasMacros            

  ‘Save the workbook 
  workbook.SaveAs("Output.xls")
End Using
{% endhighlight %}
{% endtabs %}   

## See Also

* [How to open an Excel 2013 Macro Enabled Template?](how-to-open-an-excel-2013-macro-enabled-template)
* [Does XlsIO support Excel files with macros that are digitally signed?](does-xlsio-support-excel-files-with-macros-that-are-digitally-signed)
* [Does XlsIO support password protected macro in the Excel documents?](does-xlsio-support-password-protected-macro-in-the-excel-documents)
* [How to create a macro?](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#creating-a-macro)
* [How to edit a macro?](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#editing-a-macro)
* [How to remove macros?](https://help.syncfusion.com/file-formats/xlsio/working-with-macros#removing-macros)
