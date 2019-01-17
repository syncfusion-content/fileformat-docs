---
title: UnMerge Cells in Excel
description: This page shows how to unmerge cells in Excel.
platform: file-formats
control: XlsIO
documentation: UG
---

# UnMerge Cells in Excel

Merged cells can be unmerged at anytime.

The following code shows how to unmerge cells in Excel with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void UnmergeCells()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Specify the template excel file path.
    string myPath = @"d:\test\InteropOutput_MergedCells.xlsx";

    //Open the excel file.
    Workbook workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value);

    //Get the A1 cell (Merged Cell).
    Range rng1 = excelApp.get_Range("A1", Missing.Value);

    //UnMerge the cell.
    rng1.UnMerge();

    //Save the file.
    workbook.SaveAs(@"d:\test\InteropOutput_UnmergedCells.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub UnmergeCells()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Specify the template excel file path.
    Dim myPath As String = "d:\test\InteropOutput_MergedCells.xlsx"

    'Open the excel file.
    Dim workbook As Workbook = excelApp.Workbooks.Open(myPath, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value, Missing.Value)

    'Get the A1 cell (Merged Cell).
    Dim rng1 As Range = excelApp.Range("A1")

    'UnMerge the cell.
    rng1.UnMerge()

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_UnmergedCells.xlsx")

    'Quit the Application.
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
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Open the excel file containing merged cells.
        IWorkbook workbook = application.Workbooks.Open(@"d:\test\XlsIOOutput_MergedCells.xlsx");
        IWorksheet worksheet = workbook.Worksheets[0];

        //Un-Merge the merged cells from A1 to C1.
        worksheet.Range["A1:C1"].UnMerge();

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_UnmergedCells.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub UnmergeCells()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Open the excel file.
        Dim workbook As IWorkbook = application.Workbooks.Open("d:\test1\XlsIOOutput_MergedCells.xlsx")
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Un-Merge the merged cells from A1 to C1.
        worksheet.Range("A1:C1").UnMerge()

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_UnmergedCells.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
