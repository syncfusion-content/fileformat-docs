---
title: Wrap Text in Excel | Syncfusion
description: Explains with an example on how to apply wrap text in Excel that allows to fit a long text in a single cell using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# How to apply Wrap Text in Excel

When a text is too long for the width of a cell, the lengthy text will spill over into the cell right to it, if it is an empty cell. But, if the cell right to is occupied, only a portion of the lengthy text appears. Wrapping text is a key feature, which wraps text in Excel and allows fitting a long text in a single cell.

The following code shows the comparison of some lengthy text in a cell with and without wrapping using Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void WrapText()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a workbook
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the first sheet
    Worksheet sheet = workbook.Sheets["Sheet1"];

    //Place some text in cell A1 without wrapping
    Microsoft.Office.Interop.Excel.Range cellA1 = sheet.Cells.get_Range("A1");
    cellA1.Value = "Sample Text Unwrapped";

    //Place some text in cell A2 with wrapping
    Microsoft.Office.Interop.Excel.Range cellA2 = sheet.Cells.get_Range("A2");
    cellA2.Value = "Sample Text Wrapped";
    cellA2.WrapText = true;

    //Save the Excel file
    workbook.SaveCopyAs("InteropOutput_WrapText.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub WrapText()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a workbook
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the first sheet
    Dim sheet As Worksheet = workbook.Sheets("Sheet1")

    'Place some text in cell A1 without wrapping
    Dim cellA1 As Microsoft.Office.Interop.Excel.Range = sheet.Cells.Range("A1")
    cellA1.Value = "Sample Text Unwrapped"

    'Place some text in cell A2 with wrapping
    Dim cellA2 As Microsoft.Office.Interop.Excel.Range = sheet.Cells.Range("A2")
    cellA2.Value = "Sample Text Wrapped"
    cellA2.WrapText = True

    'Save the Excel file
    workbook.SaveCopyAs("InteropOutput_WrapText.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void WrapText()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the first sheet
        IWorksheet worksheet = workbook.Worksheets[0];

        //Place some text in cell A1 without wrapping
        IRange cellA1 = worksheet.Range["A1"];
        cellA1.Value = "Sample Text Unwrapped";

        //Place some text in cell A2 with wrapping
        IRange cellA2 = worksheet.Range["A2"];
        cellA2.Value = "Sample Text Wrapped";
        cellA2.WrapText = true;

        //Save the workbook
        workbook.SaveAs("XlsIOOutput_WrapText.xlsx");
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub WrapText()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Create a workbook
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the first sheet
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Place some text in cell A1 without wrapping
        Dim cellA1 As IRange = worksheet.Range("A1")
        cellA1.Value = "Sample Text Unwrapped"

        'Place some text in cell A2 with wrapping
        Dim cellA2 As IRange = worksheet.Range("A2")
        cellA2.Value = "Sample Text Wrapped"
        cellA2.WrapText = True

        'Save as Excel file
        workbook.SaveAs("XlsIOOutput_WrapText.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
