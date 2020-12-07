---
title: Activate a Worksheet | Syncfusion
description: Explains with an example on how to programmatically activate a worksheet in a workbook in Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Activate a Worksheet

If there are more worksheets in a workbook, certain worksheets should be active while opening the workbook in Microsoft Excel.

The following code shows how to activate a worksheet in workbook containing three worksheets with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void ActivateWorksheet()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Specify the template Excel file path
    string myPath = @"d:\test\Sample.xlsx";

    //Open the Excel file
    Workbook workbook = excelApp.Workbooks.Open(myPath);

    //Activate the first worksheet by default
    workbook.Sheets[1].Activate();

    //Save as Excel file
    workbook.SaveCopyAs(@"d:\test\InteropOutput_ActivateWorksheet.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub ActivateWorksheet()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Specify the template Excel file path
    Dim myPath As String = "d:\test1\Sample.xlsx"

    'Open the Excel file
    Dim workbook As Workbook = excelApp.Workbooks.Open(myPath)

    'Activate the first worksheet by default
    workbook.Sheets(1).Activate()

    'Save as Excel file
    workbook.SaveCopyAs("d:\test1\InteropOutput_ActivateWorksheet.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void ActivateWorksheet()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Specify the template Excel file path
        string myPath = @"d:\test\Sample.xlsx";

        //Instantiate a new workbook
        //Open the Excel file
        IWorkbook workbook = application.Workbooks.Open(myPath);

        //Activate the first worksheet by default
        workbook.Worksheets[0].Activate();

        //Save as Excel file
        workbook.SaveAs(@"d:\test\XlsIOOutput_ActivateWorksheet.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub ActivateWorksheet()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Specify the template Excel file path
        Dim myPath As String = "d:\test\Sample.xlsx"

        'Instantiate a new workbook
        'Open the Excel file
        Dim workbook As IWorkbook = application.Workbooks.Open(myPath)

        'Activate the first worksheet by default
        workbook.Worksheets(0).Activate()

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_ActivateWorksheet.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
