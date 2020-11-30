---
title: Unmerge Cells in Excel | Syncfusion
description: Explains with an example on how to unmerge cells in Excel using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Unmerge Cells in Excel

Merged cells can be unmerged at anytime.

The following code shows how to unmerge cells in Excel with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void UnmergeCells()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Specify the template Excel file path
    string myPath = @"d:\test\InteropOutput_MergedCells.xlsx";

    //Open the Excel file
    Workbook workbook = excelApp.Workbooks.Open(myPath);

    //Get the A1 cell (merged cell)
    Range rng1 = excelApp.get_Range("A1", Missing.Value);

    //Unmerge the cell
    rng1.UnMerge();

    //Save the file
    workbook.SaveAs(@"d:\test\InteropOutput_UnmergedCells.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub UnmergeCells()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Specify the template Excel file path
    Dim myPath As String = "d:\test\InteropOutput_MergedCells.xlsx"

    'Open the Excel file
    Dim workbook As Workbook = excelApp.Workbooks.Open(myPath)

    'Get the A1 cell (merged cell)
    Dim rng1 As Range = excelApp.Range("A1")

    'Unmerge the cell
    rng1.UnMerge()

    'Save the file
    workbook.SaveCopyAs("d:\test1\InteropOutput_UnmergedCells.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void UnmergeCells()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Open the Excel file containing merged cells
        IWorkbook workbook = application.Workbooks.Open(@"d:\test\XlsIOOutput_MergedCells.xlsx");
        IWorksheet worksheet = workbook.Worksheets[0];

        //Unmerge the merged cells from A1 to C1
        worksheet.Range["A1:C1"].UnMerge();

        //Save the workbook
        workbook.SaveAs(@"d:\test\XlsIOOutput_UnmergedCells.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub UnmergeCells()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Open the Excel file
        Dim workbook As IWorkbook = application.Workbooks.Open("d:\test1\XlsIOOutput_MergedCells.xlsx")
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Unmerge the merged cells from A1 to C1
        worksheet.Range("A1:C1").UnMerge()

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_UnmergedCells.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
