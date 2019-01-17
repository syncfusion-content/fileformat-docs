---
title: Merge Cells in Excel
description: This page shows how to merge a range of cells in Excel into a single cell.
platform: file-formats
control: XlsIO
documentation: UG
---

# Merge Cells in Excel

We can merge a continuous range of cells into one large cell. Merged cell keeps the value in the upper-left cell and deletes all other values. Merging cells can be useful if we want to make clear that a label applies to multiple columns.

The following code shows how to merge cells in Excel with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# %}
private void MergeCells()
{
    //Instantiate the Application object.
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a Workbook.
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the range of cells i.e.., A1:C1.
    Range rng1 = excelApp.get_Range("A1", "C1");

    //Merge the cells.
    rng1.Merge(Missing.Value);

    //Save the file.
    workbook.SaveAs(@"d:\test\InteropOutput_MergedCells.xlsx");

    //Quit the Application.
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb %}
Private Sub MergeCells()
    'Instantiate the Application object.
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a Workbook.
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the range of cells i.e.., A1:C1.
    Dim rng1 As Range = excelApp.Range("A1", "C1")

    'Merge the cells.
    rng1.Merge(Missing.Value)

    'Save the file.
    workbook.SaveCopyAs("d:\test1\InteropOutput_MergedCells.xlsx")

    'Quit the Application.
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# %}
private void MergeCells()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the Application object.
        IApplication application = excelEngine.Excel;

        //Create a Workbook.
        IWorkbook workbook = application.Workbooks.Create(1);
        IWorksheet worksheet = workbook.Worksheets[0];

        //Merge Cells from A1 to C1.
        worksheet.Range["A1:C1"].Merge();

        //Save the workbook.
        workbook.SaveAs(@"d:\test\XlsIOOutput_MergedCells.xlsx");
    }
}
{% endhighlight %}

{% highlight vb %}
Private Sub MergeCells()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the Application object.
        Dim application As IApplication = excelEngine.Excel

        'Create a Workbook.
        Dim workbook As IWorkbook = application.Workbooks.Create(1)
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Merge Cells from A1 to C1.
        worksheet.Range("A1:C1").Merge()

        'Save as excel file.
        workbook.SaveAs("d:\test1\XlsIOOutput_MergedCells.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
