---
title: Unprotect Excel Workbook | Syncfusion
description: Explains with an example on how to unprotect Excel workbook with password using Interop and Essential XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Unprotect Excel Workbook

The workbooks protected by structure and window can be unprotected with the password specified during protection.

The following code shows how to unprotect Excel workbook using Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void UnprotectWorkbook()
{
  //Instantiate the application object
  var excelApp = new Microsoft.Office.Interop.Excel.Application();

  //Specify the protected Excel file path
  string myPath = "InteropOutput_ProtectedWorkbook.xlsx";

  //Open the Excel file
  Workbook workbook = excelApp.Workbooks.Open(myPath);

  //Unprotect the protected workbook using the password
  workbook.Unprotect("007");

  //Save the file
  workbook.SaveAs("InteropOutput_UnprotectedWorkbook.xlsx");

  //Quit the application
  excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub UnprotectWorkbook()
  'Instantiate the application object
  Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

  'Specify the protected Excel file path
  Dim myPath As String = "InteropOutput_ProtectedWorkbook.xlsx"

  'Open the Excel file
  Dim workbook As Workbook = excelApp.Workbooks.Open(myPath)

  'Unprotect the protected workbook using the password
  workbook.Unprotect("007")

  'Save the file
  workbook.SaveCopyAs("InteropOutput_UnprotectedWorkbook.xlsx")

  'Quit the application
  excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void UnprotectWorkbook()
{
  using (ExcelEngine excelEngine = new ExcelEngine())
  {
    //Instantiate the application object
    IApplication application = excelEngine.Excel;

    //Open the protected Excel file
    IWorkbook workbook = application.Workbooks.Open("XlsIOOutput_ProtectedWorkbook.xlsx");

    //Unprotect the protected workbook using the password
    workbook.Unprotect("password");

    //Save the file
    workbook.SaveAs("XlsIOOutput_UnprotectedWorkbook.xlsx");
  }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub UnprotectWorkbook()
  Using excelEngine As ExcelEngine = New ExcelEngine()
    'Instantiate the application object
    Dim application As IApplication = excelEngine.Excel

    'Open the protected Excel file
    Dim workbook As IWorkbook = application.Workbooks.Open("XlsIOOutput_ProtectedWorkbook.xlsx")

    'Unprotect the protected workbook using the password
    workbook.Unprotect("password")

    'Save as Excel file
    workbook.SaveAs("XlsIOOutput_UnprotectedWorkbook.xlsx")
  End Using
End Sub
{% endhighlight %}
{% endtabs %}
