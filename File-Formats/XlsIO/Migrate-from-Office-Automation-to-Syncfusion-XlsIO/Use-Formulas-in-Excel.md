---
title: Use Formulas in Excel | Syncfusion
description: Explains with an example on how to use formulas or functions (predefined formulas) in Excel using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Use Formulas in Excel

A formula is an expression that operates on values in a range of cells or a cell. Functions are predefined formulas in Excel.

The following code shows how to use formulas in Excel by adding values in a range of cells using the formula function sum and highlighting the resultant value with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight C# %}
private void ExcelFormulas()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a workbook
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the first sheet
    Worksheet worksheet = workbook.Sheets["Sheet1"];

    //Access cells A1, A2, A3, and A4
    Range cellA1 = worksheet.Range["A1"];
    Range cellA2 = worksheet.Range["A2"];
    Range cellA3 = worksheet.Range["A3"];
    Range cellA4 = worksheet.Range["A4"];

    //Set integer values in cells A1, A2, and A3
    cellA1.Value = 10;
    cellA2.Value = 20;
    cellA3.Value = 30;

    //Add formula in cell A4
    cellA4.Formula = "=Sum(A1:A3)";

    //Set the font bold in cell A4
    cellA4.Font.Bold = true;

    //Set the background color to yellow in cell A4
    cellA4.Interior.Color = XlRgbColor.rgbYellow;

    //Save the Excel file
    workbook.SaveCopyAs(@"d:\test\InteropOutput_ExcelFormulas.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight VB.NET %}
Private Sub ExcelFormulas()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a workbook
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the first sheet
    Dim worksheet As Worksheet = workbook.Sheets("Sheet1")

    'Access cells A1, A2, A3, and A4
    Dim cellA1 As Range = worksheet.Range("A1")
    Dim cellA2 As Range = worksheet.Range("A2")
    Dim cellA3 As Range = worksheet.Range("A3")
    Dim cellA4 As Range = worksheet.Range("A4")

    'Set integer values in cells A1, A2, and A3
    cellA1.Value = 10
    cellA2.Value = 20
    cellA3.Value = 30

    'Add formula in cell A4
    cellA4.Formula = "=Sum(A1:A3)"

    'Set the font bold in cell A4
    cellA4.Font.Bold = True

    'Set the background color to yellow in cell A4
    cellA4.Interior.Color = XlRgbColor.rgbYellow

    'Save the file
    workbook.SaveCopyAs("d:\test1\InteropOutput_ExcelFormulas.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight C# %}
private void ExcelFormulas()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);

        //Get the first sheet
        IWorksheet worksheet = workbook.Worksheets[0];

        //Access cells A1, A2, A3, and A4
        IRange cellA1 = worksheet.Range["A1"];
        IRange cellA2 = worksheet.Range["A2"];
        IRange cellA3 = worksheet.Range["A3"];
        IRange cellA4 = worksheet.Range["A4"];

        //Set integer values in cells A1, A2, and A3
        cellA1.Value2 = 10;
        cellA2.Value2 = 20;
        cellA3.Value2 = 30;

        //Add formula in cell A4
        cellA4.Formula = "=Sum(A1:A3)";

        //Set the font bold in cell A4
        cellA4.CellStyle.Font.Bold = true;

        //Set the background color to yellow in cell A4
        cellA4.CellStyle.Interior.Color = Color.Yellow;

        //Save the workbook
        workbook.SaveAs(@"d:\test\XlsIOOutput_ExcelFormulas.xlsx");
    }
}
{% endhighlight %}

{% highlight VB.NET %}
Private Sub ExcelFormulas()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Create a workbook
        Dim workbook As IWorkbook = application.Workbooks.Create(1)

        'Get the first sheet
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Access cells A1, A2, A3, and A4
        Dim cellA1 As IRange = worksheet.Range("A1")
        Dim cellA2 As IRange = worksheet.Range("A2")
        Dim cellA3 As IRange = worksheet.Range("A3")
        Dim cellA4 As IRange = worksheet.Range("A4")

        'Set integer values in cells A1, A2, and A3
        cellA1.Value2 = 10
        cellA2.Value2 = 20
        cellA3.Value2 = 30

        'Add formula in cell A4
        cellA4.Formula = "=Sum(A1:A3)"

        'Set the font bold in cell A4
        cellA4.CellStyle.Font.Bold = True

        'Set the background color to yellow in cell A4
        cellA4.CellStyle.Interior.Color = Color.Yellow

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_ExcelFormulas.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
