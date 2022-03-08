---
title: Merge Cells in Excel | Syncfusion
description: Explains with an example on how to merge a range of cells in Excel into a single cell programattically, using Interop and XlsIO.
platform: file-formats
control: XlsIO
documentation: UG
---

# Merge Cells in Excel

You can merge a continuous range of cells into one large cell. Merged cell keeps the value in the upper-left cell and deletes all other values. Merging cells can be useful if you want to make clear that a label applies to multiple columns.

The following code shows how to merge cells in Excel with Interop and XlsIO for .NET.

## Interop

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void MergeCells()
{
    //Instantiate the application object
    var excelApp = new Microsoft.Office.Interop.Excel.Application();

    //Add a workbook
    Workbook workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value);

    //Get the range of cells that is A1:C1
    Range rng1 = excelApp.get_Range("A1", "C1");

    //Merge the cells
    rng1.Merge(Missing.Value);

    //Save the file
    workbook.SaveAs(@"d:\test\InteropOutput_MergedCells.xlsx");

    //Quit the application
    excelApp.Quit();
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub MergeCells()
    'Instantiate the application object
    Dim excelApp = New Microsoft.Office.Interop.Excel.Application()

    'Add a workbook
    Dim workbook As Workbook = excelApp.Workbooks.Add(System.Reflection.Missing.Value)

    'Get the range of cells that is A1:C1
    Dim rng1 As Range = excelApp.Range("A1", "C1")

    'Merge the cells
    rng1.Merge(Missing.Value)

    'Save the file
    workbook.SaveCopyAs("d:\test1\InteropOutput_MergedCells.xlsx")

    'Quit the application
    excelApp.Quit()
End Sub
{% endhighlight %}
{% endtabs %}

## XlsIO

{% tabs %}
{% highlight c# tabtitle="C#" %}
private void MergeCells()
{
    using (ExcelEngine excelEngine = new ExcelEngine())
    {
        //Instantiate the application object
        IApplication application = excelEngine.Excel;

        //Create a workbook
        IWorkbook workbook = application.Workbooks.Create(1);
        IWorksheet worksheet = workbook.Worksheets[0];

        //Merge cells from A1 to C1
        worksheet.Range["A1:C1"].Merge();

        //Save the workbook
        workbook.SaveAs(@"d:\test\XlsIOOutput_MergedCells.xlsx");
    }
}
{% endhighlight %}

{% highlight vb.net tabtitle="VB.NET" %}
Private Sub MergeCells()
    Using excelEngine As ExcelEngine = New ExcelEngine()
        'Instantiate the application object
        Dim application As IApplication = excelEngine.Excel

        'Create a workbook
        Dim workbook As IWorkbook = application.Workbooks.Create(1)
        Dim worksheet As IWorksheet = workbook.Worksheets(0)

        'Merge cells from A1 to C1
        worksheet.Range("A1:C1").Merge()

        'Save as Excel file
        workbook.SaveAs("d:\test1\XlsIOOutput_MergedCells.xlsx")
    End Using
End Sub
{% endhighlight %}
{% endtabs %}
