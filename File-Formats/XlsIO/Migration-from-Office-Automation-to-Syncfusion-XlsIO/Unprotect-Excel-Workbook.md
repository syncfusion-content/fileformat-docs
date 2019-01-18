---
title: Unprotect Excel Workbook | Syncfusion
description: This page shows how to unprotect Excel workbook with password.
platform: file-formats
control: XlsIO
documentation: UG
---

# Unprotect Excel Workbook

Workbooks protected by structure and window can be unprotected with password.

The following code shows how to unprotect Excel workbook using Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void UnprotectWorkbook()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Specify the protected excel file path.
    string myPath = @"d:\test\InteropOutput_ProtectedWorkbook.xlsx";

    //Open the excel file.
    Workbook workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value);

    //Unprotect the protected workbook using the password.
    workbook.Unprotect("007");

    //Save the file.
    workbook.SaveAs(@"d:\test\InteropOutput_UnprotectedWorkbook.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub UnprotectWorkbook()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Specify the protected excel file path.
    Dim myPath As String = "d:\test1\InteropOutput_ProtectedWorkbook.xlsx"

    'Open the excel file.
    Dim workbook As Workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value)

    'Unprotect the protected workbook using the password.
    workbook.Unprotect("007")

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_UnprotectedWorkbook.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void UnprotectWorkbook()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Open the protected excel file.
        IWorkbook workbook = application.Workbooks.Open(@"d:\test\XlsIOOutput_ProtectedWorkbook.xlsx");

        //Unprotect the protected workbook using the password.
        workbook.Unprotect("password");

        //Save the file.
        workbook.SaveAs(@"d:\test\XlsIOOutput_UnprotectedWorkbook.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub UnprotectWorkbook()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Open the protected excel file.
        Dim workbook As IWorkbook = application.Workbooks.Open("d:\test1\XlsIOOutput_ProtectedWorkbook.xlsx")

        'Unprotect the protected workbook using the password.
        workbook.Unprotect("password")

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_UnprotectedWorkbook.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
